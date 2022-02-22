# CSAPP-深入理解计算机系统

作者：九曲阑干

 [TOC]

 

## 1.计算机系统漫游

[视频链接](https://www.bilibili.com/video/BV1cD4y1D7uR?from=search&seid=7136804747008949576&spm_id_from=333.337.0.0)

### 1.1编译系统

![image-20220222145703391](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222145703391.png)

预处理阶段：根据#开头代码，修改原始程序，得到.i结尾

编译阶段：词法分析、语法分析、语义分析、中间代码生成以及优化等

汇编阶段：将汇编程序翻译成机器指令，按照固定规则打包，得到可重定位文件

链接阶段：把提前编译好的printf.o跟hello.o以一定规则合并，得到可执行文件

### 1.2硬件系统结构

![image-20220222150716755](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222150716755.png)

PC：指向下条需要执行的指令

寄存器：临时存放的空间

ALU：进行算术计算

主存：存放指令和数据

总线：内存和处理器进行数据传递

输入输出设备：控制器与适配器相连

### 1.3程序执行过程

![image-20220222151211724](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222151211724.png)

输入hello->到达寄存器->执行指令->hello字符串存入内存

![image-20220222151232051](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222151232051.png)

执行一系列指令加载可执行文件->将数据和代码从磁盘复制到内存(DMA，不经过处理器)

![image-20220222151246851](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222151246851.png)

处理器执行代码->将hello world字符串复制到寄存器->复制到显示设备

### 1.4内存结构

![image-20220222151145631](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222151145631.png)

### 1.5操作系统

![image-20220222151320754](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222151320754.png)

1. 防止硬件被失控的应用程序滥用
2. 同一机制控制复杂底层硬件

### 1.6抽象

![image-20220222153356098](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222153356098.png)

### 1.7进程上下文切换

![image-20220222151518918](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222151518918.png)

### 1.8虚拟内存

![image-20220222152051847](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152051847.png)

自下(地址0)而上，

程序代码和数据：从可执行目标文件加载(从磁盘复制)，代码从固定地址开始，全局变量放在这里

堆：malloc申请的内存空间，运行时动态扩展和收缩

共享库区域：存放标准库，如printf

用户栈：函数调用，高地址到低地址

内核保留区域：对用户不可见

### 1.9文件

一切皆文件

所有IO设备都可以看做文件

所有输入输出都是通过读写文件完成

![image-20220222152217574](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152217574.png)

### 1.10网络

![image-20220222152432048](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152432048.png)

客户端发送字符串给服务器端，服务器端shell执行，将输出结果返回给客户端

### 1.11 Amdahl's Law

![image-20220222152637015](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152637015.png)

![image-20220222152733887](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152733887.png)

![image-20220222152755916](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152755916.png)

总结：优化大部分组件才能得到较大的速度提升

### 1.12更高计算能力

![image-20220222152843479](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152843479.png)

![image-20220222152954399](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222152954399.png)

增加CPU核心数，提高系统性能

![image-20220222153046334](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222153046334.png)

当一个线程因为读取数据进入等待，CPU可以去执行另一个线程

![image-20220222153201016](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222153201016.png)

指令集并行，每个周期可以执行2~4个指令

![image-20220222153327420](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222153327420.png)

单指令多数据：SIMD，提高处理视频、声音等数据执行速度点

## 3.机器级表示

### 3.1程序的机器级表示

#### shell汇编指令

![image-20220222154224876](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222154224876.png)

gcc：编译器

-Og：生成符合源程序的代码

-O1 -O2：高级别优化，但会使原代码变形

-o prog：可执行文件文件名

![image-20220222154416980](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222154416980.png)

-S：产生文件为汇编文件

![image-20220222154954357](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222154954357.png)

-c：生成机器代码，二进制文件

![image-20220222155029389](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222155029389.png)

objdump反汇编，查看相关信息

![image-20220222155047986](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222155047986.png)

#### 寄存器

![image-20220222154711035](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222154711035.png)

函数A为调用者，B为被调用者

调用者保存与被调用者保存

![image-20220222154803436](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222154803436.png)

### 3.2寄存器

#### 地址引用

![image-20220222155314573](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222155314573.png)

比例因子的值跟数据类型相关

![image-20220222155421666](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222155421666.png)

内存复制到内存需要两条指令。

![image-20220222155643487](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222155643487.png)

任何生成32位的指令会把寄存器高位置0

### 3.3栈

![image-20220222160449646](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222160449646.png)

压栈：先对栈操作，腾出空间，然后把数据移入栈中

弹栈：弹出数据存储，恢复栈

### 3.4条件码

![image-20220222161007384](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222161007384.png)

![image-20220222161022650](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222161022650.png)

![image-20220222161048670](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222161048670.png)

cmp和test指令都是设置条件码不改变寄存器内容

![image-20220222161626575](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222161626575.png)

cmp：比较a、b，相等设置零标志位为1

sete：根据零标志位赋值

![image-20220222161856080](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222161856080.png)

通过符号标志设置setl，得到a<b的最终结果

### 3.5跳转指令

![image-20220222162157928](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222162157928.png)

根据流水线机制，跳转指令，分支预测会猜测每条指令是否执行，错误预测浪费大量时间。

### 3.6过程

栈帧

参数大于6，存在栈帧中

![image-20220222162536687](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222162536687.png)

call指令压p函数地址

![image-20220222163019683](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222163019683.png)

局部变量不需要对齐，

超过6的传递参数存栈中需要8字节对齐，

### 3.7 结构体和联合体

#### 对齐

![image-20220222164019088](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222164019088.png)

由于j是int类型，起始地址必须是4的倍数，所以通过将c对齐，得到起始地址为8

![image-20220222164136778](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222164136778.png)

修改结构，由于下个索引的开头数据类型是int，所以还是需要4字节对齐

#### 联合体

联合体所有字段共享同一存储区域，最大字段大小决定

![image-20220222164355668](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222164355668.png)

![image-20220222164527732](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222164527732.png)

### 3.8缓冲区溢出

![image-20220222164854065](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222164854065.png)

栈随机化：程序每次运行地址都发生变化

![image-20220222165009229](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222165009229.png)

![image-20220222164936260](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222164936260.png)

标记可读可写不可执行。

## 4.处理器体系结构

### 4.1指令系统结构

指令设计

![image-20220222165552592](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222165552592.png)

异常处理

![image-20220222165717742](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222165717742.png)

### 4.2寄存器文件

![image-20220222170304559](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222170304559.png)

![image-20220222170350978](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222170350978.png)

#### verilog程序

![image-20220222170431049](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222170431049.png)

### 内部结构

能不能写，往哪写，写什么

data输入信号线：每个寄存器相连

![image-20220222173017482](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173017482.png)

we信号线： 能不能执行写入

地址信号线：读操作写操作公用，经过地址解析与we信号共同确定对哪个寄存器执行写

![image-20220222173038140](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173038140.png)

加入时钟和重置信号

![image-20220222173055311](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173055311.png)

#### CMOS

![image-20220222173210427](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173210427.png)

![image-20220222173243894](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173243894.png)

#### 多路选择器

select=0  输出a   select=1 输出b

![image-20220222173413764](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173413764.png)

实现某个特定寄存器内容传输到ALU输入端

#### D触发器

![image-20220222173544123](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173544123.png)

![image-20220222173633397](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173633397.png)

![image-20220222173700171](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173700171.png)

#### 组合逻辑vs时序逻辑

前者输出值仅由当前输入状态决定

后者输出值不仅与当前输入状态有关，与原来的状态也有关

#### Verilog

![image-20220222173907839](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222173907839.png)

## 4.3 Y86-64顺序实现

#### 阶段

![image-20220222174124935](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174124935.png)

#### 译码阶段

![image-20220222174244364](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174244364.png)

#### 执行阶段

![image-20220222174312501](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174312501.png)

#### 访存阶段

![image-20220222174356817](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174356817.png)

#### 写回阶段

![image-20220222174430553](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174430553.png)

#### 案例

![image-20220222174558277](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174558277.png)

![image-20220222174650173](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174650173.png)

![image-20220222174722610](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174722610.png)

![image-20220222174800881](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174800881.png)

![image-20220222174838987](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222174838987.png)

## 4.4 Y86-64处理器硬件细节

#### 取指阶段

![image-20220222175208245](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222175208245.png)

![image-20220222175305257](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222175305257.png)

#### 译码阶段

icode：例如push指令只有目的寄存器ID值

![image-20220222175556469](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222175556469.png)

#### 执行阶段

ifun：确定运算方式

cc：算术逻辑指令设置条件码，内存引用地址及对栈操作，不会设置条件码 

Set_CC：根据icode确定是否要更新条件码

Cnd：ifun跟CC确定是否发生跳转

![image-20220222190642162](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222190642162.png)

#### 访存阶段

![image-20220222190748126](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222190748126.png)

#### 写回阶段

cnd信号不满足条件，目的寄存器设置为0xF，来禁止写入

![image-20220222190817796](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222190817796.png)

#### PC更新阶段

![image-20220222190931093](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222190931093.png)

### 4.5流水线通用原理

![image-20220222191151501](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222191151501.png)

输入信号由低电平变成高电平，输入信号y才加载到寄存器

### 4.6流水线硬件结构

![image-20220222191756988](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222191756988.png)

通过改造，可以将更新PC放在开头。电路重定时。

![image-20220222192009601](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222192009601.png)

##### 寄存器F：保存PC预测值

![image-20220222192333250](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222192333250.png)

##### 寄存器D：保存刚刚取出指令的信息

如指令代码、指令功能、寄存器指示符等等

![image-20220222192448950](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222192448950.png)

##### 寄存器E：保存最新译码指令状态和寄存器文件读出的数值

![image-20220222192621611](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222192621611.png)

##### 寄存器F：保存最新执行指令结果

不仅算术逻辑指令结果，还有跳转指令的分支条件信息

##### 寄存器W

访存执行结果存到寄存器W

反馈路径将结果写回寄存器文件

ret，则访存读出数值就是下一条即将执行的指令地址，提供给PC选择逻辑

![image-20220222192747968](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222192747968.png)

### 4.7数据冒险

**暂停技术**

![image-20220222193028276](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222193028276.png)

**数据转发**

![image-20220222193220692](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222193220692.png)

添加旁路路径，添加了两个逻辑块

内存读取数据情况

**暂停+转发**

![image-20220222193428151](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222193428151.png)

### 4.8 控制冒险

ret引发控制冒险用三个气泡解决

![image-20220222195117465](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222195117465.png)

跳转情况总是选择执行跳转

错误预测，后面两步分别添加气泡

![image-20220222195225471](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222195225471.png)

暂停信号，遇到寄存器输出结果也不改变

![image-20220222195339371](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222195339371.png)

气泡信号，发生复位

![image-20220222195413520](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222195413520.png)

### 4.9 Y86-64流水实现

#### 取指阶段

![image-20220222195630962](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222195630962.png)

![image-20220222195842109](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222195842109.png)

#### 译码阶段

![image-20220222200106546](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222200106546.png)

1. ALU计算后
2. 访存前
3. 访存后
4. 写回前
5. 写回后

白色：寄存器ID

红色：转发数据

优先级：执行>访存>写回

![image-20220222200401013](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222200401013.png)

跳转时，valP可以跟valA合并

### 4.10流水线控制逻辑

数据冒险

![image-20220222200521016](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222200521016.png)

分支错误

![image-20220222200609424](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222200609424.png)

返回指令

![image-20220222200642508](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222200642508.png)

#### 组合情况

![image-20220222200802770](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222200802770.png)

![image-20220222200855039](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222200855039.png)

#### CPI

![image-20220222201001335](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222201001335.png)

## 5.优化程序性能

### 5.1优化程序性能

1. 无法确定指针是否指向同个位置，则假设所有情况可能发生

2. 函数调用返回值不同。

**代码移动**

![image-20220222202313140](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222202313140.png)

分析汇编代码，执行两次读内存一次写内存操作

![image-20220222202510545](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222202510545.png)

**引入临时变量**

![image-20220222202532876](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222202532876.png)

发生显著提高

![image-20220222202624319](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222202624319.png)

### 5.3理解现代处理器

![image-20220222202951556](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222202951556.png)

加法指令包含 读操作、写操作、加法操作

![image-20220222203343160](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222203343160.png)

每个时钟周期可以执行多个操作，并且是乱序执行的

分支：判断预测结果是否正确

**i7包含8个功能单元**

![image-20220222203241796](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222203241796.png)

4个单元可以执行整数计算

### 5.4数据流图

![image-20220222203604689](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222203604689.png)

2个加载单元限制处理器最多能读取2个数据值，吞吐量界限0.5

![image-20220222203813887](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222203813887.png)

循环寄存器：一次迭代产生的值在另一次迭代中用到

#### 数据流图

![image-20220222203919590](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222203919590.png)

浮点数乘法5个时钟周期，加法1个时钟周期，左边的链乘法成为关键路径

提供程序执行时间的下界

### 5.5 循环展开

![image-20220222204207046](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204207046.png)

减少循环开销

![image-20220222204229507](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204229507.png)

**两路并行**

2X2循环展开

![image-20220222204344408](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204344408.png)

打破界限

![image-20220222204552256](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204552256.png)

关键路径只包含n/2

![image-20220222204450132](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204450132.png)

**重新结合变换**

![image-20220222204620571](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204620571.png)

![image-20220222204700575](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204700575.png)

不用等待前一次迭代的累加值

![image-20220222204736370](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222204736370.png)

### 5.6 理解内存性能

16个浮点寄存器，超过则分配到栈上，则20X20比10X10展开慢

加载操作延迟(内存->寄存器)

![image-20220222205041972](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222205041972.png)

存储操作

![image-20220222205122764](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222205122764.png)

发生了写读相关，变慢

## 7.链接

将各种代码和数据收集组成一个文件的过程，文件加载到内存执行

### 7.1编译器驱动程序

#### 预处理阶段

![image-20220222205455242](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222205455242.png)

#### 编译阶段

![image-20220222205516829](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222205516829.png)

#### 汇编阶段

![image-20220222205549288](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222205549288.png)

#### 链接阶段

构造可执行文件

![image-20220222205626798](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222205626798.png)

#### 加载阶段

./prog

加载器将可执行文件prog代码和数据复制到内存

将CPU控制权转移动prog程序开头

### 7.2可重定位目标文件

![image-20220222210634734](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222210634734.png)

![image-20220222210730193](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222210730193.png)

![image-20220222210822028](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222210822028.png)

![image-20220222210935438](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222210935438.png)

#### sections

![image-20220222211024083](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222211024083.png)

![image-20220222211511453](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222211511453.png)

.text：已编译好的机器代码

.data：初始化全局变量，静态变量值

.bss：未初始化全局变量和静态变量(占位符，不占用实际空间)

.rodata：read only(printf格式串，switch跳转表存放位置)

![image-20220222211546392](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222211546392.png)

#### .symtab

![image-20220222211659429](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222211659429.png)

![image-20220222211718574](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222211718574.png)

Ndx：section索引值，看section header table确定

value：相对.text section起始位置的偏移量

size：所占字节数

OBJECT：数据对象(变量和数组)

COMMOM：未初始化全局变量

.bss：未初始化静态变量及初始化为0的全局或静态变量

x变量是局部变量，在运行时栈中管理，符号表不关心

![image-20220222212258652](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222212258652.png)

static：私有的，不能被其他模块使用

### 7.4符号解析与静态库

![image-20220222212743870](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222212743870.png)

1. 不允许多个同名强符号出现
2. 一强一弱选强
3. 都弱：警告后续导致错误

![image-20220222212927574](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222212927574.png)

#### 静态库

![image-20220222213030551](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222213030551.png)

![image-20220222213216367](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222213216367.png)

### 7.5静态库解析过程

集合E：链接器扫描过程中发现可重定位目标文件存放，最终合并为可执行文件

集合U：引用了尚未定义的符号

集合D：输入文件中已定义的符号

![image-20220222213551638](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222213551638.png)

![image-20220222213640890](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222213640890.png)

U为空，则合并集合E和D

U不为空，存在未定义符号，则错误并终止

**输入顺序很重要**

![image-20220222213751494](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222213751494.png)

先调用了libvector，被丢弃，再调用main，最后无法解析addvec

![image-20220222213906316](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222213906316.png)

### 7.6重定位

![image-20220222214106966](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222214106966.png)

![image-20220222214655952](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222214655952.png)

重定位条目

.rel.text：代码重定位条目

.rel.data：已初始化数据重定位条目

![image-20220222214915609](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222214915609.png)

PC相对地址

![image-20220222215006933](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215006933.png)

![image-20220222215114577](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215114577.png)

绝对地址

![image-20220222215147075](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215147075.png)

![image-20220222215203493](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215203493.png)

![image-20220222215217106](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215217106.png)

#### 7.7可执行文件

.init包含_init函数，调用函数进行初始化

![image-20220222215326069](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215326069.png)

![image-20220222215342404](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215342404.png)

![image-20220222215411887](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215411887.png)

off：偏移量

vaddr、paddr：开始地址

filesz：大小

memsz：内存占用大小

代码段memsz比filesz大8字节：存放.bss section数据

![image-20220222215630565](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215630565.png)

![image-20220222215720769](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222215720769.png)

![image-20220222220058574](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220222220058574.png)

---

**耗时**：10个番茄钟=4h10min

**时间**：2022/02/22