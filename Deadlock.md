#死锁

---
## 运行代码，观察死锁
**1.实验流程**：
<p>
* 在Deadlock.java里面编写如下代码：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-71ae111725a1f048.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>![](http://upload-images.jianshu.io/upload_images/3239746-fbc5d73c6bd8c94f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>
* 在终端运行指令：javac Deadlock.java，编译结果如下：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-d9bf4d84a8de7ffb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)    
<p>
* 在Deadlock.bat文件中编写如下代码，然将批处理文件放在java程序（Deadlock.class）目录下：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-d699814db77e2d3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<P>
* 在终端输入如下指令，调节程序中count值为3000，观察死锁：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-4128a0caca0ee0b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>
**2.实验结果**：
<p>在第2844次的时候发生死锁，运行的程序中端：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-ff56882788311771.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##产生死锁的4个必要条件
* 首先理解死锁产生的原因：死锁是指在一组进程中，各个进程均占有不会释放的资源，但因互相申请被其他进程所占用的不会释放资源而处于的一种永久等待状态
* 4个必要条件：
  * <p>互斥条件：一个资源每次只能被一个进程使用
  * <p>请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
  * <p>不剥夺条件:进程已获得的资源,在未使用完之前不能强行剥夺
  * <p>循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系

##对上述程序产生死锁的解释
* 首先观察代码块 class Deadlock：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-fbc5d73c6bd8c94f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  * <p>主函数当执行t.start()之后，线程t就被插入到调度队列里，当调度到Runnable（一个在后台运行的线程）的时候，就执行run()里面的代码，这时候b会调用class B的methodB方法,稍后再讨论methodB的具体实现。
  * <p>回到主线程中，主线程等在count(10000)后继续执行，此时开始a调用class A的methodA方法。
* 接着观察代码块class A和class B：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-71ae111725a1f048.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  * <p>注意用synchronized修饰的方法或者代码块，在同一时刻最多只有一个线程执行该段代码。而当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。
  * <p>结合代码块 class Deadlock，当b访问methodB会调用class A的last方法，而当a访问methodA也会访问代码块classB的last方法。而synchronized修饰的方法或者代码块被访问时，object中其它synchronized同步代码块或同步方法的访问将被阻塞。所以当a.methodA(b)和b.methodB(a)执行的时间差不多，就是因为同步方法不能被访问而产生死锁。
