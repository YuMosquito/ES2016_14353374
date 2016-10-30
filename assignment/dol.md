#DOL 实例分析 &编程

---
## 任务一：修改 example2
让 3个square模块变成 2个, tips: 修改 xml的iterator

**1.修改后的 *.dot截图以及编译结果**：
![.dot截图](http://upload-images.jianshu.io/upload_images/3239746-1b1266406618bd9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![编译结果](http://upload-images.jianshu.io/upload_images/3239746-0f2d9c7e593ee1dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>**2.具体修改过程**：
这里使用迭代的方法，定义了value个square模块、value+1条通道，以及每条通道需要的 2个 connection。所以这里只需要定义value值等于2，就可以把 3个square模块变成 2个。
![](http://upload-images.jianshu.io/upload_images/3239746-7624d65cacebd495.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 任务二：修改 example1 
使其输出 3次方数，tips: 修改square.c

**1.修改后的 *.dot截图以及编译结果**：
![.dot截图](http://upload-images.jianshu.io/upload_images/3239746-8de210257013ddf1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![编译结果](http://upload-images.jianshu.io/upload_images/3239746-6367fe56c7abc3a5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>**2.具体修改过程**：
* 在square.c文件中定义了平方计算进程，修改为立方计算进程即可：
<p> ![](http://upload-images.jianshu.io/upload_images/3239746-a1cee55339dd6fd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>* 将模块名称由square改成cube，需要将square.c、square.h、example1.xml中的相关函数名称和进程名称改成cube：
<p>![square.c](http://upload-images.jianshu.io/upload_images/3239746-4da2fe53c581f3d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>![square.h](http://upload-images.jianshu.io/upload_images/3239746-11cb4d33246dc998.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>![example1.xml](http://upload-images.jianshu.io/upload_images/3239746-a60f6cbf6155abdf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#实验感想及心得
*  **实验中遇到的问题：**
  * 修改代码之后要重新编译、运行，一直报错。
解决方法：编译时进错路径，在dol/examples/example1路径下运行，应该在dol/build/bin/main下运行。
  * 任务二修改模块名称的时候出错，当时只是修改example1.xml中的进程名称，报错内容大致为square_init和square_fire这两个函数（忘记截图了）。
解决方法：文档中提到*.c, 与对应的 .h是实现的模块，是*.dot 的模块功能描述。每个模块要实现 2个接口，xxx_init和xxx_fire 分别是初始化这个模块，所以需要把square.c和square.h中的相关函数名称也改成cube。改为之后编译成功，.dot中的模块名称成功修改。
*  **心得：**
  *  本次实验主要是学习DOL 实例分析和编程，首先有个整体的框架：      
    +  /src 文件夹内包含 2种文件： *.c与对应的 .h是实现的模块，是*.dot 的 框的功能描述。每个模块要实现 2个接口，由 xxx_init 和xxx_fire 这两个函数来初始化
    + ./example*.xml：该文件定义了模块连接方式。
        1.  process 定义模块框 :
 ```
 <process name=“ 未知数 1">
     　　<port type=“ 未知数 2” name=“ 未知数 3”/>
      　　<port type=“ 未知数 2” name=“ 未知数 3”/> //这里说有2个端口
    　　<source type=“c” location=“ 未知数 1.c"/> 
</process> 
```
　　• 未知数1:实现的模块名字；未知数2:output(表示输出端口)或者 input(表示输入端口)；未知数3:端口的名字，在对应的.h 文件里面定义。
       <p>　　　　b. sw_channel定义连接模块的通道：
```
<sw_channel type=“ fifo” size=“ 未知数 1” name=“ 未知数 2">
　　<port type=“input” name=“in"/> //输入端口
　　<port type=“output” name=“out"/> //输出端口
</ sw_channel >
```
　　　　　• 未知数1指缓冲区的大小；未知数2是这条通道的名字。
      <p>　　　　c. connection定义各个模块之间的连接 ：每条通道有 2个connection连接左右模块框
```
<connection name=“ 未知数 1">
　　<origin name=“ 未知数 2”>//通道左边模块
　　　　<port name=“ 未知数 3"/> 
　　</origin>
 　　<target name=“ 未知数 4”>//通道右边模块
　　　　<port name=“ 未知数 5"/> 
　　</target> 
</connection> 
```
　　　　　• 未知数1是连接线名称;未知数2\未知数4是模块或者通道的名字;未知数3\未知数5对应 process或者channel的端口名。
  *  实验中学习到一些linux语句的使用，因为dol文件加了锁，所以不能直接删掉之前build的example文件，使用```rm -rf 文件名```指令在终端删除文件夹；而且不能直接修改文件，所以使用```sudo gedit 文件名```指令在终端打开文件，然后修改保存。
