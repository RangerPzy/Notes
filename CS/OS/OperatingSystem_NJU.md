# 操作系统-NJU

[TOC]

# 复习指南

1.  根据往年卷看看哪里会了。
2.  **对应地**，看看书本和拔尖班的资料和OSTEP。
3.  **对应地**，看看课后习题（带答案那种）。
4.  再看一遍往年卷。
5.  开始做Lab。

## 具体计划

29-看看实验，抱抱佛脚

30-玩玩吃吃浪浪浪。不行，实验有多少写多少吧。

# 往年卷

1.  第二章-IPC的方式？Shell如何解释命令？
2.  第二章处理器调度-批处理系统作业调度
    1.  平均带权周转时间，权是除预计时间得到的
3.  第三章并发程序-银行家算法-分配拒绝法-死锁检测算法
    1.  死锁涉及了哪些进程？？？
4.  第四章-段页存储管理
    1.  二级页表？？？
    2.  NRU，LFU，Aging？？？
    3.  内存中工作集总尺寸？？？
    4.  最佳页面尺寸？？？
5.  **第六章-文件系统**
    1.  open?
    2.  ln?
    3.  目录项??
6.  第五章-磁盘管理
    1.  HDD还真的能考啊
7.  第二章-管程/信号量

# Preview

## 处理器调度-批处理系统作业调度

1.  平均带权周转时间，权是除预计时间得到的。
2.  需要记住一批算法的简称，书上都划过了。

## 死锁问题

### 死锁防止

通过破坏条件，死锁根本不会发生。

### 死锁避免-银行家算法

通过拒绝分配资源，避免死锁的发生。

1.  判断系统状态安全，给出安全序列即可
2.  判断能否分配给某程序资源，判断能否找到安全序列即可

### 死锁检测算法

通过检测到系统中的死锁，再处理涉及的进程搞定它们。

用**资源分配图**画出来，再标注当前还有哪些资源可用。（注意和**资源轨迹图**的区别。）

*Tips:*将分配箭头和需求箭头使用不同的颜色画出。

看看先找谁讨债比较合适，最后的坏账人员就是死锁**涉及**的进程了。

>   ## 死锁定理
>
>   可以通过将资源分配图简化的方法来检测系统状态S是否为死锁状态。简化方法如下：
>   1) 在资源分配图中，找出既不阻塞又不是孤点的进程Pi（即找出一条有向边与它相连，且该有向边对应资源的申请数量小于等于系统中已有空闲资源数量。若所有的连接该进程的边均满足上述条件，则这个进程能继续运行直至完成，然后释放它所占有的所有资源）。消去它所有的请求边和分配边，使之成为孤立的结点。在图2-18(a)中，P1是满足这一条件的进程结点，将P1的所有边消去，便得到图248(b)所示的情况。
>
>   S为死锁的条件是当且仅当S状态的资源分配图是不可完全简化的,该条件为死锁定理。

## 段页存储管理

~~连续存储空间管理的分配算法？跳过吧~~

### 分页式地址转换计算

Page Number+Offset, Page Table translates page number.

-   多级页表
-   反置页表
-   页面替换策略

#### 最佳页面尺寸估计

>    最佳页面尺寸应使函数 f(p) = se/p + p/2 取到最小值。进程平均占用空间 s = 8*2^20 B，页表项大小 e = 4 B，f(p) = 2^25/p + p/2,求导 f’(p)=1/2 – 2^25/p^2 = 0，得 p = 2^13 B。







1.  二级页表？？？
2.  NRU，LFU，Aging？？？
3.  内存中工作集总尺寸？？？
4.  最佳页面尺寸？？？

## 文件系统

NJU和OSTEP的不同：

1.  *文件系统根目录内容预先加载至内存中*->root data全部加载，不需要再读root inode了。

2.  *在不考虑磁盘缓冲的情况下，上述代码中父、子进程读文件时，文件系统各读取了几个物理块？ 其中有几个物理块父、子进程都读取了？*->根本不用读inode，也不用多读多级表头？？

    **二级链表的表头指针其实也在inode里，所以二级文件索引其实并不需要多读一份表头指针？**





## 磁盘管理



## 管程/信号量

# Rubbish from the courses



## Process & Schedule

 **Q**

-   原语primitive=>原子操作atomic action
    -   是由若干个机器指令构成的完成某种特定功能的一段程序，具有不可分割性·即原语的执行必须是连续的，在执行过程中不允许被中断。
