---
title: 用PyQT实现的BadUSB脚本编写器之闲聊
tags:
  - 工具
  - 手册
  - Python
  - PyQT
categories: python
cover: 'https://s3.ax1x.com/2020/12/09/r96Haj.jpg'
abbrlink: 3888dc4f
date: 2020-12-08 18:53:00
---
# introduce
\# =========文章废话比较多============= (pyqt式提示线)
项目地址：https://github.com/hensir/QtTest
这个存储库里实际是有三个项目的
badusb是主角的文件夹
pyb7是 为脚本攻击磐云设备 型号PY—B7 混战第二题的工具 不过只画了一个界面 
qq 是一个发送邮件的工具 (手动滑稽)

当然大多数工具的存在都是为了复习 严格来说我是从8月29就开始学习PyQT了
但其实9月上旬我都还在参加我们学校主办的那个网络安全比赛
不过距今学到了232页 我个人是挺满意的 

# 主界面
[![r9yCXF.jpg](https://s3.ax1x.com/2020/12/09/r9yCXF.jpg)](https://imgchr.com/i/r9yCXF)
一眼望去最明显的 咱先不说
从对象观察器最外边看 有两个 有一个状态栏 另一个工具栏
前者目前做了这个 按钮点击或按下的状态提示
后者的多是操作这个 TextEdit文本编辑框 复制 剪切 放大啥的 都是它内建的槽函数 
可能值得一嘴的是 那个字体action 是调用了一个标准的字体选择对话框
## groupBox
好，首(False)先登场的是 我们的DuckySpark 转DigiSpark按钮
这个按钮就是和它的名字一样 用来把 算了 别再人类本质了
代码实现我用的现成的 没错我就是代码的搬运工 Ctrl V的信仰者（滑稽）
大佬的项目地址：https://github.com/toxydose/Duckyspark
大佬的脚本用法是这样的
python3 Duckyspark_translator.py [payload.txt] [output_file]
或者
python3 Duckyspark_translator.py [payload.txt]
这样的  
我啪的拍了一下脑门 很快嗷 欸，原来，大佬的脚本是从终端接收参数执行的
之后我来了一套接化发 把大佬的脚本 改成了一个函数
接收一个str 返回一个str
然后又来了一个按钮 可能是个英国带力士 叫预览代码
嘿嘿 这个我还没实现 功能就是 用python运行TextEdit编辑框中所编写的脚本
初步思路是 就是上面那个DTD函数一样 就做一个replace呗
替换为那个叫pywin32库能执行的语句
## groupBox_2
组名叫INPUT All In One 她里面东西不少 花里胡哨的 反正我挺舒服的
bulingbuling两个瘟都死风格的 大 按钮  也不短对吧
左边那个最后再讲 右边那个也是 在做了在做了 
[![r9yplT.jpg](https://s3.ax1x.com/2020/12/09/r9yplT.jpg)](https://imgchr.com/i/r9yplT)
接下来是 按键识别输入 这一套功能是这个项目逻辑最多的了
讲一下实现的动作 功能有 这个lineedit可以直接接收不可打印字符的显示
也就是 我按个 Ctrl+Alt+A 上面就直接显示了 当然底层的还不行
就是那个 win(meta)+E win+R 。。。。。这些 都会直接显示瘟都死的功能
然后我的lineedit就接不到快捷键了 
                后来             
我以我小学三年级英语基础发现了designer里居然有那个 
叫KeySequenceEdit的组件 我开始方了 按键 序列 编辑器
！我傻了 我写了那么久的lineedit就被你一个小小小小小小小小小小小小小小小小小小小小小组件
给替掉了吗 我hyh 从这跳下去也不会用这个KSE 欸 Is so yummy
我尝试了几把 嗯？ 说鸡不说@F(H#BJF()J@JKSDL)PL:K""
文明你J<$#L&K%*H)&OGjh'asjd 
感觉还 中 吧 也都那样了 都比我的LE(LineEdit)多了 一个功能1.5秒后停止接收按键 并显示结果
说这话不是贬低它的 而是它天美的也不能接收 瘟都死的全局快捷键 得。  拜拜还是
然后是 右边这个当前文本“单击”的comboBox 当这个cB中的项目被激活后会进入相应槽函数
点一下 玩一年  单击按钮就是那个stroke，press和release 换项目后 会清空LE
stroke没啥 press只能输入一个按键 而这个release 就更厉害了
它是直接预定好的一个 “0” 就是头文件指定的松开方式嘛
打印字符串 没得说    接着是 Sleep步长是100
好了 该说说我们的KeyDialog了  这个对话框花了我不少时间 也学到了好多东西
[![r9y96U.jpg](https://s3.ax1x.com/2020/12/09/r9y96U.jpg)](https://imgchr.com/i/r9y96U)
里面有 3个组合框 24个按钮和三个单选按钮
首先是  按钮太多 所以用了findchildren 循环遍历的连接了信号
很快啊 3个cB也是这样做的 至于传送的是什么数值 嘿嘿
是按钮的名字 我没写常量表 反正按钮名字也方便 同时也学到了sender()
[![r9yim4.jpg](https://s3.ax1x.com/2020/12/09/r9yim4.jpg)](https://imgchr.com/i/r9yim4)
然后是其它按键 到底如何实现这个其它按键 我想了以下两种方法
一。删除整个KeyDialog的组件 然后循环遍历生成按钮
二。在原来的KeyDilog上向右扩展按钮 
其次再次点击 其他按键 会把界面返回到原来的样子
啊这 第一种方法好像不太适合我们的 其次
主要这个 二 我已经画好了 不想删
还原界面原来的样子 用的是 隐藏右边的布局
还有这个对整个窗体进行adjustsize

## groupBox_3
好家伙 组名 Ctrl+V 这么大一闪亮按键组合 组成了我多少代码
四个按钮 上面都有tooltip 就是那个你懂的
项目地址：https://github.com/CedArctic/DigiSpark-Scripts


说句实话 各位可能没看到这个define功能的实现
没错 我还真没写 哈哈哈哈哈哈-


