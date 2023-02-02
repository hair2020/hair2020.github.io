# 如何把旧电脑改成服务器用


# 如何把旧电脑改成服务器用

[TOC]

## 任务

- [ ] 下载服务器系统。本次采用Ubuntu server LTS 20.04

- [ ] 制作系统U盘。本次采用rufus 3.17

- [ ] 安装系统

- [ ] 可从外网访问，本次采用cpolar内网穿透工具

## 一.下载

- 官网下载
- 上这[原版软件 (itellyou.cn)](https://next.itellyou.cn/Original/)

## 二.制作U盘

- win10系统中用rufus软件将下载的iso文件+U盘（能装的下系统的）制作成启动盘。

## 三.安装

1. 进入BIOS，我的老台式是F12 --> 设置启动方式为U盘
2. 语言选择，键盘布局，选择install Ubuntu
3. Network connections网络设置。若网线已插好，默认DHCP，并把已经获取到的IP显示到对应的网卡上。使用DHCP就直接光标选择Done。其他情况遇到再补充
4. Configure proxy设置代理服务器。一般不需要，默认为空，回车
5. Configure Ubuntu archive mirror 设置安装软件、更新源。本次采用[Index of /ubuntu](http://cn.archive.ubuntu.com/ubuntu/)
6. Filesystem setup磁盘分区，我新手直接选择Use An Entire Disk 回车。需要分区再补充。 显示分区情况，回车
7. 格式化 continue
8. Profile setup设置用户名，密码
9. SSH Setup 需要远程登陆选择安装，Import SSH identity 默认选 NO ，回车
10. Featured Server Snaps系统服务安装清单，直接Done，回车
11. 等待安装（我把安全更新跳过了
12. 设置密码sudo passwd root

## 四.配置ssh

1. ##### 检查是否安装ssh服务

   ```
   rpm -qa |grep ssh
   ```

   若未安装rpm则执行

   ```
   sudo apt-get install rpm
   ```

   安装ssh服务器

   ```
   sudo apt-get install openssh-server
   ```

   安装ssh客户端

   ```
   sudo apt-get install openssh-client
   ```

2. ##### 启动ssh服务

   ```
   sudo service ssh start
   ```

   或者

   ```
   sudo service ssh restart
   ```

3. ##### 查看版本

   ```
   ssh -V
   ```

## 五.内网连接

1. ##### win10系统，安装SecureCRT

2. ##### 查看服务器ip

   ```
   ipconfig
   ```

   inet后边的ip地址

3. ##### 打开SecureCRT

​	{{< figure src="/images/djfwq/djfwq1.png">}}

​	{{< figure src="/images/djfwq/djfwq2.png">}}

​	{{< figure src="/images/djfwq/djfwq3.png">}}

完事

## 六.外网连接

1. ##### 从五-2开始（已获得服务器ip

2. ##### 国内（China）安装cpolar

   ```
   curl -L https://www.cpolar.com/static/downloads/install-release-cpolar.sh | sudo bash
   
   ```

   查看版本

   ```
   cpolar version
   ```

   [cpolar官网](https://www.cpolar.com/)注册并登陆后台获取[认证token](https://dashboard.cpolar.com/auth)

   认证

   ```
   cpolar authtoken xxxxxxxxxxxxxxxxxx
   ```

   配置cpolar服务开机自启动

   ```
   sudo systemctl enable cpolar
   ```

   守护进程方式，启动cpolar

   ```
   sudo systemctl start cpolar
   ```

   查看守护进程状态

   ```
   sudo systemctl status cpolar
   ```

3. ##### 查看映射到公网的隧道地址

   登录cpolar后台–>[状态](https://dashboard.cpolar.com/status)，查看一下ssh隧道映射的公网地址：

   {{< figure src="/images/djfwq/djfwq4.png">}}

​		看五-3，

​		主机名：蓝线

​		端口：黄线

## 七.参考文档

[https://www.cpolar.com/blog/how-to-remotely-access-the-raspberry-pi-at-home-with-ssh]

[Ubuntu 20.04 LTS (Focal Fossa) Server Installation Guide (linuxtechi.com)](https://www.linuxtechi.com/ubuntu-20-04-lts-server-installation-guide/)

还有呢 忘了...
