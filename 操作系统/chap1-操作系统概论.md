## chap1 操作系统概论

#### outline
1.1 操作系统的定义  
1.2 操作系统的形成与发展  
1.3 操作系统功能、服务和特性    
1.4 操作系统的进一步发展    
1.5 用户与操作系统接口  
1.6 操作系统的运行环境  
1.7 操作系统的设计规范和结构设计    

---
#### 1.1 操作系统的定义
1.  计算机系统从下到上划分为四个层次。   
    ![](https://i.screenshot.net/4dnovux)
    * 硬件层由计算机的硬件资源组成，包括中央处理机（CPU）、存储器、输入输出设备。
    * 操作系统只包含操作系统内核。如Windows系统的Ntoskrnl.exe。
    * 实用程序包括：语言编译程序、文本编辑程序、调试排错程序、链接装配和装入程序等。
    * **单向调用关系**：外层的软件必须以事先约定的方式调用内层软件或硬件提供的服务。称这种约定为**接口**。

2.  操作系统的设计目标：
    * 方便性
    * 有效性
    * 便于设计、实现、维护

#### 1.2 操作系统的形成与发展
1.  顺序处理（手工操作）
    >没有操作系统，程序员直接操作计算机硬件，调度程序作业
    >作业步骤：编写程序、编译程序、链接装配程序、装入可执行程序
2.  简单批处理系统
    * 单道批处理系统
    >有一个监控程序软件常驻内存（主存），操作员将多个作业按序成批地放在一个输入设备上。监控程序自动控制输入设备，一次装入一道作业，并启动运行。比如早期联机批处理、脱机批处理。
3. 多道批处理系统
    >随着硬件通道、中断、缓冲技术等的出现，使得计算机在组织结构上发生了重大变革。使原先以CPU为中心的体系结构，转变为以主存为中心。
    >多道程序设计：是指在主存同时存放多个作业，使之同时处于运行状态，共享系统中的各种资源，根本目的是提高CPU利用率，在单处理机上，宏观并行，微观串行。

    
    >通道：
独立于CPU，专门用来控制输入/输出设备的<u>I/O</u><u>处理机</u>，比CPU便宜。连接着主存和外设。使CPU和外设并行操作。
    > 中断：
    > 当I/O设备完成传输后，通过中断机构向CPU报告完成情况。
    
    > 缓冲：
    > 在主存设置缓冲区，用来缓存用户的输入输出，改善IO设备和主存、CPU之间的速度不匹配问题。
    
    * 批处理系统的特点
        * 优点：系统吞吐量大、资源利用率高，适合计算量大、自动化程度高的成熟作业。
        * 缺点：用户与作业无法交互，作业平均周转时间长（周转时间包含等待时间，进入——》离开）
    
3.  分时系统
    * 工作方式
    > 一台主机连接有若干个终端。用户交互式地向系统提出命令请求，系统接受命令，采用时间片轮转方式处理请求，并在终端上显示结果。如在大型数据库上j的查询。
    > 多用户分时使用CPU。将CPU的单位时间(如1秒钟)划分成若干个时间片，用户并不会有多人共同使用的感觉，比如Linux Xrdp。
    * 分时系统的特点
    同时性、独立性、交互性、及时性。
4.  实时系统
    * 定义
    >对随机发生的外部事件做出实时响应，是一个**专用系统**。
    >不以作业为处理对象，只有几个由外部事件触发的任务：**实时过程控制**、**实时信息处理**
    * 特点
        * 实时性
        * 可靠性
        * 确定性

6.  嵌入式系统
通常是一个，多任务可抢占式的实时操作系统，只有满足实际需求的有限功能，比如任务调度，同步与通信，主存管理，时钟管理。
嵌入式Linux， Windows CE，智能卡操作系统等。

#### 1.3 功能、服务和特性
1. 三种基本类型：批处理系统；分时系统；实时系统。
2. 通用操作系统：兼有批处理、分时和实时三者或其中两者的功能。
    > 分时和批处理相结合，将分时任务作为前台任务，将批处理作业作为后台任务，便是分时批处理系统。
3. 操作系统的功能
    *   处理机管理：进程管理
    *   存储器管理：主存、外存管理
    *   设备管理：涉及对系统中各种输入、输出设备的管理和控制。
    *   文件管理：
4. 系统资源的当前状态信息
    > 进程——进程表
    > 存储器——存储表
    > I/O设备——I/O设备表
    > 文件——文件表
5. 操作系统同提供的服务
    >**用户接口**：用户通过OS来使用计算机
**程序执行**：装入内存执行，结束执行
I/**O操作**：可能涉及到文件或I/O设备
**文件系统操作**：向用户提供按名存取文件
**通信服务**：进程之间（共享内存/消息传递）
**错误检测和处理**：能检测和处理错误
**资源分配**：多进程并发，资源共享
**记帐**：统计用户对系统资源的使用情况
**保护**：控制用户有限制地存取系统资源

6. 操作系统的特性
    * 并发性（支持系统并发性的物质基础是资源共享）
    * 共享性
    * 虚拟性（把共享资源的一个物理实体变为若干个逻辑上的对应物。如，CPU的分时共享；虚拟存储器技术。）
    * 异步性（即随机性）

#### 1.4 操作系统的进一步发展
1. 个人计算机操作系统
    * 单用户单任务OS：MD-DOS
    * 单用户多任务OS：Windows
    * 多用户多任务OS：Unix、Linux
2. 多处理机操作系统
    * 非对称多处理(ASMP)
    > 主处理机运行操作系统，其他处理机运行用户作业，主处理机为其他处理机分配和调度任务，主从模式。
    * 对称多处理(SMP)
    > 操作系统和用户程序可安排在任何一个处理机上运行，各处理机共享主存和各种I/O设备。
3. 网络操作系统
    > 网络中的各台计算机都配有各自独立的操作系统。
    > 网络操作系统把它们联系起来，并为它们提供通信和网络资源共享。
   * 网络操作系统的模式
        * 客户/服务器（Client/Server)模式。服务器是一个瓶颈。
        * 对等模式 P2P。系统内的节点机（nodes）是对等的，既可作为客户机，又可作为服务器。

4. 分布式操作系统
    * 定义
        > 分布式系统：是由多个分散的计算机通过网络连接而成的计算机系统。可以获得极高的运算能力和广泛的数据共享。
        >
        > 对等模式则是对每一个计算机形成一个计算机系统，对等模式所有的机器既可以当客户机又可以当服务器
        > 
        > 对分布式系统来说，整个机群（cluster）是一个服务器，统一调度分配资源。
    
    
    
  
1.5 用户与操作系统接口
1. 接口
    * 操作接口（命令语言+窗口界面）
    * 编程接口（系统调用是用户与操作系统nei内核之间的编程接口）
2. 命令语言
    > Linux的1号进程为每个终端用户建立一个运行 **shell命令解释程序** 的终端进程，该进程不断地处理用户发来的命令。
3. 窗口界面
    > Windows为终端用户生成了一个运行Explorer.exe程序的进程，打开一个桌面窗口, Explorer.exe程序它是一个具有窗口界面的解释程序。当点击桌面内的某个实用程序时，解释程序就会产生一个新进程。
4. 系统调用
    > 用户通过系统调用接口，运行系统内核里的一些子程序。
    > Windows系统提供的Win32 API函数集合，是一些库函数，由库函数去调用系统调用。
    > 
    系统调用执行过程    
      ![系统调用](https://i.screenshot.net/eyrgeik)
     
5. CPU运行状态：用户态和核心态
    * 计算机两类程序：操作系统内核程序、用户程序
    * 处理机状态字（PSW）中有2个执行方式位。00为核心态，11为用户态。
        > 在核心态下， 允许执行处理机的全部指令集，访问所有的**寄存器和存储区**；
        > 在用户态下，只允许执行处理机的**非特权指令**，访问指定的寄存器和存储区。
        > 用户态到核心态的转换由硬件完成；核心态到用户态的转换由内核程序执行后完成。
    * 操作系统大部分功能模块运行在核心态， 极个别功能模块通过创建用户级进程（比如窗口界面）运行在用户态。例如， Windows子系统进程Csrss.exe，为用户提供窗口界面。极个别内核程序可能运行在用户态。

#### 操作系统的运行环境
1. 中断
    * 异步时间
    * 重要的并发性来源
    * 内核代码触发软件中断切换线程
    * 中断优先级和处理机优先级
2. 异常
    * 同步事件，程序自己的特殊事件，一旦出现立即处理
    * **系统调用**、非法操作码、地址越界、除数为0等

3. 通过**中断和异常**，CPU能从**用户程序**的运行转入操作系统**内核程序**的运行。
4. 中断或者异常发生——》中断处理程序 和 系统调用程序启动——》保护进程运行现场——》CPU控制权交给OS内核——》OS利用 用户进程 的 核心栈空间， 把 内核程序 嵌入到用户进程中运行。

#### OS设计规划
>系统效率：体现系统效率的指标有资源利用率、吞吐量、周转时间、响应时间等。
系统可靠性：系统发现、诊断和恢复故障的能力。
可移植性：指从一种硬件环境移植到另一种硬件环境，系统仍能正常工作。
可伸缩性：系统对添加软、硬件资源的适应能力。
兼容性：系统执行为其他OS或为同一系统早期版本所编写的软件的能力。   
安全性：系统应具有一定的安全保护措施。


#### Q&A
> 1  早期操作系统设计的主要目标是什么?  
> 2  操作系统是资源管理程序，它管理系统中的什么资源？   
> 3  为什么要引入多道程序系统?它有什么特点？    
> 4  叙述操作系统的基本功能。   
> 5  批处理系统、分时系统和实时系统各有什么特点?各适合应用于哪些方面?   
> 6  操作系统的特性?    
> 7  衡量OS的性能指标有哪些？什么是吞吐量、响应时间和周转时间？ 
> 8  什么是嵌入式系统？ 
> 9  什么是对称多处理？它有什么好处？   
> 10  为了实现系统保护，CPU通常有哪两种工作状态？各种状态下分别执行什么程序？什么时候发生状态转换？状态转换由谁实现的？ 
> 11  什么是系统调用？什么是特权指令？特权指令执行时，CPU处于哪种工作状态？ 
> 12  操作系统通常向用户提供哪几种类型的接口?其主要作用是什么?  