-   程序性中断=>异常？
-   Real & Protect mode



Linux下的三种Schedule机制

1.  Tasklet
2.  Softirq
3.  Workqueue

### Thread

[三种组织形式](http://maxim.int.ru/bookshelf/PthreadsProgram/htm/r_19.html)

## Concurrency & Sync

-   周转时间和响应时间

    -   >   响应时间：从提交第一个请求到产生第一个响应所用时间。
        >   周转时间：从作业提交到作业完成的时间间隔。
        >   平均周转时间：衡量不同调度算法对相同作业流的调度性能。
        >   带权周转时间：反映长短作业的差别。
        >   平均带权周转时间：比较某种算法对不同作业流调度性能。
        >   举例说明：
        >   比如你让我回答:100加100加100加100减100等于多少? 我用2秒回答了你等于300 那么我要计算你这个问题是要时间的我花了1.8秒来运算就是周转时间. 总共用了2秒准确地回答了你的问题就是响应时间. 计算过程是周转时间.接到命令到计算出答案就是响应时间.


**上课要注意的点**

-   简单地描述各类调度算法-OK
-   能人肉模拟调度过程-OK

### 并发进程概述



### 临界区管理

-   软件 Peterson算法 要进和已经进（虽然好像也没有写得很及时？）
-   硬件
    -   关中断
    -   指令
        -   Test & Set
        -   Swap
-   *Q：具体操作？*

### Sync机制

PV操作和信号量

*Q：看OS162吧。*

### IPC（进程间通信）

-   信号通信机制
-   管道
-   共享内存

### 死锁

-   Prevention-4 Prop
-   Aviodence-Banker
-   Detect & Recovery

### 同步

#### 信号量与PV操作

#### 管程



## Storage

### 页面替换算法

课本P235有简要小结，Dropbox里的pdf文件有详细介绍。

LRU没有Belady现象：

>   LRU一般都有栈的特性，一个N+1大小的cache很自然的就包含了大小为N的cache的内容。所以随着cache大小增加，hit rate要么不变，要么提高。

## Device

TBD：

-   单|双|多缓冲

## Files

# 名词解释

### 分时系统

>   要弄清批处理系统和分时系统的区别，首先我们得了解何为批处理系统和分时系统？ 
>   一、批处理系统 
>   从字面上理解，就是一批一批的处理任务的一种系统，严格的定义，就是指用户将一批作业提交给操作系统后就不再干预，由操作系统控制它们自动运行。这种采用批量处理作业技术的操作系统称为批处理操作系统。简单地理解就是我手中有一大堆作业（相当一个程序）要运行，我一个一个的放入内存中执行效率会很慢，因为我要人为的去装载程序（早期的机器会把程序写到磁带中，然后人为地放到专门处理程序的机器中），**所以我一次性放一批的作业，让操作系统自己去运行它，而我不需要干涉，这样我就省了很多力气。**
>   ![img](OperatingSystem_NJU.assets/20170329153105707.png)
>
>   
>
>   二、分时系统 
>   分时操作系统：“分时”的含义是指多个用户使用同一台计算机，多个程序分时（分时间片）共享硬件和软件资源。分时操作系统是指在一台主机上连接多个带有显示器和键盘的终端，同时允许多个用户通过主机的终端，以交互方式使用计算机，共享主机中的资源。**分时操作系统将CPU的时间划分成若干个片段，称为时间片，操作系统以时间片为单位，轮流为每个终端用户服务。**
>
>   ![img](OperatingSystem_NJU.assets/20170329152411531.png)
>
>   从他们的定义我们大概可以总结出： 
>   批处理系统没有人机交互，而分时系统允许多个用户同时使用 
>   批处理系统中允许程序长时间地占用CPU，而分时系统不允许 
>
>   问题：多道程序按不按时间片来分配时间 
>   不按，时间片时在分时系统中提出的概念，多道程序没有时间片的概念



### 可重入代码

>   可重入代码(Reentry code)也叫纯代码(Pure code)是一种**允许多个进程同时访问的代码。**为了使各进程所执行的代码完全相同，故不允许任何进程对其进行修改。**程序在运行过程中可以被打断，并由开始处再次执行，并且在合理的范围内（多次重入，而不造成堆栈溢出等其他问题），程序可以在被打断处继续执行，且执行结果不受影响。**



### 可重入函数

>   可重入函数主要用于多任务环境中，一个可重入的函数简单来说就是**可以被中断的函数**，也就是说，**可以在这个函数执行的任何时刻中断它，转入OS调度下去执行另外一段代码，而返回控制时不会出现什么错误**；而不可重入的函数由于使用了一些系统资源，比如全局变量区，中断向量表等，所以它如果被中断的话，可能会出现问题，这类函数是不能运行在多任务环境下的。



# 作业

操作系统概论（4周）

- 课后作业（一、13，17，34，二、5，11）

处理器管理（3周）

- 课后作业（一、9，13，35，43；二、12，21，28

> 1.需求分析
>
> 某多道程序系统采用可变分区存储管理，供用户使用的内存空间为200KB，磁带机5台。采用静态方式分配外部设备，且不能移动内存中的作业，进程调度采用FCFS算法，忽略用户作业I/O操作时间。现有作业序列如下：
>
> 作业号进入时间运行时间(min)内存需求(KB)磁带机(台)
>
> A 8:30 40 30 3
>
> B 8:50 25 120 1
>
> C 9:00 35 100 2
>
> D 9:05 20 20 3
>
> E 9:10 10 60 1
>
> 求：（1）FCFS算法选中作业装入内存时间、开始执行时间、执行结束时间、执行的次序、作业平均周转时间、内存分配情况；
>
> （2）SJF算法选中作业装入内存时间、开始执行时间、执行结束时间、执行的次序、作业平均周转时间、内存分配情况；
>
> ２．详细说明： 
> 1 ．先来先服务算法。说明： 
> ( 1 ) 8 : 30 作业A 到达并投入运行。注意它所占用的资源。 
> ( 2 ) 8 : 50 作业B 到达，资源满足进主存就绪队列等CPu 。 
> ( 3 ) 9 : 00 作业C 到达，主存和磁带机均不够，进后备作业队列等待。 
> ( 4 ) 9 : 05 作业D 到达，磁带机不够，进后备作业队列等待。后备作业队列有C 、D 。 
> ( 5 ) 9 : 10 作业A 运行结束，归还资源磁带，但注意主存不能移动（即不能紧缩）。作业B 投入运行。作业C 仍因主存不够而等在后备队列。这时作业E 也到达了，。也由于主存不够进入后备作业队列。此时作业D 因资源满足（主存磁带均满足），进主存就绪队列等待。后备作业队列还有C 、E 。 
> ( 6 ) 9 : 35 作业B 运行结束，作业D 投入运行。这时作业C 因资源满足而调入主存进就绪队列等CPU 。而作业E 因磁带机不够继续在后备作业队列等待。 
> ( 7 ) 9 : 55 作业D 运行结束，作业C 投入运行。这时作业E 因资源满足而调入主存进就绪队列等CPU 。 
> ( 8 ) 10 : 30 作业C 运行结束，、作业E 投入运行。 
> ( 9 ) 10 : 40 作业E 运行结束。 
>
> 2 ．短作业优先算法。说明： 
> ( 1 ) 8 : 30 作业A 到达并投入运行。注意它所占用的资源。  
> ( 2 ) 8 : 50 作业B 到达，资源满足进主存就绪队列等CPU 。  
> ( 3 ) 9 : 00 作业C 到达，主存和磁带机均不够，进后备作业队列等待。  
> ( 4 ) 9 : 05 作业D 到达，磁带机不够，进后备作业队列等待。后备作业队列有C 、D .  
> ( 5 ) 9 : 10 作业A 运行结束，归还资源磁带，但注意主存不能移动（即不能紧缩）。作业B 投入运行。作业C 仍因主存不够而等在后备队列。这时作业E 也到达了，虽然该作业最短，也由于主存不够进入后备作业队列．此时作业D 因资源满足（主存磁带均满脚，进主存就绪队列等待。后备作业队列还有C 、E 。  
> ( 6 ) 9 : 35 作业B 运行结束，作业D 投入运行。这时作业C 和E 资源均满足，但按SJF 应把作业E 调入主存进就绪队列等CPU 。而作业C 因磁带机不够继续在后备作业队列等待。  
> ( 7 ) 9 : 55 作业D 运行结束，作业C 调入主存进就绪队列等CPU . 
> ( 8 ) 10 : 05 作业E 运行结束，作业C 投入运行．  
>
> ( 9 ) 10 : 40 作业C 运行结束。 

文件系统（2周）

- 课后作业：（一、11，32，36；二、10，14，19，23）

存储管理（2周）

- 课后作业：（一、17，20，28；二、1，12，17，24，47）