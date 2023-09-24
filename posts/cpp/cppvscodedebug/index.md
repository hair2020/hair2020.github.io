# cppVscodeDebug


### 出问题时的配置

数据结构的源码是GBK编码，vscode右下角可以改文件编码为GBK

vscode终端选择powershell: `Ctrl+Shift+p` search `Select Deafult profile `

输入`chcp`查看编码：`活动代码页: 936`

### 按教程进行调试

[VS Code之C/C++程序的调试(Debug)功能简介](https://zhuanlan.zhihu.com/p/85273055)

### 问题出现

调试时终端是cppdbg
​{{< figure src="/images/cppVscodeDebug/0.png">}}

试了改注册表，将`计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor`中的`autorun`的值改为`936`（gbk）

然而在调试运行时，他原因不明的自动改为了`65001`（utf-8）编码，导致原先被GBK编译的文件出现乱码。

### 解决

看到了这边文章[Windows控制台中文乱码问题测试、分析与解决 ](https://www.freesion.com/article/61141178992/)

in the cpp file, add 

```c
#include "windows.h"
int main() {
	SetConsoleOutputCP(936); # change the encode what you want
    
}
```

Problem solved.
