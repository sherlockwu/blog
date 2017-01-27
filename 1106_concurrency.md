# Concurrency
##  Threads
* Use multiple cores: multi-threads, parallely, cooperatively working
* Producer/ consumer; Pipeline; Defer work with background thread
* 共享的东西：
    * code&heap, pagedir  (stack和一些寄存器是自己独有的）
    * file descriptiors, 当前directory等
* 对比线程 和 进程：
    * 进程是CPU分配资源的基本单位（线程是CPU调度的基本单位，一个线程阻塞可以是同进程的其他线程，也可以是其他进程的线程上来执行），但是现代CPU可以同时执行多个任务（multi-cores），相当于process中的多个threads
    * 在context switch 的时候存独有的registers等
* 实现threads
    * User-level: 完全由库实现，OS不知道
    * Kernel-level: 轻量级的进程 (能使用multiprocessor 并行)
* Concurrency 的问题
    * 会导致non-determinisitic的结果： race conditions
    * 解决方案： 用一些硬件的东西实现我们能用的保证synchronization的原语
* 引入 Locks  但是有代价的，小一点比较好 
* API'
    * pthread_create用法
    ```
    int pthread_create(pthread_t *restrict tidp,const pthread_attr_t *restrict attr,
    void *(*start_rtn)(void),void *restrict arg);
    Returns: 0 if OK, error number on failure
    ```
    * pthread_join
    等待一个线程的结束（block）， 一般在主线程中，防止主线程很快结束导致整个进程结束了

## Handle issues from concurrency
#### Lock (atomicity, excluded use)
* Lock
* 实现 （一些目标）
    * 保证正确性 使用 atomic operations （mutual exclusion; 有一个一定能获得锁； 不会被饿死）
        * 只要不交出CPU就肯定原子执行 (acquire disableInterrupts) 只能在uniprocessor 上用
        * load/ store words
            * 单纯的读判断，然后修改不行（因为load 和 store 之间不是原子的）
            * 使用Peterson Algorithm实现：
                * lock[0,1] 判断别的thread想不想要； turn判断谁先想要的
                * 只有别人不想要，或者是自己的轮的时候，可以 进入 （否则循环）
                * 但是没有sequential consistency， 在caching的情况下
        * Test&Set
            * XCHG(addr, newval) 指令（返回addr的旧值，并置为newval，原子）
                * while ( XCHG(&lock, 1) == 1) ; 出来就知道获得锁了
        * Compare&Swap
            * CompareAndSwap(addr, expected, new) （返回addr中的值，如果等于expected就置为new）
                * while(CompareAndSwap(&lock, 0, 1) == 1) ;  出来就知道获得了锁 
    * Fairness:
        * 保证能按请求lock的顺序得到lock  (ticket, turn)
        * 使用 FetchAndAdd(* ticket) 原子操作（查，然后++）
        * 每个进程acquire时，FAA(ticket)（表示他能拿到锁的histurn，然后等待turn到达ticket）
        * release时，FAA(turn)
* Spinlock/ Yield/ Block
    * Spinlock 就是一直等锁，直到被换下
    * yield 就是被schedule上来之后检查一下，没有就yield cpu（被换下，但是下次能被换上来）
    * acquire不到锁就 被block，变成waiting （不能被换上）， 然后unlock的时候，被置为runnable
        * 使用park， unpark， setpark 实现
        * 有一个等待lock的queue （因为是block，所以需要）
    * spin vs block： 需要比较 等待时间t 和 context switch waste C （折中的方法是，先spin等C， 不行block）

#### 条件判断执行（高效）
* CV 
    * join
        * 一定还是要给条件相关的操作 加锁
    * Producer/ Consumer 问题
        * 先写条件-> 然后分到各个thread
        * 1 consumer/ 1 producer 一个cv就行
        * 多个threads， 公用一个可能唤醒不expected的thread
        * broadcast 唤醒的作用 
    * 含义
        * 可以是别人唤醒，或者干脆就是自己判断条件成立
        * 等的是一个条件，但是本质上也是某种资源
    * 操作
        * wait(cv, lock) 等待cv->sleep并release锁
        * signal(cv) wake一个thread （但不确保他能下一个拿到锁，下一个被schedule）
    * 三条：
        * 必须先拿锁
        * 不同条件判断要用不同锁
        * while 判断
    * 很好的实例:

    ```
    总的来说，给条件变量发送信号的代码大体如下：
    pthread_mutex_lock(&mutex);
    设置条件为真
    pthread_mutex_unlock(&mutex);　　
    pthread_cond_signal(&cond);　　//发送信号

    等待条件并进入睡眠以等待条件变为真的代码大体如下：
    pthread_mutex_lock(&mutex);　
    while(条件为假)
　　     pthread_cond_wait(&cond,&mutex);　　
    执行某种操作
    pthread_mutex_unlock(&mutex);
    ```

* Semaphores
    * 含义
    * 操作  （因为wait, post 的semantics不变，所以我们要从这个想含义）
        * init 设integer值
        * wait 直到sem>0 -- 
        * post ++ wake 一个(一定要注意这个)
    * 和cv lock的关系   equally powerful to Locks&CVs
        * 互相实现 （用sem实现cv很难）
    * 实例
        * 实现Producer/ Consumer
        * 多producer, consumer 的时候要注意确定不同threads写入恰当的位置(确定这个位置又需要锁了)
* 读写锁
    * 可以用sem 实现 
    * 一般读都可以读（但是因为要改readers数量，所以需要给结构加锁（再来一个sem））
    * write 只要等writelock就可以 （write之后的所有read也要block，否则write饿死了） 
    * 需要几个信号量： 还需要自己回顾一下

#### Cases (producer/ consumer, reader/ writer )
* Monitor language级别自动帮我们（java: synchronized）
* Dining Philosophers
    * 同时需要左边和右边的 资源（五个sem就好）
    * 先拿右，再等左 （deadlock）
    * 哲学家就餐问题的实现 判断左边和右边的人是不是都不在eating(就可以signal,因为是sem，没有问题）, 当有个筷子放下可以帮助隔壁的两个人判断（signal）
* Reader/Writer locks
    * Read priority
        * write 等 writer lock
        * 读的第一个sem_wait(writer lock), 然后最后一个才放
    * Write priority
        * 
* Bugs:
    * 死锁：
        * 四个条件：
            * mutual exclusion (一个资源是独占的)
                * 将锁换成原子操作
            * hold-and-wait (会hold一个资源等别的资源)
                * 要不全acquire，要不全不acquire；  （将几个请求lock的操作定位临界区）
                * 需要知道哪些可能会竞争，最大限度的限定
            * no preemption (无法抢占资源)
                * 如果没办法全获得，就全部release   （可能livelock, back-off 解决）
                * trylock 失败 就全 release
            * circular wait (循环等待) 
                * 制定去的一系列锁的 一个顺序
#### Ref

[一个cv和lock区别的讲解](http://www.cnblogs.com/lonelycatcher/archive/2011/12/20/2294161.html)
[说的挺好的semphore](http://blog.csdn.net/yusiguyuan/article/details/14161225)
[综述的挺好的blog](http://blog.csdn.net/yusiguyuan/article/details/14160081)
[讲线程和进程](http://www.cnblogs.com/CareySon/archive/2012/05/04/ProcessAndThread.html)
