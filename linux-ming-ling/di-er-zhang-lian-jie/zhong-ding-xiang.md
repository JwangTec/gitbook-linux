# 2. 重定向

## 重定向

1. 说明 : I/O 重定向。“I/O”代表输入/输出， 通过这个工具，你可以重定向命令的输入输出，命令的输入来自文件，而输出也存到文件。 也可以把多个命令连接起来组成一个强大的命令管道
2. 配合io使用的命令

   cat － 连接文件

   sort － 排序文本行

   uniq － 报道或省略重复行

   grep － 打印匹配行

   wc － 打印文件中换行符，字，和字节个数

   head － 输出文件第一部分

   tail - 输出文件最后一部分

3. 标准输入，输出，和错误

   > 与 Unix 主题“任何东西都是一个文件”保持一致，程序，比方说 ls，实际上把他们的运行结果 输送到一个叫做标准输出的特殊文件（经常用 stdout 表示），而它们的状态信息则送到另一个 叫做标准错误的文件（stderr）。默认情况下，标准输出和标准错误都连接到屏幕，而不是 保存到磁盘文件。除此之外，许多程序从一个叫做标准输入（stdin）的设备得到输入，默认情况下， 标准输入连接到键盘。
   >
   > I/O 重定向允许我们可以更改输出走向和输入来向。一般地，输出送到屏幕，输入来自键盘， 但是通过 I/O 重定向，我们可以改变输入输出方向。

4. 重定向标准输出

   使用 &gt; 把本来应该输出到屏幕上面的信息输出到文本上面

   ```text
    rimideiMac-10:ln_dir4 admin$ ls / > test1.txt
   rimideiMac-10:ln_dir4 admin$ let test1.txt
   ```

   但是 当我们得到一个错误的输出时候,这个时候程序就不会把信息写入文本

   ```text
    rimideiMac-10:ln_dir4 admin$ ls /bin/ac > test2
   ls: /bin/ac: No such file or directory
   ```

   重定向错误输出的话我们需要使用

   ```text
    rimideiMac-10:ln_dir4 admin$ ls /bin/ac 2> test2
   ```

   现在的bash给我们提供了一种方法 同时提供重定向错误和标准输出

   ```text
    rimideiMac-10:ln_dir4 admin$ ls /bin/ac &> test2
   ```

5. cat \(concatenate\)－ 连接文件

   cat 命令读取一个或多个文件，然后复制它们到标准输出，就像这样:

   ```text
    rimideiMac-10:ln_dir4 admin$ cat test1.txt 
    Applications
    Library
    Network
    System
    Users
    Volumes
    bin
    cores
    data
    dev
    etc
    home
    installer.failurerequests
    net
    private
    sbin
    tmp
    usr
    var
   ```

   | 参数 | 描述 |
   | :--- | :--- |
   | -n | 对输出的所有行编号,由 1 开始对所有输出的行数编号 |
   | -s | 有连续两行以上的空白行，就代换为一行的空白行 |

   > tac 将 cat 反写过来，所以它的功能就跟 cat 相反，cat 是由第一行到最后一行连续显示在屏幕上，而 tac 则是由最后一行到第一行反向在屏幕上显示出来

6. 管道线
7. 使用方式: 命令可以从标准输入读取数据，然后再把数据输送到标准输出，命令的这种能力被 一个 shell 特性所利用，这个特性叫做管道线。使用管道操作符”\|”（竖杠），一个命令的 标准输出可以管道到另一个命令的标准输入：

   ```text
    rimideiMac-10:ln_dir4 admin$ ls / |less
   ```

   > 把ls的标准输出管道到less的标准输入

   可以使用xargs 把输出的命令改成一行或者安装自己的指定行数打印

   ```text
    ls / | xargs
   ```

   ```text
    ls / | xargs -n 4
   ```

   > -n 每行打印多少个

8. 过滤器：

   管道线经常用来对数据完成复杂的操作。有可能会把几个命令放在一起组成一个管道线。 通常，以这种方式使用的命令被称为过滤器。过滤器接受输入，以某种方式改变它，然后 输出它。第一个我们想试验的过滤器是 sort。想象一下，我们想把目录/bin 和/usr/bin 中 的可执行程序都联合在一起，再把它们排序，然后浏览执行结果：

   ```text
    rimideiMac-10:ln_dir4 admin$ ls /bin/ /usr/bin/ | sort | less
   ```

   > 因为我们指定了两个目录（/bin 和/usr/bin），ls 命令的输出结果由有序列表组成， 各自针对一个目录。通过在管道线中包含 sort，我们改变输出数据，从而产生一个 有序列表。

