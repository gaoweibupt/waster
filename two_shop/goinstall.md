## go 语言环境安装


##### 下载地址:
[go语言中文网 https://studygolang.com/dl](https://studygolang.com/dl)

### Linux or Mac 安装
##### 下载:
```
wget https://dl.google.com/go/go1.1X.对应系统版本.tar.gz
```
##### 解压:
```
tar -C /usr/local -xzf go1.1X.对应系统版本.tar.gz
```
##### 修改环境变量:
```
vim ~/.bashrc
```
```
export GOROOT="/usr/local/go"
export GOPATH="~/go"
export GOBIN="~/go/bin"
export PATH="$PATH:$GOROOT/bin:$GOBIN"
# go代理，可以访问被墙的代码库
GOPROXY=https://proxy.golang.org,direct
```
```
source ~/.bashrc
```
##### 测试:
执行如下命令，可以输出go环境变量信息则为安装成功
```
go env
```

### windows 安装
#### 下载与安装
下载 [.msi 文件](https://studygolang.com/dl/golang/go1.14.3.windows-386.msi)，直接进行安装。

#### 修改环境变量
.msi 文件的安装默认会修改环境变量，安装完成之后可以打开cmd执行
```
go env
```
如果命令不存在的话，检查系统的环境变量：
[windows 如何添加环境变量](https://jingyan.baidu.com/article/47a29f24610740c0142399ea.html)


设置GOROOT为go的安装目录，并将 **%GOROOT%\bin;**  加入到 系统的path中。

### 详解环境变量
#### GOROOT
golang 的安装路径
go的可执行文件在$GOROOT/bin下，因此需要将 **$GOROOT/bin** 加入到系统的环境变量PATH下。
#### GOPATH
使用绝对路径作为GOPATH，即项目的工作目录，允许使用 **";"** 来分割多个目录。
按照约定，GOPATH下一般有三个目录:

* src
* pkg
* bin

其中, 源代码总是会保存在src目录下；经过go build、go install或者go get指令会产生二进制的可执行文件，将会保存在bin目录下，也可以通过GOBIN环境变量指向其他的目录；pkg文件存放了编译过程中产生的中间缓存文件。