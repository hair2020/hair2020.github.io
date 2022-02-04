# GRPC_Strat

## 0.介绍
 备忘，不涉及技术

## 1 proto文件

### 1.1 项目结构

​	{{< figure src="/images/grpc/xmjg0.png">}}

### 1.2 proto

在proto文件夹下新建xxx.proto文件，vscode会提示有插件，安装前俩即可

```ini
// 说明使用proto3语法
syntax = "proto3";
// ；之前：生成文件在那个目录中。 之后：包名
option go_package = "../pb;processor_message";
```

### 1.3 serve

1. 取出server
2. 挂载方法
3. 注册服务
4. 创建监听

### 1.4 client

1. 创建一个连接
2. new 一个client
3. 调用client方法
4. 获取返回值

## 环境配置

### .0

go环境OK

### .1 gRPC

安装gPRC核心库（网络可能不行，设置代理或者去科学或者）

`go get google.golang.org/grpc`

### .2 protocol buffer

安装protocol编译器

win64版：下载--解压--将bin目录添加环境变量

测试：`protoc`

下载地址：[Releases · protocolbuffers/protobuf (github.com)](https://github.com/protocolbuffers/protobuf/releases)

### .3 protoc-gen-go

golang语言的代码生成工具

有个小小的坑，`github.com/golang/protobuf/protoc-gen-go`和`google.golang.org/protobuf/cmd/protoc-gen-go`是不同的。

版本不同，命令不同。我采用Google接管的版本。

`go install google.golang.org/protobuf/cmd/protoc-gen-go`
`go install google.golang.org/grpc/cmd/protoc-gen-go-grpc`

安装gRPC时已经下载下来了，因此用`install`命令，不用`get`



## 参考连接

[Quick start | Go | gRPC](https://www.grpc.io/docs/languages/go/quickstart/)

[gRPC-go 入门（1）：Hello World - 红鸡菌 - 博客园 (cnblogs.com)](https://www.cnblogs.com/hongjijun/p/13724738.html)

