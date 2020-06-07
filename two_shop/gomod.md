## 包管理工具 


不使用包管理工具，完全依靠GOPATH：

* 每次项目都要手动设置GOPATH
* 依赖需要手动go get
* GOPATH 依赖的项目没有版本管理
* ... 谁用谁知道

go是开发者比较活跃的一门语言，官方和社区的迭代都非常迅速，大家也都探索过很多go的包管理方式：

* godep
* govendor
* go module

go module是go1.11版本才开始推出的，相比于godep 和 govendor更加灵活并且解决了依赖包版本管理的问题，所以到go1.13已经成为了go语言开发的默认模式。


### gomod

开发时所有的包都放在GOPATH/src下 很混乱，所以go 在go1.11之后的版本增加了go module的功能，简称 **gomod**。

#### 什么是module？
在go语言安装的章节中，介绍了所有的go源代码都需要放置在GOPATH中；但是如果不同的工程依赖了不同版本的相同go源码模块，这种方式就会出现冲突。那么为了脱离GOPATH的代码管理，module应运而生。<br/>

module 就是为了方便我们管理项目代码使用的，它是一个版本控制单元，是一系列相关包的集合表示。<br/>

使用 go module 管理依赖后会在项目根目录下生成两个文件 go.mod 和 go.sum。
go.mod 中会记录当前项目的所依赖, go.sum记录每个依赖库的版本和哈希值。


#### 开启gomod可用
可以使用环境变量GO111MODULE选择开启或者是关闭module模块的支持。有三个值可选:
* GO111MODULE=off, 关闭module功能, 到GOPATH中寻找依赖
* GO111MODULE=on, 代码不会到GOPATH中去寻找
* GO111MODULE=auto, go命令行根据当前目录来决定是否启用module, 当在GOPATH目录外且有go.mod文件时启用module


因为go mod是从github上拉取代码，可以设置代理进行加速
```
export GOPROXY="https://mirrors.aliyun.com/goproxy/" 
export GO111MODULE=on
```

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
| go mod vendor  | 将依赖复制到vendor下           |