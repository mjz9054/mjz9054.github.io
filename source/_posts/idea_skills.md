---
title: IntelliJ IDEA Skills
date: 2020-09-09 20:18:50
tags: [idea]
---

## 1. IDEA 剪切板
快捷键`command + shift + v`, 可以查看 idea 剪切板的近 100 条记录

## 2. 快速命名新建的变量
### 方式1： .val 或者 .var
在新创建的对象后面添加`.val` or `.var`，然后点击`Tab`或者`Command`，能够弹出新建变量的选项，有助于快速命名变量
![](/images/idea_skill_val.gif)

- 对于`.val`，在`Java`工程中，需要结合`lombok`使用；而在`kotlin`项目中，因为`kotlin`语言有`.val`来声明一个不会改变的变量，则会生成`val xx = xxx`形式的代码；
- 对于`.var`，在`Java`工程中，生成`对象 + 变量名`的形式；在`kotlin`中，则是`var xx = xxx`的形式。
- 总的来说，在`Java`工程中，`.var`更实用，而在`kotlin`工程中，`val`和`var`都比较实用，具体看想要声明的变量是否为可变化的，不可变，则使用`.val`，可变，则使用`.var`。

### 方式2：快捷键 
`option + command + v` ，
![](/images/idea_keymap_ocv.gif)

## 3. live template

## 4. 快速选择相同内容，并启动多区域编辑
当单个代码文件中有多个相同地方需要修改时，可以使用快捷键`control + command + g`
![](/images/idea_skill_same_text_edit.gif)

## 5. 将内容放在一行
当想把多行内容放在一行中显示时，可以使用快捷键 `control + shift + j`
![](/images/idea_skill_one_line.gif)

## 6. 打印变量时指定变量名称
在代码调试的时候，常会遇到打印出某个变量的场景，如果打印的时候不给变量起名字或者指定文本，在控制台不容易定位到打印的信息，而手动去写有时并不方便，此时可以使用`soutv`，然后按下`tab`，就会自动选择要打印的变量，并填写好前缀。
![](/images/idea_skill_print_variable.gif)

`soutv`其实是`IDEA`内置的一个`live tempalte`，通过添加自定义的 template ，可以提升编码的效率。

## 7. 快速定位到编译错误的位置
`F2` 定位到下一个错误

`Shift + F2` 定位到上一个错误

