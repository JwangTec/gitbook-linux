# 1. 权限

1. 说明:
   1. Unix 传统中的操作系统不同于那些 MS-DOS 传统中的系统，区别在于它们不仅是多任务系统，而且也是 多用户系统。这到底意味着什么？它意味着多个用户可以在同一时间使用同一台计算机。然而一个 典型的计算机可能只有一个键盘和一个监视器，但是它仍然可以被多个用户使用。例如，如果一台 计算机连接到一个网络或者因特网，那么远程用户通过 ssh（安全 shell）可以登录并操纵这台电脑。 事实上，远程用户也能运行图形界面应用程序，并且图形化的输出结果会出现在远端的显示器上。 X 窗口系统把这个作为基本设计理念的一部分，并支持这种功能。
   2. Linux 系统的多用户性能，不是最近的“创新”，而是一种特性，它深深地嵌入到了 Linux 操作系统的 设计过程中。想一下 Unix 系统的诞生环境，这会很有意义。多年前，在个人电脑出现之前，计算机 都是大型的，昂贵的，集中化的。一个典型的大学计算机系统，例如，是由坐落在一座建筑中的一台 大型中央计算机和许多散布在校园各处的终端机组成，每个终端都连接到这台大型中央计算机。 这台计算机可以同时支持很多用户。
2. 权限系统中的命令
   1. id – 显示用户身份号

      当用户创建帐户之后，系统会给用户分配一个号码，叫做用户 ID 或者 uid，然后，为了符合人类的习惯，这个 ID 映射到一个用户名。系统又会给这个用户 分配一个原始的组 ID 或者是 gid

      ```text
      rimideiMac-10:log admin$ id
      uid=503(admin) gid=20(staff) groups=20(staff),703(com.apple.sharepoint.group.3),12(everyone),61(localaccounts),79(_appserverusr),80(admin),81(_appserveradm),98(_lpadmin),701(com.apple.sharepoint.group.1),33(_appstore),100(_lpoperator),204(_developer),250(_analyticsusers),395(com.apple.access_ftp),398(com.apple.access_screensharing),399(com.apple.access_ssh)
      ```

      > uid 是用户的独立id gid是用户所属的用户组 后面的groups是表示这个系统中的用户组有哪些
3. chmod – 更改文件模式
   1. 数字的意义

      权限模式

      | Octal | Binary | File Mode |
      | :--- | :--- | :--- |
      | 0 | 000 | – |
      | 1 | 001 | —x |
      | 2 | 010 | -w- |
      | 3 | 011 | -wx |
      | 4 | 100 | r— |
      | 5 | 101 | r-x |
      | 6 | 110 | rw- |
      | 7 | 111 | rwx |

```text
当我看到如下,就能分析出来 文件的所有者 admin有 读写 用户组staff对文件有 读 其他用户对文件有读权限

```
-rw-r--r--  1 admin  staff    0  9 19 09:48 file2
```


>更改文件或者目录的权限

```
rimideiMac-10:test admin$ chmod 600 file2 

```

>循环递归的改变文件夹和文件里面的权限

```
rimideiMac-10:test admin$ chmod -R 777 dir4

```

2. 符号表示法

 chmod 命令符号表示法

 |符号|意义|
 |---|---|
|u| “user”的简写，意思是文件或目录的所有者。|  
|g|  用户组。 | 
|o|  “others” 的简写，意思是其他所有的人。  |
|a |     “all” 的简写，是“u”，“g”，和 “o” 三者的联合。|  


 chmod 符号表示法实例

  |命令|意义|
  |---|---|
  |u+x  |        为文件所有者添加可执行权限。  
  |u-x      |   删除文件所有者的可执行权限。  
  |+x       |  为文件所有者，用户组，和其他所有人添加可执行权限。等价于 a+x。  
  |o-rw        | 除了文件所有者和用户组，删除其他人的读权限和写权限。  
  |go=rw      |   给群组的主人和任意文件拥有者的人读写权限。如果群组的主人或全局之前已经有了执行的权限，他们将被移除。   
  |u+x,go=rw  |       给文件拥有者执行权限并给组和其他人读和执行的权限。多种设定可以用逗号分开。  


  u代表 用户  g 代表用户组 o代表其他人

  示例:

  ```
  $ rimideiMac-10:test admin$ chmod u+x dir4
  $ rimideiMac-10:test admin$ chmod u-x dir4

  ```

  删除权限是对文件所属的目录有w权限


3. su – 以另一个用户的身份来运行 shell

4. sudo – 以另一个用户的身份来执行命令

5. chown – 更改文件所有者

    chown 命令被用来更改文件或目录的所有者和用户组。使用这个命令需要超级用户权限。

    chown 参数实例

  |参数|        结果 |
  |---|---| 
  |bob|         把文件所有者从当前属主更改为用户 bob。  
  |bob:users|         把文件所有者改为用户 bob，文件用户组改为用户组 users。  
  |:admins      |   把文件用户组改为组 admins，文件所有者不变。  
  |bob:         |文件所有者改为用户 bob，文件用户组改为，用户 bob 登录系统时，所属的用户组。  

  ```
  $ rimideiMac-10:test admin$ chown canvas  file2
  ```


    passwd – 更改用户密码

    只要输入 passwd 命令，就能更改你的密码。shell 会提示你输入你的旧密码和你的新密码：

    ```
    $ passwd
    ```
```

