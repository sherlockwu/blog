# LabRef 使用
Latex下使用的索引管理工具 BibTex files(papers 的metadata?) 

两个版本standalone or web
所以我认为就是 能够 生成索引文件的软件而已？ 

## BibTex格式
文献的Metadata,很多下载网站都适用于BibTex的导出（其实也就是一小段格式化的代码而已） 

我认为关键是把整个管理文献的过程弄熟就好！

# 管理过程 
1. 下载BibTex数据
2. 导入到LabRef 数据库（这部分还不知道 ）
3. LabRef 会重新生成每个BibTexKey, 将paper的pdf文件按照BibTexKey重命名(这是为了方便直接点击阅读paper文档的)
4. 在tex文件中添加参考文献目录（一段代码，包括在头部，和document中的两部分）
5. 之后每次cite，加一个
6. 还能规定显示什么样的索引项

# 在Latex中cite
* 在documentclass 后面
```
\bibliographystyle{IEEEtran}
\bibliography{IEEEabrv,你的bib文件名称}
%%第一行是用来启用IEEEtran的引文功能，第二行将IEEE会议缩写、和你自己定义的bib引文文件都包含进来。
```
* 之后` \cite{文章索引名称}`


## Reference
1. [知乎“管理文献全过程”解答](https://www.zhihu.com/question/23565739)
