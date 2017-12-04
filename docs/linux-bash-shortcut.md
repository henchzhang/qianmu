#Linux Bash 快捷键
> 本文适用于Mac OS以及大部分Linux发行版本
> 注意本文内所说的前、后分别是指行首、行尾方向

Linux、Mac OS操作系统，在其默认的命令行模式下（也就是Bash），有许多快捷键。熟悉常用的快捷键可以大大提高我们的操作速度，提升工作效率。按照命令的作用，大概可以分下面几种类型：

## 进程控制
* `Ctrl + c` 向当前进程发送一个`SIGINT`信号，通知进程退出。具体效果要看进程的程序如何处理SIGINT信号，有可能会有延迟，有可能甚至会被忽略。比如scrapy程序，按下`Ctrl + c`需要等当前的请求处理完毕后才会结束进程，如果想要强制立即退出，需要按下两次`Ctrl + c`
* `Ctrl + z` 向当前进程发送一个`SIGTSTP`信号，让进程转到后台执行，如果想恢复前台执行，可以使用`fg process_name`
* `Ctrl + d` 退出命令行

## 屏幕输出
* `Ctrl + l` 清除屏幕输出
* `Ctrl + s` 停止屏幕输出
* `Ctrl + q` 恢复屏幕输出

```js
有时候我们在输入命令的时候，不知道不小心按到了什么键，控制台“卡死”了，不管怎么操作都不动了。其实就是因为误按下了"ctrl + s"键，我们的输入仍然有效，仍然会执行，只是屏幕上没有反馈罢了。
```

## 移动光标
* `Ctrl + a` 移动到命令行首
* `Ctrl + e` 移动到命令行尾
* `Ctrl + f` 往前移动一个字符
* `Ctrl + b` 往后移动一个字符
* `Esc + f` 往前移动一个单词（不包含符号）
* `Esc + b` 往后移动一个单词（不包含符号）
* `Ctrl + xx` 在光标当前所处的位置和行首之间切换。

## 删除
* `Ctrl + d` 删除光标当前位置的字符
* `Ctrl + h` 删除光标前一个字，相当于Window键盘的Backspace或者Mac键盘的delete键

## 剪切与粘贴
* `Ctrl + k` 从光标当然位置剪切到行尾
* `Ctrl + u` 从光标当然位置剪切到行首
* `Ctrl + w` 从光标当前位置向前剪切整个单词（包含符号）
* `Esc + Backspace` 从当前位置向前剪切一个单词（不包含符号，Mac键盘为Esc + delete键）
	```bash
	scrapy crawl university -a max_num=500 -t csv -o u.csv    
	# 注意：假设此时光标500后面，按下 Ctrl + w 后会将 “max_num=500”都删除，如果只想删除到“=”符号之后，则按Esc + BackSpace
	```
	
* `Esc + d` 从光标当前位置向后剪切一个单词（不包含符号）
* `Ctrl + y` 将剪切板中的文本粘贴到当前光标之前

## 编辑
* `Ctrl + -` 撤销上一步操作（注意没有反撤销操作，至少目前为止还没发现）
* `Ctrl + t` 交换当前光标所处的字符与前一个字符
* `Esc + t` 交换当前光标所处的单词与前一个单词（不包含符号）
  ```bash
	scrapy crawl university -a max_num=500 -t csv -o u.csv    
	# 还是以scrapy命令为例，假设现在光标处理max_num中的"u"处，按下“Esc + t”后，max_num就会变成num_max

	```

## 修改大小写
* `Esc + u` 将光标所处位置往后一个单词变为大写
* `Esc + l` 将光标所处位置往后一个单词变为小写
* `Esc + c` 将光标所处位置的字符变为大写，并将往后一个单词变为小写


## 历史记录
* `history`可以查看所有命令的历史记录
```
该命令实际上相当于`cat ~/.bash_history`。大家可以看一下自己操作系统用户目录下的.bash_hitory文件，里面记录了命令执行的序号、时间、命令以及所有参数。
```

* `echo $HISTSIZE` 显示历史记录最大记录数量
```
HISTSIZE这个环境变量决定了历史记录的最大数量，我们可以通过修改它来修改.bash_history文件的最大行数
```
* `history -c` 清除所有的历史命令
* `Ctrl + p` 上一条命令
* `Ctrl + n` 
* `Ctrl + r` 进入历史记录逆向搜索模式
* `Esc + r` 撤消所有对当前历史记录命令的修改
* `Esc + .` 使用上一条命令的最后一个参数

# 命令缩写
除了以上列出的快捷键，bash还支持下面这些快捷命令
* `!!` 执行上一条命令
* `!command` 执行上一条以“command”开头的命令
* `^command` 删除上一条命令中的"command"并执行
* `^command1^command2` 将上一条命令中第一个"command1"替换为"command2"并执行
* `^command1^command2^` 将上一条命令中所有的"command1"替换为"command2"并执行
* `!$:p` 打印出上一条命令的最后一个参数，类似于上面介绍的"Esc + ."
* `!*:p` 打印出上一条命令的所有参数
```bash
:p 可以用在很多地方，表示将前面的命令只打印出来，不执行。比如：
	!!:p 打印出上一条命令
	!scrapy:p 打印出上一条以scrapy开头的命令
```

