## 为什么要使用Node

### 目录

- [Node能够解决什么问题](#Node能够解决什么问题)
  - [什么是进程](#什么是进程)
  - [什么是线程](#什么是线程)
  - [什么是多线程](#什么是多线程)
    - [多线程的优势](#多线程的优势)
    - [多线程的劣势](#多线程的劣势)
  - [什么是单线程](#什么是单线程)
  - [同步和异步](#同步和异步)
  - [同步异步/阻塞非阻塞](#同步异步/阻塞非阻塞)
  - [Node是什么](#Node是什么)
  - [Node使用场景](#Node使用场景)

### Node能够解决什么问题

- Java是多线程语言，在处理高并发上存在一定短板；Node是单线程的，可以很好的处理这个问题。

- 说到线程，那么再讲下进程和线程的概念以及区别。

#### 什么是进程

当一个程序开始运行时，它就是一个进程，进程包括运行中的程序和程序所使用到的内存和系统资源。

而一个进程又是由多个线程所组成的。

#### 什么是线程

线程是程序中的一个执行流，每个线程都有自己的专有寄存器(栈指针、程序计数器等)，但代码区是共享的，即不同的线程可以执行同样的函数。

#### 什么是多线程

多线程是指程序中包含多个执行流，即在一个程序中可以同时运行多个不同的线程来执行不同的任务，也就是说允许单个程序创建多个并行执行的线程来完成各自的任务。

##### 多线程的优势

可以提高CPU的利用率。在多线程程序中，一个线程必须等待的时候，CPU可以运行其它的线程而不是等待，
这样就大大提高了程序的效率。 

##### 多线程的劣势

- 线程也是程序，所以线程需要占用内存，线程越多占用内存也越多； 
- 多线程需要协调和管理，所以需要CPU时间跟踪线程； 
- 线程之间对共享资源的访问会相互影响，必须解决竞用共享资源的问题；
- 线程太多会导致控制太复杂，最终可能造成很多Bug；

#### 什么是单线程

顾名思义，一个程序中只有一个线程，任何操作都基于此线程，那么就存在一个阻塞问题。

#### 同步和异步

同步和异步关注的是消息通知机制

- 同步就是发出调用后，没有得到结果之前，该调用不返回，一旦调用返回，就得到返回值了。 简而言之就是调用者主动等待这个调用的结果
- 而异步则相反，调用者在发出调用后这个调用就直接返回了，所以没有返回结果。换句话说当一个异步过程调用发出后，调用者不会立刻得到结果，而是调用发出后，被调用者通过状态、通知或回调函数处理这个调用。

#### 同步异步/阻塞非阻塞

上面是书本上比较枯燥的概念，下面举一个生活中的例子便于理解同步异步和阻塞非阻塞的关系。

现在有一个场景，一个男生当面向一个女生表白。在程序中男生对应着客户端即调用者，女生对应着服务端即被调用者。

男生向女生表白后可能发生如下几种情况：

- 女生说你等着我一会给你答复。这个等着的过程对于女生（被调用者）来说是同步的，但是对于男生（调用者）来说就是阻塞的。
- 女生说你先回去干别的事儿，我思考两天再给你答复。这两天对于女生（被调用者）来说是异步的，对于男生（调用者）来说也就是非阻塞的，他可以在此期间再向别的女生表白或干别的事儿，等女生想好了再通知他。

上面说到同步阻塞、异步非阻塞，当然还有另外两种情况（同步非阻塞、异步阻塞），我们在此暂不讨论。

#### Node是什么

在Node中写了一个[libuv](https://github.com/libuv/libuv)库，采用了异步非阻塞的思想，底层实际上使用了多线程来实现的。

Node使用了事件驱动、非阻塞式I/O的模型，使其轻量又高效

Node能火起来最大的一个原因在于包管理器`npm`，它是全球最大的开源库生态系统。

#### Node使用场景

- 现在各个公司都在主推的**前后端分离**中，使用Node做中间层。
  - 前后端分离，那就必然存在跨域问题，使用Node做一层接口封装，这个过程不会跨域，Node也在前端控制，对于前端也不会跨越。即解决跨域问题。
  - 当然还能通过`Nginx`解决跨域问题。引入Node也主要是为了让后端职责更专注于逻辑处理，对于一些数据转换完全可以交由前端处理，使得职责更加分明。

- 当应用程序需要处理高并发场景时，多线程语言中如Java会耗费大量内存，是并不推荐的。
  - 聊天服务器：大量并发的输入输出
  - 电子商务网站：无过复杂逻辑，大量并发的输出（大量用户同一时间浏览网站）