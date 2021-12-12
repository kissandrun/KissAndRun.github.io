# 如何用远程服务器进行开发？

作为一个炼丹术士，操作服务器是家常便饭，如何高效的操作服务器，管理环境，运行代码便成了头等大事。炼的好不好先不说，得先炼得舒服。

常用的方法无非以下几种：
1. 利用远程桌面（**teamviewer**，**VNC** 等工具）全程 **GUI** 操作
2. 利用本地端的 **IDE**（如 **Pycharm**）或者代码编辑器（如 **VS Code** 等）写代码，然后利用他们的 **Remote Tools** 进行代码上传等
3. **SSH** 到远程服务器，全程 **CLI** 操作

本文将详细介绍这三种开发的方式

## SSH (Secure Shell) 

如果你操作远程服务器，那你一定接触过 SSH，如果没有那一定是没到家。SSH是最为基础的连接远程服务器的方法。`windows`的`powershell`和几乎所有的`Linux`发行版都自带`SSH`，可以在终端中使用。
![](https://atulhost.com/wp-content/uploads/2020/04/ssh.png)
常用的命令是

```
ssh user@domain.com

比如
ssh hth@10.9.xx.xx

如果有端口限制则需要加入 -p 参数
ssh -p 端口号 user@domain.com
```
`Windows`下也可以使用`PuTTY`等工具使用`SSH`。这里不得不再推荐一下`Windows Subsystem for Linux`因为服务器是`Linux`系统，统一一下环境岂不美哉。

连接上之后就是一个小黑框，里面就可以输入命令行了，可以使用命令行工具比如**Tmux**和**Vim**进行开发了，不过单纯的使用**CLI**比较的难，可以采用**Visual Studio Code** 进行开发。

## Visual Studio Code

[VSCode](https://code.visualstudio.com/) 是一个全平台通用的文本编辑器，在官网下载安装即可。

![](https://cdn.jsdelivr.net/gh/TianYang-TY/myPic/20201124145300.png)

### [Remote-SSH / 远程开发](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)

安装方法如下所示：

![image-20210329150007094](https://i.loli.net/2021/03/29/HxRXdKcWF3UhYwD.png)

可以让通过**SSH**连接远程服务器作为本地的开发环境，连接远程服务器最好使用 **SSH key**，不建议使用密码，否则会不停地在输入密码。

![image-20210329145458065](https://i.loli.net/2021/03/29/YidFl1kwMZDzO4r.png)

如上图所示，装完最左边的导航栏中就有了远程管理的图标，在里面可以管理你的所有**SSH目标**，此时新建终端出现的也是远程的终端，此时安装插件也将装在远程服务器上。

### [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)插件

安装方法和上面相似

![image-20210329150156803](https://i.loli.net/2021/03/31/G19dLTQgxktUmq5.png)

**VSCode** 的 **Python** 扩展，使 **VSCode** 拥有调用 **Python** 解释器的功能。安装成功之后可以新建一个 `.py` 文件，然后在窗口的左下角选择 **Python** 解释器，**VSCode** 会自动搜索系统中的 **Python** 环境。然后可以 `print('hello world')` 检查一下是否有问题。

![image-20210329151433870](https://i.loli.net/2021/03/31/HvEq5oNzmr6dBlO.png)
当然细节还有很多，比如代码的美化（Format），错误提示（Lint），代码补全（Completion）等等，这些熟悉了基本操作之后再了解也不迟。



### Python远程调试

![image-20210329154818966](https://i.loli.net/2021/03/29/nLOBowWuDmiGrtX.png)

点击如上框出的按钮,选择调试打开的文件。

调试前可以在行号前打上断点，然后在进行上面的调试，左侧能查看变量，上方的悬浮框可以进行单步调试。

![image-20210329155203342](https://i.loli.net/2021/03/29/xzkvn6wZyRuOKJL.png)

