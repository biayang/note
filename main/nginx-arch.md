# nginx arch

## 架构
![ img ](res/nginx-arch.png)
![ img ](res/nginx-inner.png)

### 主进程
Nginx 启动时，会生成两种类型的 进程 *，一个是 主进程 （ master ）， 一个 （ windows版本的目前只有一个）或 多个工作进程 （ worker ）。 主进程 并不处理网络请求，主要负责 调度工作进程 ，也就是图示的 3 项： 加载配置 、 启动工作进程 及 非停升级 。所以， Nginx 启动以后，查看操作系统的进程列表，我们就能看到 至少有两个 Nginx 进程。

### 工作进程
服务器实际 处理网络请求 及 响应 的是 工作进程 （ worker ），在类 unix 系统上， Nginx可以配置 多个 worker ，而每个 worker 进程 都可以同时处理 数以千计 的 网络请求 。

### 模块化设计
Nginx 的 worker 进程，包括 核心 和 功能性模块 ， 核心模块 负责维持一个 运行循环 （ run-loop ），执行网络请求处理的 不同阶段 的模块功能，比如： 网络读写 、 存储读写 、 内容传输 、 外出过滤 ，以及 将请求发往上游服务器 等。而其代码的 模块化设计 ，也使得我们可以根据需要对 功能模块 进行适当的 选择 和 修改 ，编译成具有 特定功能 的服务器。

### 事件驱动模型
基于 异步及非阻塞 的 事件驱动模型 ，可以说是 Nginx 得以获得 高并发 、 高性能 的关键因素，同时也得益于对 Linux 、 Solaris 及类 BSD 等操作系统内核中 事件通知 及 I/O 性能增强功能 的采用，如 kqueue 、 epoll 及 event ports 。

### 代理（proxy）设计
代理设计，可以说是 Nginx 深入骨髓的设计，无论是对于 HTTP ，还是对于 FastCGI 、 Memcache 、 Redis 等的网络请求或响应，本质上都采用了 代理机制 。所以， Nginx 天生就是高性能的 代理服务器 。

## 进程模型
### master / worker 多进程模型
![ img ](res/nginx-proc.png)
1. 主程序 Master process 启动后，通过一个 for 循环来 接收 和 处理外部信号  
2. 主进程通过 fork() 函数产生 worker 子进程 ，每个子进程执行一个 for 循环来实现 Nginx 服务器对事件的接收和处理 。
3. 进程间通讯(master-worker, worker-worker)通过管道

> **master先建立好需要listen的socket（listenfd）**之后，然后再fork出多个worker。所有worker进程的listenfd会在新连接到来时变得可读，**所有worker进程抢占accept_mutex**，抢到互斥锁的那个进程**注册listenfd读事件**，在读事件里调用accept接受该连接。以保证只有一个进程处理该连接。

## 实战
推荐worker**进程数与CPU内核数一致**。避免了进程之间竞争CPU资源和进程切换的开销

nginx提供了**CPU亲缘性的绑定选项**，一个进程绑定在某一个核上，这样就不会因为进程的切换带来Cache的失效。  
