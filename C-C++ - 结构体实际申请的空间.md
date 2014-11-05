## C/C++ - 结构体实际申请的空间

1. 如下的结构体，`sizeof()`大小,实际申请的空间以及理论上申请最佳空间
```
struct Spot
{
    int x;
    int y;
    bool visible;
    int red;
    int blue;
    int green;
    double alpha;
    bool cleaned;
};
```

> 在分析前，要先了解下<font color='#FF0000'>Data structure alignment</font>概念

> * 简单来说，就是因为CPU访问内存时是成块成块读取数据的，所以编译器为了让CPU访问的时候更加方便些（同时也使得程序更加高效些），会将变量的内存地址移动到2的N次幂上。而为此空出来的空间叫做padding，在计算结构体总大小的时候，也得考虑这些padding。
<br/>
> * 简单说，假设CPU每次读取内存都是读4个字节，那么要把变量内存地址移到4的倍数上。不过在64位系统中，CPU每次可以读取8个字节，所以8个字节的double变量地址要位于8的倍数上。一个个变量算下来，最后就会得到结构体的实际大小了。


## 1. 计算理论上的最佳值：
 > <font color = '#FF00FF' >
 1. int --> 4 Byte
 2. bool --> 1 Byte
 3. double --> 8 Byte
 </font>
 
 所以理想最佳值为：４＋４＋１＋４＋４＋４＋８＋１ ==>　３０
 
## 2.sizeof() 程序输出结果（在64位机器ubuntu上测试）输出结果
  * 测试机器：ubuntu x64
  * 编译器：gcc4.8.2
　 最终结果是：40
 
## 3.根据Data structure alignment在以下平台分析

* 测试机器：ubuntu x64
* 编译器：gcc4.8.2

因为在６４位机器上运行，所以CPU每次可以读取8个字节，也就意味着每８个字节位一组数据。

int x和int y作为１组。
 bool visible ---> 1 Byte
 int red      ---> 4 Byte
 int blue     ---> 4 Byte
 因为visible＋red ---> 5 Byte,没到8 Byte　所以后面可以在追加字段，但是visible + red + blue --> 9 Byte　超出８Byte　所以这里分成两组，visible + red 一组，blue为另外一组

依次类推：最终结果和sizeof()结果一致

## 后记：对于Spot结构的优化

```
struct Spot
{
　　double alpha;
    int x;
    int y;
    int red;
    int blue;
    int green;
    bool cleaned;
    bool visible;
};
```

* 参考http://segmentfault.com/blog/spacewander/1190000000753849
Tags: C++