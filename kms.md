# 前言

KMS(Key Management Server),[密钥管理服务器](https://zh.wikipedia.org/wiki/金鑰管理伺服器).
<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">
自建KMS服务器激活Windows和Office
是原创的 是原创的 但是就是过不了审 一个字一个字敲的 一张图一张图拍的  就是过不了

# 一、环境说明

# 二、使用步骤

## 1.安装使用vlmcsd

> [github项目地址](https://github.com/Wind4/vlmcsd)

1. 打开github的项目地址
![image-2021040619194901](https://img-blog.csdnimg.cn/20210406230159880.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)

2. 找到最新的releases，并复制链接

![](https://img-blog.csdnimg.cn/202104062302286.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)


> binaries 是编译好的版本 可以拿过来直接用
>
> source 是源代码，需要自己编译以后才能使用

3.  登录服务器(ubuntu)

```
ssh ***************************
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230248907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)

4. 找一个自己喜欢的位置下载安装 (我喜欢`usr/local/`)
```
cd /usr/local
mkdir kms
mkdir installed.d   # installed目录用来存放安装包
cd installed.d
```
5. 使用wget下载第二步复制的链接
```
wget https://github.com/Wind4/vlmcsd/releases/download/svn1113/binaries.tar.gz
```
6. 解压压缩包到kms目录下
```
tar xvf binaries.tar.gz -C  ../
```
>tar命令 可以为linux的文件和目录创建档案。
>-x或--extract或--get：从归档文件中提取文件，可以搭配-C（大写）在特定目录解开，需要注意的是-c、-t、-x不可同时出现在一串命令中；
>-v：显示操作过程
>-f<备份文件>或--file=<备份文件>：指定备份文件；
>......

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230301773.png)


7. 查看ubuntu服务器的硬件信息（为安装做准备）
```
lshw -short
```
>lshw命令显示详细硬件信息。如果要用概要方式显示，可以加上short参数：lshw -short
>要显示指定硬件信息，加上class(或C)参数：lshw -class memory

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230309991.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)


8. 进入我们服务器对应的安装包
```
cd binaries/Linux/intel/static
```
9. 基于我们的系统版本，执行对应的文件
```
./vlmcsdmulti-x64-musl-static vlmcsd
```
没有任何错误提示，则代表我们运行成功了

**注意：**防火墙记得开放端口！ （专栏会有专门一篇博客学习使用防火墙.）

10. 查看vlmcsd的运行情况，查看1688端口状态

> KMS 主计算机名称是由 KeyManagementServiceName (REG_SZ) 指定的，而端口是由 KeyManagementServicePort (REG_SZ) 指定的。 默认端口为 1688。
> netstat命令 用来打印Linux中网络系统的状态信息，可让你得知整个Linux系统的网络情况。找出运行在指定端口的进程： netstat -an | grep ':80'
```
ps aux | grep vlmcsd
netstat -an | grep ':1688'
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230320342.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)


## 2.激活office
注册kms服务器地址（管理员身份运行）
```bash
cscript ospp.vbs      /sethst:yours.kms
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230329729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)

手动激活
```
cscript ospp.vbs      /act
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230337609.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)


激活成功-查看

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230345724.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)


## 3.激活windows
运行批处理激活windows
```
# 激活脚本.bat
# yours.kms 你的kms服务器地址
cd /d "%SystemRoot%\system32"
slmgr /skms yours.kms 
slmgr /ato
slmgr /xpr
```
查看window激活状态
```
slmgr.vbs -xpr
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230354896.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)


查询Win10激活状态的详尽信息

```
slmgr.vbs -dlv
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210406230402865.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NjI4NTk1,size_16,color_FFFFFF,t_70)

# 总结

# 参考文献

[使用 KMS 激活 Office 的批量许可版本](https://docs.microsoft.com/zh-cn/deployoffice/vlactivation/activate-office-by-using-kms)