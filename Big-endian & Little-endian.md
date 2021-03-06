

#### 什么是大小端模式：

    大端模式：是指数据的高字节保存在内存的低地址中，而数据的低字节保存在内存的高地址中，这样的存储模式有点儿类似于把数据当作字
             符串顺序处理：地址由小向大增加，而数据从高位往低位放；
    
    小端模式：是指数据的高字节保存在内存的高地址中，而数据的低字节保存在内存的低地址中，这种存储模式将地址的高低和数据位权有效
             地结合起来，高地址部分权值高，低地址部分权值低，和我们的逻辑方法一致。
   
    简而言之：大端模式就是低位高地址，高位低地址；小端模式就是低位低地址，高位高地址；
    
    例如：int num = 1; num占一个整形空间的大小，四个字节。如果你的机器是小端存储，那么num在内存中应该是这样存储的：01 00 00 00
         如果你的机器是大端存储，那么num在内存中应该是这样存储的：00 00 00 01 。 


<br>
### 通常有两种常见的方法来检测机器的存储模式：


```cpp
//方法一：利用指针；
int sys_check()
{
    //如果你的电脑是小端存储，则内存中为01 00 00 00；大端则为：00 00 00 01；
    int num = 1;            
 
    //取内存中的第一个字节，小端返回1，大端返回0；
    if (1 == *(char *)&num)
    {
        return 1;   
    }
    else
    {
        return 0;
    }
}
 
 ```
 
 
 ```cpp
//方法二：利用联合体；
int sys_check()
{
    //该共用体占四个字节，c访问第一个字节，num访问所有字节，
    //若为小端，则第一个字节为1，否则为0；
    union CHECK
    {
        int num;
        char c;
    }_check;
 
    _check.num = 1;
         
    //取内存中的第一个字节，小端返回1，大端返回0；
    if (1 == _check.c)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}


```

<br>
#### 为什么会有大小端模式之分呢？

         这是因为在计算机系统中，我们是以字节为单位的，每个地址单元都对应着一个字节，一个字节为 8bit。 但是在C语言中除了8bit
     
     的char之外，还有16bit的short型，32bit的long型（要看具体的编译器），另外，对于位数大于 8位的处理器，例如16位或者32位的处
     
     理器，由于寄存器宽度大于一个字节，那么必然存在着一个如何将多个字节安排的问题。因此就导致了大端存储模式和小端存储模式。例
     
     如一个16bit的short型x，在内存中的地址为0x0010，x的值为0x1122，那么0x11为高字节，0x22为低字节。对于大端模式，就将0x11放在
     
     低地址中，即0x0010中，0x22放在高地址中，即0x0011中。小端模式，刚好相反。我们常用的X86结构是小端模式，而KEIL C51则为大端
    
     模式。很多的ARM，DSP都为小端模式。有些ARM处理器还可以由硬件来选择是大端模式还是小端模式。
     
     
     名字由来：在乔纳森·斯威夫特的著名讽刺小说《格列夫游记》中，小人国内部分裂成Big-endian和Little-endian两派，区别在于一派要
     
     求从鸡蛋的大头把鸡蛋打破，另一派要求从鸡蛋的小头把鸡蛋打破。斯威夫特借以讽刺英国的政党之争，在计算机工业中指数据储存顺序
     
     的分歧。


----------------------------------------------------------------------------------------------------------------------------------


