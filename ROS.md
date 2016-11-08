#安装ROS

---
##安装
**1.配置 Ubuntu 软件仓库**
<p>配置Ubuntu 软件仓库(repositories) 以允许 "restricted"、"universe" 和 "multiverse"这三种安装模式（注：此步骤可以不执行，默认允许上诉三种安装模式）：
* <p> 允许 "restricted"、"universe" 和 "multiverse"这三种安装模式,这里取消了main模式：
![](http://upload-images.jianshu.io/upload_images/3239746-2e344a3778539541.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* <p>点击Reload重新加载：
<p>![](http://upload-images.jianshu.io/upload_images/3239746-b3984643ac006932.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<p> 
**2.添加 sources.list**
<p>配置ubuntu使其能够安装来自 packages.ros.org的软件包。这里选择ustc的镜像源：
<p>
``` 
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list' 
```
<p>![](http://upload-images.jianshu.io/upload_images/3239746-ad86a3554eaad9f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<p>
**3.添加 keys**
<p>
```
sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116
```
![](http://upload-images.jianshu.io/upload_images/3239746-317ff635d4deeb0b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>注：这里因为已经成功安装ROS多次，但是之前安装时没有截图，所以有些会提示已经存在。

<p>
**4.安装**
<p>
* 首先更新Debian软件包索引
<p>
``` 
sudo apt-get update ```
<p>![](http://upload-images.jianshu.io/upload_images/3239746-2a25082040a4311e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>
* 安装桌面完整版（这里也是因为已经安装过了）：
<p>
```
sudo apt-get install ros-jade-desktop-full```
<p>
![](http://upload-images.jianshu.io/upload_images/3239746-43d1908682593460.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<p>
**5.初始化 rosdep**
<p>
```
sudo rosdep init
rosdep update
```
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/3239746-cd2609958730282b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<p>注：结果报错是因为已经存在这个文件夹了。

<p>
**6.环境配置**
<p>
``` 
echo "source /opt/ros/jade/setup.bash" >> ~/.bashrcsource ~/.bashrc
```
![](http://upload-images.jianshu.io/upload_images/3239746-e5655a91ff3c3661.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<p>
**7.安装 rosinstall**
<p>
```
sudo apt-get install python-rosinstall
```
![](http://upload-images.jianshu.io/upload_images/3239746-73c64cbbc690ac8d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
