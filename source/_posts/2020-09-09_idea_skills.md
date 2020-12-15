---
title: IntelliJ IDEA Skills
date: 2020-09-09 20:18:50
tags: [idea]
---

记录下在使用`IDEA`时，常用或者觉得比较有用的操作技巧，便于后期的回顾和查阅。

<!--more-->

## 1. IDEA 剪切板
快捷键`command + shift + v`, 可以查看 idea 剪切板的近 100 条记录

## 2. 快速命名新建的变量
### 方式1： `.val` 或者 `.var`
在新创建的对象后面添加`.val` or `.var`，然后点击`Tab`或者`Command`，能够弹出新建变量的选项，有助于快速命名变量
![](/images/idea/idea_skill_val.gif)

对于`.val`，在`Java`工程中，需要结合`lombok`使用；而在`kotlin`项目中，因为`kotlin`语言有`.val`来声明一个不会改变的变量，则会生成`val xx = xxx`形式的代码；

对于`.var`，在`Java`工程中，生成`对象 + 变量名`的形式；在`kotlin`中，则是`var xx = xxx`的形式。

总的来说，在`Java`工程中，`.var`更实用，而在`kotlin`工程中，`val`和`var`都比较实用，具体看想要声明的变量是否为可变化的，不可变，则使用`.val`，可变，则使用`.var`。

### 3. 方式2：快捷键 
`option + command + v` ，
![](/images/idea/idea_skill_keymap_ocv.gif)

## 4. Live Templates
`IDEA`的`Live Templates`可以快速生成指定模板的代码。`IDEA`已经内置了一些 template，例如 参数的打印，参数是否为空的判断等，通过对应输入对应的缩写（abbreviation）,然后`Enter`或者`Tab`来生成所需的代码。

#### 打印参数
![](/images/idea/idea_skill_live_templates_soutv.gif)

#### 判读参数是否为空
![](/images/idea/idea_skill_live_templates_ifn.gif)

#### 判读参数是否不为空
![](/images/idea/idea_skill_live_templates_inn.gif)

除了 IDEA 自带的 Templates，用户还可以进行自定义。

## 5. 快速选择相同内容，并启动多区域编辑
当单个代码文件中有多个相同地方需要修改时，可以使用快捷键`control + command + g`
![](/images/idea/idea_skill_same_text_edit.gif)

## 6. 将内容放在一行
当想把多行内容放在一行中显示时，可以使用快捷键 `control + shift + j`
![](/images/idea/idea_skill_one_line.gif)

## 7. 打印变量时指定变量名称
在代码调试的时候，常会遇到打印出某个变量的场景，如果打印的时候不给变量起名字或者指定文本，在控制台不容易定位到打印的信息，而手动去写有时并不方便，此时可以使用`soutv`，然后按下`tab`，就会自动选择要打印的变量，并填写好前缀。
![](/images/idea/idea_skill_print_variable.gif)

`soutv`其实是`IDEA`内置的一个`live tempalte`，通过添加自定义的 template ，可以提升编码的效率。

## 8. 快速定位到编译错误的位置
`F2` 定位到下一个错误

`Shift + F2` 定位到上一个错误

## 9. 移动光标到文本开头
`fn + command + ←`

对应`IDEA`里的操作：`Move Caret to Text Start`

在`IDEA`里，Mac系统级别的移动至文本开头`Command + ↑`和结尾`Command + ↓`被指定给了其他操作。

## 10. 移动光标到文本结尾
`fn + command + →`

对应`IDEA`里的操作：`Move Caret to Text End`

## 11. 每次仅 run 单个单元测试case
当 idea 里打开的是一个 gradle 项目时，默认在run tests 时，使用的是 gradle，这个时候它不能通过点击 idea 侧边的run按钮来仅run当前的case，每次会将当前单元测试类里的所有case都跑一遍。
在 `Preferences` -> `Build,Execution,Deployment` -> `Build Tools` -> `Gradle` -> `Run tests using` 将其改为 `IntelliJ IDEA`，就能够 run 某个 case。

![](/images/idea/idea_skill_run_single_unit_test_case.png)

也可以选择 `Choose per test`, 启用后，在每次run时会提示选择用那种方式去run当前的case。

---
# IDEA 使用分享

### Find in actions

- find shortcuts
    - About
    - Reformat code
    - Rename 
    - Update Project
    - Commit
    - Recent Tests
    - ...
- find settings

### Useful Actions
| action | shortcut | note |
| - | - | - |
| Project | Command + 1 | Show/hide project window | 
| Paste from history | Shift + Command + V | clipboard |
| Split Horizontally | - | - |
| Split Vertically | - | - |
| Split and move donw | - | - |
| Split and move left | - | - |
| Start New Line | Shift + Command + Enter |
| Start New Line Before Current Line | Option + Command + Enter | 
| Collapse |
| Jump to Source | F4 / Command + Down / Commant + left click |
| Open Blank Diff Window | - | Compare different files | 
| Complate Current Statement | Shift + Command + Enter | complete `;` `,`...|
| Column Selection Mode | Shift + Command + 8 | for multiple lines edit |
| Select All Occurrences | Control + Command + G | Select all occurrences and edit |

#### Find/Location
| action | shortcut | note |
| - | - | - |
| Search anywhere | Double Shift | popup searh window | 
| Find in path | Shift + Command + F | find something by keyword in different path |
| Find classes | Command + O | all classes |
| Find files | Shift + Command + O | all files |
| Find symbols | Optin + Command + O | files/method/variable |


#### Navigation
| action | shortcut | note |
| - | - | - |
| Next Method | - | 
| Previous Method | - | 
| Super Method | 
| File Structure | Command + F12 | display members like variables and methods in the file |
| Line/Column | Command + L | go to the specific location of file | 
| Last Edit Location | Shift + Command + Backspace | - |
| Recent Files / Recent Changed Files  | Command + E |
| Recent Locations / Recent Changeds Locations | Shift + Command + E |
| Back | Command + [ / Option + Shift + Left | back to last caret Location |
| Forward | Command + ] /  Option + Shift + Right | Forwart to next caret Location | 
| Next Highlight Error | F2 | 
| Previous Highlight Error | Shift + F2 |


#### Git
| action | shortcut | note |
| - | - | - |
| Update Project | Command + T | pull |
| Commit changes | Command + K | display the changed files and commit |
| Push Commits | Shift + Command + K | diaplay the commits and push |
| Stash Changes | - | Stash Changes |
| Unstash Changes | - | Unstash Changes | 
| Show history | - | - |
| Local history | - | - |


#### Refactoring
| action | shortcut | note |
| - | - | - |
| Rename | 
| Extract Method | Option + Command + M |
| Extract Variable | Option + Command + V |
| Extract Constant | Option + Commmand + C |
| Extract Parameter | Option + Command + P / .val / .var |

#### live template
#### open http requests collection