title: Sulime Text 2在Ubuntu上的安装和配置（一）
date: 2015-12-24 01:40:29
tags:
---
### 前言
工欲善其事，必先利其器。
在Ubuntu操作系统中，好多看似简单的事情，比如安装个软件甚至创建个桌面快捷方式都不是像windows操作系统一样，点点鼠标就能做到，然而好多开发环境对windows实在是不友好，而且windows自带的命令行和shell简直不能忍有木有。
这是一个鼓捣的过程，为了打造一个优雅的开发环境（其实是没钱买苹果），我们开始吧
<!--more-->
### 1. 下载
[Sublime官网下载地址][1]
请选择合适的版本和对应的操作系统，这里我们选择linux 64 bit
### 2. 安装
得到下载文件后，安装是一个解压的过程，您可以选择使用linux的命令

```bash 
$ tar -zxvf Sublime Text 2.0.2 x64.tar.bz2
```
也可以直接右键提取文件
现在我们得到一个名为**Sublime Text 2**的文件夹，为了后续操作方便，您可以把文件夹的名字中的空格改掉，这里我没有改变。其实现在我们打开文件夹根目录，双击sublime_text就可以使用，然而每次都去相应的文件夹找很麻烦，我们希望可以在桌面或者快速启动栏中都可以找到Sublime的快捷启动方式，就像windows那样。那么问题来了：~~挖掘机技术。。。~~ **Ubuntu如何建立快捷方式**
### 3. 快捷方式的建立
* 建立命令行链接
  我们首先要做的是想在bash中使用一行命令打开sublime，这看上去并没有什么神奇，你现在似乎也不明白为什么要多此一举。实际上我们是为了后续的操作才这么做的。
我们把解压后的文件夹复制到**/urs/lib**中去

``` bash
$ sudo mv Sublime\ Text\ 2 /usr/lib/
```

注意命令中空格前面的\，这是为了转义。这也是为什么一开始建议大家的文件夹名字中最好不要有空格的原因，毕竟怎么简单怎么来。复制到/usr/lib中的意义是，因为$PATH这个环境变量自动涵盖了/usr/lib这个目录，不用专门去修改环境变量。
下一步就是建立命令的链接，使用ln命令

``` bash 
$ sudo ln -s /usr/lib/Sublime\ Text\ 2/sublime_text  /usr/bin/something
```

你可以把bin后面的"something"改成任何东西，我直接使用"sublime"
现在你在命令行中键入

``` bash
$ sublime
```

就可以打开sublime了
* 新建桌面方式配置文件sublime.desktop
你会说，怎么还没完啊，我还是没看到快捷方式的影子啊。是的，在linux中，好多操作都得亲自写配置文件，不用着急。
我们需要先去这个路径下**/usr/share/appliations/**，这是一个神奇的路径，你会看见好多.desktop为结尾的文件，它们在侧边栏和dash中都能找到，如果我们建立了**sublime.deskdop**的文件，想必也可以咯。你可以使用[vim][2]做这件事
``` bash
[Desktop Entry]
Version=2.0.2
Name=Sublime Text 2
GenericName=Text Editor
Exec=sublime %F
Terminal=false
Icon=/usr/lib/Sublime Text 2/Icon/48x48/sublime_text.png
Type=Application
Categories=TextEditor;IDE;Development
X-Ayatana-Desktop-Shortcuts=NewWindow
```
其中**Exec=**后面的**sublime**就是我们之前用**ln**命令定义的链接名字。
Now，保存之后，你就可以在**/usr/share/appliations/**看到sublime的图标了，拖动它到桌面或者侧边栏就可以啦
### 补刀
你叹了口气说终于完了，不过我听说另一种方法可以轻松搞定以上所有

``` bash
$ sudo add-apt-repository ppa:webupd8team/sublime-text-2
```

``` bash 
$ sudo apt-get update
```

``` bash 
$ sudo apt-get install sublime-text-2 
```

你是不是很想杀人，不过我也没试过，下集见

[1]: http://www.sublimetext.com/2
[2]: http://buildall.github.io/2015/12/09/frontendvim/