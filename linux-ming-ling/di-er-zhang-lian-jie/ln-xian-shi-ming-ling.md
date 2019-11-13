# 1. ln文件链接

## ln 文件链接 （硬链接\|硬链接）

1. 硬链接

   ```text
    $ ln file link
   ```

硬链接和符号链接比起来，硬链接是最初 Unix 创建链接的方式，而符号链接更加现代。 在默认情况下，每个文件有一个硬链接，这个硬链接给文件起名字。当我们创建一个 硬链接以后，就为文件创建了一个额外的目录条目

硬链接有两个重要局限性：

1. 一个硬链接不能关联它所在文件系统之外的文件。这是说一个链接不能关联 与链接本身不在同一个磁盘分区上的文件。
2. 一个硬链接不能关联一个目录

> 一个硬链接和文件本身没有什么区别

1. 符号链接

   ```text
    $ ln -s file link
   ```

创建符号链接是为了克服硬链接的局限性。符号链接生效，是通过创建一个 特殊类型的文件，这个文件包含一个关联文件或目录的文本指针。

1. 链接实战

> 链接文件

```text
    ln -s  file2 ln_file2
```

> 链接文件夹

```text
    ln -s dir4 ln_dir4
    cd ln_dir4
```

## 显示命令

1. 概览:
   1. type – 说明怎样解释一个命令名
   2. which – 显示会执行哪个可执行程序
   3. man – 显示命令手册页
   4. apropos – 显示一系列适合的命令
   5. info – 显示命令 info
   6. whatis – 显示一个命令的简洁描述
   7. alias – 创建命令别名
2. 到底什么是命令
   1. 是一个可执行程序，就像我们所看到的位于目录/usr/bin 中的文件一样。 属于这一类的程序，可以编译成二进制文件，诸如用 C 和 C++语言写成的程序, 也可以是由脚本语言写成的程序，比如说 shell，perl，python，ruby，等等
   2. 是一个内建于 shell 自身的命令。bash 支持若干命令，内部叫做 shell 内部命令 \(builtins\)。例如，cd 命令，就是一个 shell 内部命令。
   3. 是一个 shell 函数。这些是小规模的 shell 脚本，它们混合到环境变量中。
   4. 是一个命令别名。我们可以定义自己的命令，建立在其它命令之上。
3. type－显示命令的类型

   说明: type 命令是 shell 内部命令，它会显示命令的类别，给出一个特定的命令名（做为参数）。

   \`\`\` $ type cd

   cd is a shell builtin

   $ type ls ls is hashed \(/bin/ls\)

```text
4. 定位

    1. which － 显示一个可执行程序的位置

        在 PATH 变量指定的路径中搜索可执行文件的所在位置。它一般用来确认系统中是否安装了指定的软件。

        说明:有时候在一个操作系统中，不只安装了可执行程序的一个版本。然而在桌面系统中，这并不普遍， 但在大型服务器中，却很平常。为了确定所给定的执行程序的准确位置，使用 which 命令
```

```text
    rimideiMac-10:ln_dir4 admin$ which ls
    /bin/ls

    ```

    > (某些系统中)这个命令只对可执行程序有效，不包括内部命令和命令别名，别名是真正的可执行程序的替代物

2. whereis 命令

    whereis 命令主要用于定位可执行文件、源代码文件、帮助文件在文件系统中的位置。whereis 命令还具有搜索源代码、指定备用搜索路径和搜索不寻常项的能力。

    whereis 命令查找速度非常快，这是因为它根本不是在磁盘中漫无目的乱找，而是在一个数据库中（/var/lib/mlocate/）查询。这个数据库是 Linux 系统自动创建的，包含有本地所有文件的信息，并且每天通过自动执行 updatedb 命令更新一次。也正是因为这个数据库要每天才更新一次，就会使得 whereis 命令的搜索结果有时候会不准确，比如刚添加的文件可能搜不到。

3. locate 

    locate 命令跟 whereis 命令类似，且它们使用的是相同的数据库。但 whereis 命令只能搜索可执行文件、联机帮助文件和源代码文件，如果要获得更全面的搜索结果，可以使用 locate 命令。
```

