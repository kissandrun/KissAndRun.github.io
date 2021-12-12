# 👨‍💻Windows 下优秀软件推荐(2)

Windows下不仅仅有 **360**全家桶，腾讯全家桶等毒瘤软件，也有很多优秀的效率工具。本文将介绍一些能够大大提升开发效率。

## **RaiDrive** 硬盘映射工具

**RaiDrive** 是一款将网络位置（比如服务器）映射为本地磁盘的工具。同时也支持支持 **Google Drive**、**Google Photos**、**Dropbox**、**OneDrive**、**FTP**、**SFTP**、**WebDAV**。其中 **SFTP** 能够直接利用SSH协议映射硬盘，不需要在服务器上做额外的操作。

![image-20210331183022193](https://i.loli.net/2021/03/31/vsHUzXnQV5e2qR7.png)

如上图，添加一个SFTP地址，填入**SSH**协议的**ip**地址和端口号，使用密码登录或者**Key**登录即可。完成后即可在**我的计算机**里面找到添加的网络位置。可以像操作本地磁盘一样操作服务器上的磁盘了。

![image-20210331183244322](https://i.loli.net/2021/03/31/cdGuBJMeXUOPhCr.png)

## Tmux 终端复用工具

**Tmux**是一个终端复用的命令行工具。所谓的终端复用就是在一个终端里面使用多个终端。不仅如此，它还可以让你的程序始终处于运行状态，不管终端是否关闭，只要你的 **Tmux** 进程没有停止。这就对深度学习训练特别有用。

试想这样一个情形，你用 **Pycharm** 写了代码，并上传到了服务器，利用 **Pycharm** 的终端开始了训练，这时你不小心把 **Pycharm** 关了，或者突然断电了，或者 **Win10** 又蓝屏又重启更新了，那你的训练就强制停止了。

而如果你是在 **Tmux** 里的训练的，那没有任何问题，你只要重新 **attach** 回之前的那个 **session** 就行。

![https://i.loli.net/2020/11/22/XqCRiMG7oYpQyu9.png](https://i.loli.net/2021/03/31/GfoQruzOjJItiBm.png)

### 安装 Tmux

首先先确认一下是否安装 **Tmux**，直接在终端输入`tmux`如果提醒命令没找到就使用`sudo apt install tmux`安装 **tmux**。然后再在终端输入`tmux`就可以建立一个新的会话。详细的`tmux`教程可以看 [Tmux 使用教程](http://www.ruanyifeng.com/blog/2019/10/tmux.html)

#### 分离会话（暂时退出该tmux会话）

在 Tmux 窗口中，按下**Ctrl+b d**或者输入**tmux detach**命令，就会将当前会话与窗口分离。

> $ tmux detach

上面命令执行后，就会退出当前 Tmux 窗口，但是会话和里面的进程仍然在后台运行。**tmux ls**命令可以查看当前所有的 **Tmux** 会话。

> $ tmux ls

or

>  $ tmux list-session

#### 接入会话（重新回到tmux会话）
**tmux attach**命令用于重新接入某个已存在的会话。

使用会话编号

> $ tmux attach -t 0

#### 使用会话名称

> $ tmux attach -t  <session-name>

## 其他优秀的效率工具

[👨‍💻Windows 下优秀软件推荐 - No Visitor Website (kissandrun.github.io)](https://kissandrun.github.io/app-0/)

这里面推荐了一些，比如**Autohotkey**，**utools**，**Everything**，**Windows Subsystem for Linux(WSL)**

[装机用所有软件合集 | Yang's blog (yangt.me)](https://yangt.me/post/apps-recommended/)

这里面也有一些优秀的软件。
