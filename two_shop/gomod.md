## 包管理工具 gomod

go的程序会分门别类的组织成若干组文件，每组文件被称为一个包。<br/>

每个go文件都属于且只能属于一个包，并且在源文件的第一行必须要使用 **package 包名**  来指名文件的包所属关系。<br/>

go的代码组织就是通过定义这些不同的包来实现的。<br/>


go的标准库代码在GOROOT/src下，而用户的代码都在GOPATH/src下；<br/>
开发时所有的包都放在GOPATH/src下 很混乱，所以go 在go1.11之后的版本增加了go module的功能，简称 **gomod**。

#### 什么是module？
在go语言安装的章节中，介绍了所有的go源代码都需要放置在GOPATH中；但是如果不同的工程依赖了不同版本的相同go源码模块，这种方式就会出现冲突。那么为了脱离GOPATH的代码管理，module应运而生。<br/>

module 就是为了方便我们管理项目代码使用的，它是一个版本控制单元，是一系列相关包的集合表示。<br/>

#### 开启gomod可用
可以使用环境变量GO111MODULE选择开启或者是关闭module模块的支持。有三个值可选:
* GO111MODULE=off, 关闭module功能, 到GOPATH中寻找依赖
* GO111MODULE=on, 代码不会到GOPATH中去寻找
* GO111MODULE=auto, go命令行根据当前目录来决定是否启用module, 当在GOPATH目录外且有go.mod文件时启用module

#### 创建新项目

创建项目文件夹
```
mkdir payment
cd payment
```
初始化module
```
go mod init github.com/willierGo/payment
```

**go mod init**后面是模块的名称，执行完该命令就会生成 **go.mod** 文件, go.mod文件就标识着它所在的目录是一个模块。


#### gomod的其他常用命令

| 命令            | 说明                           |
| --------------- | ------------------------------ |
| go mod tidy     | 拉取缺少的模块，移除不用的模块 |
| go mod verify   | 验证依赖是否正确               |
| go mod graph    | 打印模块依赖图                 |
| go mod download | 下载依赖包                     |
| go mod version  | 将依赖复制到vendor下           |