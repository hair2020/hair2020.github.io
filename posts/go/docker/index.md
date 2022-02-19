# Docker

## 虚拟机爬吧
## 等我用用再来写
## 安装问题

- win10 已开启hyper-v所有服务

  打开报错：

  `System.InvalidOperationExceptionshell`

  `Failed to set version to docker-desktop: exit code: -1windows`

  解决：

  [Windows 10 Docker InvalidOperationException Failed to set version to docker-desktop: exit code: -1 - 尚码园 (shangmayuan.com)](https://www.shangmayuan.com/a/67b6aead43c5494d91ee2f8f.html)

  临时方案：cmd/shell下执行：`netsh winsock reset`

  重启docker

  永久方案：...