9. uniq - 报道或忽略重复行

   uniq 命令经常和 sort 命令结合在一起使用。uniq 从标准输入或单个文件名参数接受数据有序 列表（详情查看 uniq 手册页），默认情况下，从数据列表中删除任何重复行。所以，为了确信 我们的列表中不包含重复句子（这是说，出现在目录/bin 和/usr/bin 中重名的程序），我们添加 uniq 到我们的管道线中：

   ```text
    rimideiMac-10:ln_dir4 admin$ ls /bin/ /usr/bin/ | sort |uniq | less
   ```

   > 在这个例子中，我们使用 uniq 从 sort 命令的输出结果中，来删除任何重复行

10. grep wc
    1. grep

       说明: grep 是个很强大的程序，用来找到文件中的匹配文本。

       比如说，我们想在我们的程序列表中，找到文件名中包含单词“zdiff”的所有文件。这样一个搜索， 可能让我们了解系统中的一些程序与文件压缩有关系。

       ```text
        rimideiMac-10:~ admin$ ls /bin/ /usr/bin/ | sort | grep zdiff |less
       ```

       ```text
        $ grep 'root' /etc/passwd
       ```

       > 将/etc/passwd 文件中出现 root 的行取出来
       >
       > ```text
       >  $ grep -v 'root' /etc/passwd
       > ```
       >
       > 将/etc/passwd 文件中未出现 root 的行取出来

    2. wc 统计的工具，主要用来显示文件所包含的行、字和字节数

       | 参数 | 描述 |
       | :--- | :--- |
       | -c | 统计字节数 |
       | -l | 统计行数 |
       | -m | 统计字符数，这个标志不能与 -c 标志一起使用 |
       | -w | 统计字数，一个字被定义为由空白、跳格或换行字符分隔的字符串 |
       | -l | 打印最长行的长度 |

       ```text
        canvasdeMBP:project canvas$ cat test.py | wc -c
       165847
       canvasdeMBP:project canvas$ cat test.py | wc -l
       1380
       canvasdeMBP:project canvas$ cat test.py | wc -m
       165847
       canvasdeMBP:project canvas$ cat test.py | wc -w
       12420
       canvasdeMBP:project canvas$ cat test.py | wc -m
       165847
       12420
       canvasdeMBP:project canvas$ cat test.py | wc -l
       ```
11. head / tail －打印文件开头部分/结尾部分

    说明:

    有时候你不需要一个命令的所有输出。可能你只想要前几行或者后几行的输出内容。 head 命令打印文件的前十行，而 tail 命令打印文件的后十行。默认情况下，两个命令 都打印十行文本，但是可以通过”-n”选项来调整命令打印的行数。

    它们也能用在管道线中：

    ```text
     rimideiMac-10:log admin$ head -n 5 fsck_hfs.log
     rimideiMac-10:log admin$ tail -n 5 fsck_hfs.log

     rimideiMac-10:log admin$ ls /usr/bin | tail -n 5
    ```

tail 有一个选项允许你实时的浏览文件。当观察日志文件的进展时，这很有用，因为 它们同时在被写入。

```text
    tail -f /var/log/system.log
```

## 高级键盘技巧

1. clear － 清空屏幕
2. history － 显示历史列表内容
3. ! 回顾历史命令
4. 表9-1: 光标移动命令

   | 按键 | 行动 |
   | :--- | :--- |
   | Ctrl-a | 移动光标到行首。 |
   | Ctrl-e | 移动光标到行尾。 |
   | Ctrl-f | 光标前移一个字符；和右箭头作用一样。 |
   | Ctrl-b | 光标后移一个字符；和左箭头作用一样。 |
   | Alt-f | 光标前移一个字。 |
   | Alt-b | 光标后移一个字。 |
   | Ctrl-l | 清空屏幕，移动光标到左上角。clear 命令完成同样的工作。 |

