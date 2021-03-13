# 2021-linux-public-zhang-de-xin
2021-linux-public-zhang-de-xin created by GitHub Classroom
## 第一章实验  无人值守安装

#### 实验步骤

1.先手动安装，新建虚拟机

![1](https://user-images.githubusercontent.com/56664193/111030699-b259cb00-843e-11eb-9be0-65d62b5865d2.png)

2.设置双网卡，host-only。然后选择提前下载好的Ubuntu安装镜像文件，启动虚拟机。

![2](https://user-images.githubusercontent.com/56664193/111030702-b4238e80-843e-11eb-8c97-e5b054c5acd7.png)

3.启动虚拟机后，进行虚拟机配置选择，然后等待安装

![3](https://user-images.githubusercontent.com/56664193/111030703-b4bc2500-843e-11eb-92a7-b520a1abc150.png)

4.安装完成，输入用户名和密码


![4](https://user-images.githubusercontent.com/56664193/111030706-b554bb80-843e-11eb-89f7-7b423591d827.png)

![5](https://user-images.githubusercontent.com/56664193/111030707-b5ed5200-843e-11eb-9244-0600ff00bcf7.png)

5.尝试制作无人值守安装镜像文件，我阅读了下面两个链接的文章，但还是没弄出来。第一篇文章我照着上面说的在终端输入它提供的代码，但运行不了，这个我是在宿主机终端命令行输入的。

![6](https://user-images.githubusercontent.com/56664193/111032077-99084d00-8445-11eb-98a9-23432f4edab5.png)

![7](https://user-images.githubusercontent.com/56664193/111032082-9ad21080-8445-11eb-9fd9-21240dea6366.png)

然后我又照着第二篇文章的代码输入了一下，这个是在虚拟机命令行输入的，结果如下：

![8](https://user-images.githubusercontent.com/56664193/111032083-9b6aa700-8445-11eb-84e0-a393db542f26.png)

![9](https://user-images.githubusercontent.com/56664193/111032084-9c033d80-8445-11eb-9ecb-b162b1a782d5.png)

第一个代码运行成功了，第二和第三个代码似乎没运行成功，实在搞不懂。

6.于是选择偷懒，用老师配置好的focal-init.iso文件，按顺序导入两个虚拟盘，配置双网卡，启动虚拟机

![10](https://user-images.githubusercontent.com/56664193/111032085-9c9bd400-8445-11eb-85d7-073e12175339.png)

7.在此处输入yes，然后开始无人值守安装

![11](https://user-images.githubusercontent.com/56664193/111032087-9d346a80-8445-11eb-834b-7275dd4053a4.png)

8.安装完成，输入用户名密码。因为用的是老师的，所以都是cuc，不能自己配置

![12](https://user-images.githubusercontent.com/56664193/111032089-9dcd0100-8445-11eb-8e0b-ba8c01bc8a7d.png)

#### 实验问题

1.有人值守安装虚拟机的时候遇到了[FAILED] Failed unmounting /cdrom 的问题，删除虚拟机又试了几次，一直有，最后选择继续执行，顺利完成了安装。后来问了老师，老师说安装结束后就不用再挂载光盘了。

2.GitHub上不去，去CSDN查了解决办法，修改hosts文件，加入查询到的IP。虽然上得去了，但还是十次有七八次都上不去，一直在查IP换IP，太难了，简直就是浪费时间。

#### 实验总结

还是没学会怎么配置自动安装镜像文件，但过程基本清楚了，希望老师可以演示一下。本来我想自己再研究一下的，但是GitHub太搞心态了，这次实验一大半的时间都是花费在尝试连接GitHub上。而且连不上GitHub，连作业都交不上，这个网真的恶心。
