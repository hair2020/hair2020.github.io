# 写的小玩意


## go

- ### 打麻将投骰子模拟器1.0

  main.go

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main()  {
	fmt.Println("欢迎使用麻将投骰子模拟器，第一次投色子的人为1号，逆时针依次编号。")
	GenerateNumber(2,12,4)
}

// 最小值，最大值，麻将人数
func GenerateNumber(min int, max int,population int){
	rand.Seed(time.Now().Unix())
	// 第一次投骰子
	tNum0 := rand.Intn(max + 1 - min) + min
	// 选出第二家
	tPeo := tNum0 % population
	if tPeo == 0 {
		fmt.Printf("第一次骰子结果是：第%d号投 \n",population - 1)
	}else {
		fmt.Printf("第一次骰子结果是：第%d号投 \n",tPeo)
	}

	// 再投，出结果
	tNum1 := rand.Intn(max + 1 - min) + min
	sumD := tNum0 + tNum1
	fmt.Printf("两次总和是%d\n",sumD)
}
	
```

## Python

- ### 视频下载器

  知乎文章魔改+封装you-get得叙利亚风格程序界面

  ！下载B站视频时只以BV结尾是不行的，换成av格式结尾就行了。

  无效格式：`https://www.bilibili.com/video/BV1D5411Z7Mr`

  有效格式：`https://www.bilibili.com/video/BV1D5411Z7Mr?spm_id_from=333.851.b_7265636f6d6d656e64.2`

  
  
  好在bv转av的算法已经被大佬逆向出来了
  
  ##### BV转AV的算法

```python
table='fZodR9XQDSUm21yCkr6zBqiveYah8bt4xsWpHnJE7jL5VG3guMTKNPAwcF'
tr={}
for i in range(58):
	tr[table[i]]=i
s=[11,10,3,8,4,6]
xor=177451812
add=8728348608

def dec(x):
	r=0
	for i in range(6):
		r+=tr[x[s[i]]]*58**i
	return "av"+str((r-add)^xor)
```

##### 自动转av并下载的程序（没有写GUI

```python
# -*- coding = utf -8 -*-
# @Time : 2022/2/19 11:17
# @Author : hair
# -*- coding = utf -8 -*-
import subprocess
import bvToAv
import os


# https://www.bilibili.com/video/
# BV13x411o72x
def getBv(bv):
	return bvToAv.dec(bv)


def Command(videoUrl, outFile, playlist):
	if playlist == None:
		playlist = ""
	cmds = f"you-get {playlist} -o {outFile} {videoUrl}"
	print(cmds)
	p = subprocess.Popen(cmds, shell=True, stdout=subprocess.PIPE, stderr=subprocess.STDOUT, encoding="utf-8")
	for l in iter(p.stdout.readline,b''):
		print(l)

def genUrl(ori):
	tl = ori.split("/BV")
	oriUrl = tl[0]
	bv = "BV"+ tl[1].split("?")[0]
	av = bvToAv.dec(bv)
	return oriUrl + "/" + av

def main():
	yuan = input("1.bilibili \n2. 其他\n输入数字选择视频源：")
	outFile = input("输入下载路径：")
	if yuan == "1":
		videoUrl = input("输入视频连接：")
		videoUrl = genUrl(videoUrl)
		playlist = input("是否批量下载,输入1 是 2 否")
		if playlist == "1":
			Command(videoUrl, outFile, "--playlist")
		else:
			Command(videoUrl, outFile, None)
	else:
		pass

	
if __name__ == '__main__':
    main()
```

##### 小改叙利亚GUI源码