1. help 帮助文档

   ```text
    rimideiMac-10:ln_dir4 admin$ help cd
    cd: cd [-L|-P] [dir]
        Change the current directory to DIR.  The variable $HOME is the
        default DIR.  The variable CDPATH defines the search path for
        the directory containing DIR.  Alternative directory names in CDPATH
        are separated by a colon (:).  A null directory name is the same as
        the current directory, i.e. `.'.  If DIR begins with a slash (/),
        then CDPATH is not used.  If the directory is not found, and the
        shell option `cdable_vars' is set, then try the word as a variable
        name.  If that variable has a value, then cd to the value of that
        variable.  The -P option says to use the physical directory structure
        instead of following symbolic links; the -L option forces symbolic links
        to be followed.
   ```

   > 注意表示法：出现在命令语法说明中的方括号，表示可选的项目。一个竖杠字符 表示互斥选项。 这种表示法说明，cd 命令可能有一个”-L”选项或者”-P”选项，进一步，可能有参数“dir”

   1. 许多可执行程序支持一个”—help”\|-h选项，这个选项是显示命令所支持的语法和选项说明

      ```text
           rimideiMac-10:ln_dir4 admin$ python --help
           usage: python [option] ... [-c cmd | -m mod | file | -] [arg] ...
           Options and arguments (and corresponding environment variables):
           -b     : issue warnings about str(bytes_instance), str(bytearray_instance)
                    and comparing bytes/bytearray with str. (-bb: issue errors)
           -B     : don't write .pyc files on import; also PYTHONDONTWRITEBYTECODE=x
           -c cmd : program passed in as string (terminates option list)
           -d     : debug output from parser; also PYTHONDEBUG=x
           -E     : ignore PYTHON* environment variables (such as PYTHONPATH)
           -h     : print this help message and exit (also --help)
           -i     : inspect interactively after running script; forces a prompt even
                    if stdin does not appear to be a terminal; also PYTHONINSPECT=x
           -I     : isolate Python from the user's environment (implies -E and -s)
           -m mod : run library module as a script (terminates option list)
           -O     : remove assert and __debug__-dependent statements; add .opt-1 before
                    .pyc extension; also PYTHONOPTIMIZE=x
           -OO    : do -O changes and also discard docstrings; add .opt-2 before
                    .pyc extension
           -q     : don't print version and copyright messages on interactive startup
           -s     : don't add user site directory to sys.path; also PYTHONNOUSERSITE
           -S     : don't imply 'import site' on initialization
      ```

   2. 一些程序不支持”—help”选项

      ```text
       rimideiMac-10:ln_dir4 admin$ ls --help
      ls: illegal option -- -
      usage: ls [-ABCFGHLOPRSTUWabcdefghiklmnopqrstuwx1] [file ...]
      ```

2. man －显示程序手册页

```text
    rimideiMac-10:ln_dir4 admin$ man ls
```

> 手册文档的格式有点不同，一般地包含一个标题，命令语法的纲要，命令用途的说明， 和命令选项列表，及每个选项的说明。然而，通常手册文档并不包含实例，它打算 作为一本参考手册，而不是教材。

1. apropos

   ```text
    rimideiMac-10:ln_dir4 admin$ apropos mkdir
    mkdir(1)                 - make directories
    mkdir(2), mkdirat(2)     - make a directory file
   ```

2. whatis －显示非常简洁的命令说明

   ```text
    rimideiMac-10:ln_dir4 admin$ whatis mkdir
    mkdir(1)                 - make directories
    mkdir(2), mkdirat(2)     - make a directory file
   ```

3. info - 显示程序 Info 条目

说明：GNU 项目提供了一个命令程序手册页的替代物，称为 “info”。info 内容可通过 info 阅读器 程序读取。info 页是超级链接形式的，和网页很相似。

```text
    info ls
```

> info 程序读取 info 文件，info 文件是树型结构，分化为各个结点，每一个包含一个题目。 info 文件包含超级链接，它可以让你从一个结点跳到另一个结点。一个超级链接可通过 它开头的星号来辨别出来，把光标放在它上面并按下 enter 键，就可以激活它。

1. alias 创建你自己的命令

   说明: alias 可以用于 自己创建一个属于自己的命令,语句结构 alias name=‘string’

   ```text
   rimideiMac-10:ln_dir4 admin$ ll
   -bash: ll: command not found
   rimideiMac-10:ln_dir4 admin$ alias ll='ls -l'
   rimideiMac-10:ln_dir4 admin$ ll
   total 0
   drwxr-xr-x  5 admin  staff  170  9 19 09:51 dir5
   -rw-r--r--  1 admin  staff    0  9 19 09:43 test2

   rimideiMac-10:ln_dir4 admin$ type ll
   ll is aliased to `ls -l'
   ```

