# 第二章实验

#### 软件环境

- 当前课程推荐的 Linux 发行版本
- 在[asciinema](https://asciinema.org/)注册一个账号，并在本地安装配置好asciinema

- 确保本地已经完成**asciinema auth**，并在[asciinema](https://asciinema.org/)成功关联了本地账号和在线账号

- 上传本人亲自动手完成的**vimtutor**操作全程录像

- 在自己的github仓库上新建markdown格式纯文本文件附上asciinema的分享URL

- **提醒** 避免在终端操作录像过程中暴漏**密码、个人隐私**等任何机密数据

  ```
  # 下载安装简体中文语言包
  sudo apt update && sudo apt install language-pack-zh-hans
  
  # 临时设置 简体中文 环境变量并启动 vimtutor
  LANG=zh_CN.UTF-8 vimtutor
  ```

#### 实验步骤

1.注册账号并安装asciinema

```Ubuntu
sudo apt-add-repository ppa:zanchey/asciinema
sudo apt-get update
sudo apt-get install asciinema
```

![image-20210603160025585](C:\Users\12524\AppData\Roaming\Typora\typora-user-images\image-20210603160025585.png)

2.连接库，复制链接，从当前登录界面粘贴进入网址

```Ubuntu
asciinema auth
```

![image-20210603160926407](C:\Users\12524\AppData\Roaming\Typora\typora-user-images\image-20210603160926407.png)

![image-20210603161345777](C:\Users\12524\AppData\Roaming\Typora\typora-user-images\image-20210603161345777.png)

3.进行**vimtutor**操作全程录像

```
asciinema rec  //开始录制
vimtutor  //进入指南阅读界面
exit  //结束录制，按enter得到链接
```

##### asciinema的分享URL：

##### lesson 1.1

[![asciicast](https://asciinema.org/a/Ofk02Gugi26LGFTfJlGETk4c6.svg)](https://asciinema.org/a/Ofk02Gugi26LGFTfJlGETk4c6)

##### lesson 1.2

[![asciicast](https://asciinema.org/a/MeB2YaYChq1BtwGgGmqdnVo09.svg)](https://asciinema.org/a/MeB2YaYChq1BtwGgGmqdnVo09)

##### lesson 1.3

[![asciicast](https://asciinema.org/a/qh1mMC4g4oyNERaIPd30KABDp.svg)](https://asciinema.org/a/qh1mMC4g4oyNERaIPd30KABDp)

##### lesson 1.4

[![asciicast](https://asciinema.org/a/pqHMx8GK7kX7WE4GemGP8KdMC.svg)](https://asciinema.org/a/pqHMx8GK7kX7WE4GemGP8KdMC)

##### lesson 1.5

[![asciicast](https://asciinema.org/a/IudSdemi6k0coa5kMRn6QTqgz.svg)](https://asciinema.org/a/IudSdemi6k0coa5kMRn6QTqgz)

##### lesson 1.6

[![asciicast](https://asciinema.org/a/j7H9Y57CD8iiVFMmGG4P2TQcA.svg)](https://asciinema.org/a/j7H9Y57CD8iiVFMmGG4P2TQcA)

##### lesson 2.1-2.2

https://asciinema.org/a/L8M1xivh9SXPsyN76yfPliAZG

##### lesson 2.3

https://asciinema.org/a/DwIKFlnh2ssDy69GHFqU1XwYL

##### lesson 2.4-2.5

https://asciinema.org/a/za3FqxOQFbzX9Ncg3md6EHR3W

##### lesson 2.6-2.7

https://asciinema.org/a/gjQrA8g4Semt1k20ubGrMq9qu

##### lesson 3.1

https://asciinema.org/a/cropeIMEzpgkV3WDXqATlASDp

##### lesson 3.2-3.4

https://asciinema.org/a/FGFeGPOZWYBYADVzFAKToM7ZR

##### lesson 4.1

https://asciinema.org/a/jwxuyBb6BioH7E9mIT4y9vV0M

##### lesson 4.2

https://asciinema.org/a/ZGFS4QefdIBAdDAt3gjbp8n2x

##### lesson 4.3-4.4

https://asciinema.org/a/RToXJFyD7XbJ2G49Q3g1fSJod

##### lesson 5.1-5.4

https://asciinema.org/a/RbaujoEdYUXalNxfvlG2id3hP

##### lesson 6.1-6.3

https://asciinema.org/a/8yw8iTGaQ5MzpN5LJ7sukAh4h

##### lesson 6.4

https://asciinema.org/a/WgGoJRoTgh4zeR8UWQ73Fwl56

##### lesson 6.5

https://asciinema.org/a/LUCqU4bcWhkRnHsg75gPbf8Op

##### lesson 7.1

https://asciinema.org/a/GIwSHnUPmoCEaATptdiu56tdh

##### lesson 7.2-7.3

https://asciinema.org/a/cTLNlinw36KfnTDgPkxXTp650

#### 自查清单

- ##### 你了解vim有哪几种工作模式？

  正常模式，编辑模式，命令模式，Visual模式

- ##### Normal模式下，从当前行开始，一次向下移动光标10行的操作方法？如何快速移动到文件开始行和结束行？如何快速跳转到文件中的第N行？

  10j，gg，G，NG

- ##### Normal模式下，如何删除单个字符、单个单词、从当前光标位置一直删除到行尾、单行、当前行开始向下数N行？

  单个字符：按x

  单个单词：将光标移动至需要删除的单词的首字母处，然后按下dw

  删除到行尾：按下d$，可以删除当前光标处至行尾的所有字符

  删除单行：按dd

  删除N行：按Ndd

- ##### 如何在vim中快速插入N个空行？如何在vim中快速输入80个-？

  No 下方，NO 上方

  80i-esc或80a-esc，大小写都行

- ##### 如何撤销最近一次编辑操作？如何重做最近一次被撤销的操作？

  u：撤销上一次操作

  U：撤销整行的操作

  CTRL-R：恢复撤销

- ##### vim中如何实现剪切粘贴单个字符？单个单词？单行？如何实现相似的复制粘贴操作呢？

  单个字符：x删除（剪切），p粘贴

  单个单词：dw删除单词，p粘贴

  通过visual模式，v选择行

  y：复制

- ##### 为了编辑一段文本你能想到哪几种操作方式（按键序列）？

  a A i I 插入模式

  x d 删除

  y 复制

  p 粘贴

  r R替换

  o O 插入新行并进入插入模式

  e 移动至词尾

- ##### 查看当前正在编辑的文件名的方法？查看当前光标所在行的行号的方法？

  在正常模式下，键入CTRL-G，会显示出光标的位置和文件的状态信息

- ##### 在文件中进行关键词搜索你会哪些方法？如何设置忽略大小写的情况下进行匹配搜索？如何将匹配的搜索结果进行高亮显示？如何对匹配到的关键词进行批量替换？

  键入“/search”，表示从光标处向下搜索search字符串

  想要顺着搜索方向搜索下一个PHRASE，键入n

  想要逆着搜索方向搜索下一个PHRASE，键入N

  忽略大小写：

  :set ignorecase

  :set ic

  高亮：

  :set hlsearch

  替换：

  :s/替换目标/替换为

  全局替换：

  :s/替换目标/替换为/g

- ##### 在文件中最近编辑过的位置来回快速跳转的方法？

  CTRL-O：回到刚才的位置

  CTRL-I：去往下一个新位置

- ##### 如何把光标定位到各种括号的匹配项？例如：找到(, [, or {对应匹配的),], or }

  %：跳转至另一半括号或者光标所在处最近的右括号

- ##### 在不退出vim的情况下执行一个外部程序的方法？

  :!<command>

- ##### 如何使用vim的内置帮助系统来查询一个内置默认快捷键的使用方法？如何在两个不同的分屏窗口中移动光标？

  :help（可以在:help后加参数，查看对应的subject的帮助）

  CTRL-W