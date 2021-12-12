# 如何充分利用校园网


校园网非常坑，时不时就断了，但校园网也非常的良心，因为他连接校内IP不要钱，不要钱，不要钱，还是上下对等千兆！设备连上了的校园网就会得到一个校内IPv4地址和全球IPv6地址，这俩都是好东西。

## 校内IP

可以在 **设置/网络和Internet/属性** 里面查看当前网络的地址。校内IPv4 一般长的是 `10.*.*.*` 这个样子，IPv6地址一般长的像 `2001:*:*:*:*:*`的很长一串。但下面这个，就没有拿到校内IP，明显是因为这个设备是路由器下的一个子设备，拿到的地址是`192.168.*.*`这样的地址。这样的设备是不能作为服务端的，除非在路由器内进行端口绑定，给每一个设备绑定一个端口。但是是可以作为客户端的。

![image-20210507151903042](https://i.loli.net/2021/05/07/TZW8RKyFPqnglYj.png)

## 校园网内传输文件

还在使用传统的U盘传文件？还在用垃圾百度网盘传文件？千兆校园网免费传文件为啥不用呢！
传文件的话总是两个设备直接传文件，我们可以通过一些网络协议进行文件的传输，比如`FTP`,`SFTP`,`WebDav`等等。传文件的逻辑是这样的，一个设备为服务端，进行文件的存储，然后多个设备为客户端，可以通过传输协议从服务端读或写文件，显然我们平时的生活中客户端一般都是**Windows**系统的电脑，使用**Linux**系统的用户也不会来看这篇科普文章了。

![](https://nimg.ws.126.net/?url=http%3A%2F%2Fdingyue.ws.126.net%2F2021%2F0308%2F9a636462j00qpmwil000kc000hs00bvg.jpg&thumbnail=650x2147483647&quality=80&type=jpg)

### 客户端软件 RaiDrive

**RaiDrive** 是一款将网络位置（比如服务器）映射为本地磁盘的工具。同时也支持支持 **Google Drive**、**Google Photos**、**Dropbox**、**OneDrive**、**FTP**、**SFTP**、**WebDAV**。

#### 以 Linux 为服务端

以 **Linux** 为服务端，就很方便，因为使用自带的SFTP协议就可以了，不用安装额外的应用，可以说服务端无需配置。

 **SFTP** 能够直接利用**SSH**协议映射硬盘，不需要在服务器上做额外的操作。

![image-20210331183022193](https://i.loli.net/2021/03/31/vsHUzXnQV5e2qR7.png)

如上图，添加一个**SFTP**地址，填入**SSH**协议的**IP**地址和端口号，使用密码登录或者**Key**登录即可。完成后即可在**我的计算机**里面找到添加的网络位置。可以像操作本地磁盘一样操作服务器上的磁盘了。

![image-20210331183244322](https://i.loli.net/2021/03/31/cdGuBJMeXUOPhCr.png)

#### 以 Windows 为服务端

Windows 虽然有自带的共享功能，但我不会用，整不明白 Windows 的用户权限。推荐使用 **FileZilla Server**软件，创建一个 **FTP** 服务端。参考 [FTPZilla Server简单配置FTP服务器](https://blog.csdn.net/weixin_42828211/article/details/81291649)

## 远程桌面

还在使用**TeamViewer**？在校园网环境下，可以使用**Windows**自带的远程桌面。

要求是被控设备需要是 **Windows 10** 专业版或者教育版，同时拥有校内**IP**。如下图，允许通过远程连接此电脑。

![image-20210507153116493](https://i.loli.net/2021/05/07/zJstRkvgcA2pI57.png)

客户端则没有版本要求。打开**Windows**自带的远程桌面

![image-20210507153353497](https://i.loli.net/2021/05/07/KsPGVLa3toYZMvX.png)

在计算机栏输入 被控设备的 **IP**

![image-20210507153615278](https://i.loli.net/2021/05/07/zTx7ncdX2CWRVb9.png)

## 充分使用 IPv6 

首先测试自己是否拥有 **IPv6**，进入网站[IPv6 测试 (test-ipv6.com)](https://test-ipv6.com/index.html.zh_CN)

如果拥有**IPv6**的话，就可以使用 **IPv6**了，目前最大的用途就是玩**PT**，可以访问
蒲公英Pt https://npupt.com 进行探索。
