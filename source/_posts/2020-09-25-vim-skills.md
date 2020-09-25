---
title: Vim Skills
date: 2020-09-25 11:12:02
tags:
---

虽然现在有很多优秀的文本编辑器，但在一些时候还是会用到`Vim`，比如`Termial`或者`iTerm`里，由于并不是一个`Vim`的熟手，经常会遇到知道某功能但想不起来具体指令的时候。

这里并没有囊括所有的指令或者完整的`Vim`使用技巧，而是做一下简单记录，方便用到的时候查找。

### Vim 键盘图
![](https://www.runoob.com/wp-content/uploads/2015/10/vi-vim-cheat-sheet-sch.gif)

### Command

| 功能 | 命令 | 备注 |
| --- | --- | --- |
| 复制当前行 | yy | 
| 删除当前行 | dd |
| 删除当前行向后n行 | ndd | 包括当前行 | 
| 删除当前行至最后一行 | dG |
| 删除当前行至第一行 | d1G |
| 向前删除一个字符 | X | 类似 backspace |  
| 向后删除一个字符 | x | 类似 del |
| 先后删除n个字符 | nX | 
| 粘贴至当前行的上一行 | P | 
| 粘贴至当前行的下一行 | p | 
| 重复前一个动作 | . | 
| 重做上一个动作 | Ctrl + r |
| 撤销 | u |
| 行首 | 0 | 或者 Home |
| 行尾 | $ | 或者 End | 
| 首行 | gg | 或者1G | 
| 最后一行 | G |
| 屏幕中央的一行 | M |
| 第 n 行 | nG |
| 向下移动n行 | n + Enter |
| 下一页 | Ctrl + f |
| 上一页 | Ctrl + b |
| 向下半页 | Ctrl + d |
| 向上半页 | Ctrl + u |
| 向下搜索 | /word | word 为搜索的内容 | 
| 想前搜索 | ?word |
| 下一个搜索结果 | n |
| 上一个搜索结果 | N |
| 合并当前行和下一行为一行 | J | 
| 保存并退出 | ZZ | 
| 不保存退出 | ZQ |
| 显示行号 | :set nu | 
| 取消显示行号 | :set nonu | 


参考：[Linux vi/vim](https://www.runoob.com/linux/linux-vim.html)