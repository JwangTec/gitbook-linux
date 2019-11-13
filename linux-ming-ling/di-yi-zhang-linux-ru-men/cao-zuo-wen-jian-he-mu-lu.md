# 2. 操作文件和目录

1. shell通配符

   > 当操作文件的时候,可以使用通配符来匹配文件,这样就可以批量的操作文件

   | 通配符 | 意义 |
   | :--- | :--- |
   | \* | 匹配任意多个字符（包括零个或一个） |
   | ? | 匹配任意一个字符（不包括零个） |
   | \[characters\] | 匹配任意一个属于字符集中的字符 |
   | \[!characters\] | 匹配任意一个不是字符集中的字符 |
   | \[\[:class:\]\] | 匹配任意一个属于指定字符类中的字符 |
   | \[:alnum:\] | 匹配任意一个字母或数字） |
   | \[:alpha:\] | 匹配任意一个字母 |
   | \[:digit:\] | 匹配任意一个数字 |
   | \[:lower:\] | 匹配任意一个小写字母 |
   | \[:upper\] | 匹配任意一个大写字母 |

   示例

   1. `[[:upper]]*` 以大写字母开头的文件
   2. `*[[:lower:]123]`  文件名以小写字母结尾，或以 “1”，“2”，或 “3” 结尾的文件  
   3. `[abc]*` 文件名以“a”,“b”,或“c”开头的文件  
   4. `Data???`  以“Data”开头，其后紧接着3个字符的文件 

2. mkdir

   说明: mkdir是用来创建目录的

   > 可以一次性创建一个文件夹或者多个文件夹

   ```text
   $ mkdir dir1   

   $ mkdir dir1 dir2 dir3
   ```

   命令参数:

   | 参数 | 描述 |
   | :--- | :--- |
   | -m --mode=模式 | 设定权限&lt;模式&gt; |
   | -p --parents | 可以是一个路径名称。若路径中的某些目录尚不存在,加上此选项后,系统将自动建立好那些尚不存在的目录,即一次可以建立多个目录 |
   | -v --verbose | 每次创建新目录都显示信息 |

   > 递归创建多个目录

   ```text
   $ mkdir -p testmkdir/testmkdir
   ```

   > 创建权限为 777 的目录

   ```text
   $ mkdir -m 777 -p test/test1
   ```

3. cp命令

   说明: cp命令是用来复制文件或者目录的

   > 复制文件到哪个文件

   ```text
    $ cp file1 fil2
   ```

   > 复制文件到xx文件里面

   ```text
    $cp file1 file2 dir2
   ```

   > 复制文件夹到另一个文件夹中

   ```text
    cp -r dir1 dir3
   ```

   > 复制文件夹到文件夹，区别在于 test\_dir1不存在会创建新的文件夹

   ```text
    $ cp -r dir1 test_dir1
   ```

   > 复制文件中的所有文件到另一个文件夹中

   ```text
    cp dir/* dir3
   ```

> 扩展选项

| 选项 | 意义 |
| :--- | :--- |
| -a | 复制文件和目录，以及它们的属性，包括所有权和权限。 默认情况下，复本具有用户所操作文件的默认属性。 |
| -i | 在重写已存在文件之前，提示用户确认。如果这个选项不指定， cp 命令会默认重写文件。 |
| -r | 递归地复制目录及目录中的内容。当复制目录时， 需要这个选项（或者-a 选项）。 |
| -u | 当把文件从一个目录复制到另一个目录时，仅复制 目标目录中不存在的文件，或者是文件内容新于目标目录中已经存在的文件。 |
| -v | 显示翔实的命令操作信息 |
| -n | 不要覆盖已存在的文件\(使前面的 -i 选项失效\) |

1. mv命令 移动文件或者文件夹

   mv的命令和cp命令有许多的相似

   > 扩展选项

   | 参数 | 描述 |
   | :--- | :--- |
   | -i | 在重写已存在文件之前，提示用户确认。如果这个选项不指定， cp 命令会默认重写文件。 |
   | -u | 当把文件从一个目录移动到另一个目录时，仅移动 目标目录中不存在的文件，或者是文件内容新于目标目录中已经存在的文件。 |
   | -v | 显示翔实的命令操作信息 |
   | -f | 如果目标文件已经存在，不会询问而直接覆盖 |

> 移动文件到哪个文件

```text
    $ mv file1 file2
```

> 移动目录到哪个目录

```text
    $cp dir1 dir2
```

> 移动目录或文件到到哪个目录下

```text
    $cp file dir2
```

1. rm命令

   说明: rm删除文件 这是一个危险的命令 因为linux没有回收站 所以当你删除了文件是不能后悔的

   | 选项 | 意义 |
   | :--- | :--- |
   | -i | 在删除之前，提示用户确认。 |
   | -r | 递归地删除目录及目录中的内容 |
   | -f | 忽视不存在的文件，不显示提示信息 |
   | -v | 显示翔实的命令操作信息 |

   > 删除文件

   ```text
    rm file1 file2
   ```

   > 删除文件夹

   ```text
    rm -r dir1
   ```

```text
##### 小心 rm! 不要使用 rm / 这样会把你的系统毁掉
```