```python
# -*- coding = utf -8 -*-
# @Time : 2022/2/19 11:17
# @Author : hair
from tkinter import *
import tkinter.messagebox
from tkinter import filedialog
from tkinter.scrolledtext import ScrolledText
import subprocess as sub
import threading
import os
import subprocess
import bvToAv
#为避免在下载时tkinter界面卡死，创建线程函数
def thread_it(func, *args):
    # 创建
    t = threading.Thread(target=func, args=args)
    # 守护
    t.setDaemon(True)
    # 启动
    t.start()

#浏览本地文件夹，选择保存位置
def browse_folder():
    #浏览选择本地文件夹
    save_address = filedialog.askdirectory()
    #把获得路径，插入保存地址输入框（即插入input_save_address输入框）
    input_save_address.insert(0,save_address)

def download():
	videoUrl = input_url.get()
	playlist = flag01.get()
	if playlist == "0":
		playlist = ""
	else:
		playlist = "--playlist"
	outFile = input_save_address.get()
	cmds = f"you-get {playlist} -o {outFile} {videoUrl}"
	print(cmds)
	input_url.delete(0, END)
	input_save_address.delete(0, END)
	flag01.delete(0,END)

	p = subprocess.Popen(cmds, shell=True, stdout=subprocess.PIPE, stderr=subprocess.STDOUT, encoding="utf-8")
	for line in iter(p.stdout.readline, b''):
		stext.insert(END, line)
		stext.yview_moveto(1)
		if not sub.Popen.poll(p) is None:
			if line == "":
				break
	p.stdout.close()

if __name__ == '__main__':
	top = Tk()
	top.title("头发视频下载器")
	path1=os.path.dirname(os.path.abspath(__file__))
	# print(path1)
	# print(os.environ["Path"])
	os.environ["PATH"] += os.pathsep + path1
	# print(os.environ["Path"])

	#获取屏幕尺寸以计算布局参数，使窗口居屏幕中央,其中width和height为界面宽和高
	width=700
	height=700
	screenwidth = top.winfo_screenwidth()
	screenheight = top.winfo_screenheight()
	alignstr = '%dx%d+%d+%d' % (width, height, (screenwidth-width)/2, (screenheight-height)/2)
	top.geometry(alignstr)

	#阻止窗口调整大小
	top.resizable(0,0)

	#框架布局
	frame_root=Frame(top)
	frame_left=Frame(frame_root)
	frame_left.pack(side=LEFT)
	# frame_right.pack(side=RIGHT,anchor=N)
	frame_root.pack()

	#输入视频链接
	tip1= Label(frame_left, text='请输入视频链接：         ',font = ('楷体',20))
	tip1.pack(padx=10,anchor=W)
	#视频链接输入框
	input_url= Entry(frame_left,bg='#F7F3EC')
	input_url.pack(ipadx=159,ipady=8,padx=20,anchor=W)
	#是否下载全部框
	tipf=Label(frame_left, text='是否下载全部(输入0,1，1代表是） ',font = ('楷体',20))
	tipf.pack(padx=10,anchor=W)
	flag01= Entry(frame_left,bg='#F7F3EC')
	flag01.pack(ipadx=159,ipady=8,padx=20,anchor=W)
	#请选择保存位置：
	tip2=Label(frame_left, text='请选择保存位置(必填！)：  ',font = ('楷体',20))
	tip2.pack(padx=10,anchor=W)
	#保存地址输入框
	input_save_address= Entry(frame_left,bg='#F7F3EC')
	input_save_address.pack(ipadx=159,ipady=8,padx=20,anchor=W)

	# “浏览文件夹”按钮
	browse_folder_button = Button(top, text='浏览',font = ('楷体',15),bg="green",command=lambda :thread_it(browse_folder))
	browse_folder_button.place(relx=0.86,rely=0.25,anchor="nw")

	# “下载”按钮
	download_button = Button(frame_left, text='下载',font = ('楷体',15),command=lambda :thread_it(download))
	download_button.pack( padx=20,pady=20,anchor=W)

	# ScrolledText组件（滚动文本框）
	stext = ScrolledText(frame_left, width=60, height=23, background='#F7F3EC')
	stext.pack(padx=20,anchor=W)

	top.mainloop()

```


