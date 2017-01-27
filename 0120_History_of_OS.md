# 0119_Advanced_OS
* General purpose
* Complexity
    * Debugging
    * Correctness
        * No safety rails
* Timing and Interrupts
* Abstractions
    * CPU sequential process
        * Abstract away interrupts, context swtiches and timing
    * Mem & Storage
        * Virtual segments
    * I/O
        * Use seq process write to shared mem with signal a semaphore
* Organization
    * Dependencies between CPU and Mem and I/O
        * Layers
            * Seq Processes
            * VM 
        * Advantages of Layering
            * testing could be easy (just make sure the underlying layer works correctly)
        * Disadvantage:
            * Cannot be divided clearly into layers


* UNIX
    * Motivation: Hackers/ Programmers   convenient to use
    * Organizations: treat things like files
        * Single namspace
        * Interactivity
        * Lots of small processes
            * Compose programs
        * System Services are programs or small processes
        * Little program
        * Pipes for Inter-processes-communicating
        * File API including piples, TTYs, Dev and Files
        * High Level Languages