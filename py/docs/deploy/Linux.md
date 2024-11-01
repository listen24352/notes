

[TOC]



# Linux 常用命令

## cd 命令 

>   change directory  

```bash
# cd 目录  切换指定目录

# 切换到当前用用户主目录   cd
cd ~       

# 切换到上一级目录
cd ..        

# 切换到上一次所在的目录
cd -       

# 切换到当前目录
cd .        
```

## ls 命令

作用:  查看目录的信息

形式:  ls [选项] [默认当前目录]  

常用选项:

-l   详细信息

-h  human being 人类友好 方式显示文件大小（需要和 l 合用才有效果）

-a  all  显示指定目录下所有的文件信息(包括隐藏文件)

```shell
# 常用容量单位  bit-8-Byte-1024-KB-1024-MB-1024-GB-TB-PB-EB-ZB
ls ~/Desktop/
ls -l -a == ls -a -l == ls -la == ls -al  == ll
ls -alh ~/Desktop/ready/
```

>   在 Linux 中不以后缀名区分文件类型  
>   以点符 .开始的文件默认隐藏  需要使用-a 才能显示出来

## mkdir 命令选项

作用:创建目录

形式:mkdir 选项 目录名

常用选项:

-p   parents 如果子目录的父目录不存在就自动创建父目录

```shell
# 不能直接创建多级目录
python@ubuntu:~/py27$ mkdir 2/3/4
mkdir: 无法创建目录"2/3/4": 没有那个文件或目录
python@ubuntu:~/py27$ mkdir -p 2/3/4
python@ubuntu:~/py27$ tree
.
├── 1
│   └── 2
│       └── 3
├── 1.py
├── 2
│   └── 3
│       └── 4
├── haha
└── project1.py
```



## rm 命令选项

作用:删除文件或者目录

形式:rm 选项 文件目录名 ...

常用选项:

-r  递归删除目录下所有的文件

-f  静默删除一个文件

-i  交互式 需要用户确认是否删除

-f  静默删除一个文件

-d  删除空目录

```shell
leo@ubuntu:~/py27$ rm -i 1.py
rm：是否删除普通空文件 '1.py'？ yes

python@ubuntu:~/py27$ rm 1.py
rm: 无法删除'1.py': 没有那个文件或目录

python@ubuntu:~/py27$ rm -f 1.py
python@ubuntu:~/py27$ rm -d haha  # 等价于  rmdir haha
python@ubuntu:~/py27$ rm -d 1  # 非空出错 
rm: 无法删除'1': 目录非空

rm -r /home/python/py27/
rm -rf /  删除整个系统根目下及其所有的子目录
```



## cp 命令

作用: 复制文件或者目录

形式: cp 选项 源目录/源文件名 目的目录/

常用选项:

```shell
# -r  递归拷贝目录
cp -r ../code /home/python/Desktop

# -i  交互式  默认情况会自动覆盖目的目录的同名文件 
cp 1.py ~/Desktop/
#    加-i  并且 在目的目录有同名文件就提示 需要用户确认是否需要覆盖
cp -i 1.py ~/Desktop/

# -v 显示拷贝的文件所在的路径信息 
cp -v 1.py ~/Desktop/

# -a 保留原有文件的相关属性 权限时间等 默认情况不保留
cp xjj.jpg ~/Desktop/
cp -a xjj.jpg ~/Desktop/
```

>   cp 也可以在拷贝文件的时候给文件一个新的名字
>
>    cp 选项 源目录/源文件名 目的目录/新文件名
>
>   cp xjj.jpg ~/Desktop/xjj2.jpg



## mv 命令选项

作用:移动、重命名     文件 、目录

形式:mv 选项 源目录/源文件名 目的目录/

常用选项:

```shell
# -i 如果目的路径下有同名文件默认覆盖  加-i 要求用户确认是否覆盖文件数据
mv -i xjj.jpg ~/Desktop/

# -v 显示移动的文件路径信息
mv -v xjj.jpg ~/Desktop/

# 移动文件并且改名
mv girl.jpg ~/xjj.jpg

# 目录改名
mv Linux/ linux/
```

## cat 文件名

## more 文件名

>   文件内容很少 一样的
>
>   文件内容很多的额情况下    cat 查看内容会直接全部显示<刷屏>
>
>   more 会分屏显示文件内容  空格显示下一页  q 退出

## tail命令

## 输出重定向

概念: 把原本要输出到终端的结果  转而输出到文件中<输出重定向>

用法: 命令   符号  文件名字

符号种类:  

> ​		>    覆盖输出重定向  类似文件打开方式的"w"模式

> ​		>> 追加输出重定向  类似文件打开方式的"a"模式

```shell
ls -l > a.txt 
ls -alh > a.txt   # 第二次命令结果会覆盖文件原有内容 

ls -alh /bin >> a.txt  # 本次命令结果会追加原有文件内容后面
```

## 管道

概念:把左边命令的输出结果 给 右边的命令当做输入来用。

形式:命令  | 命令

用法:

```shell
 # cat a.txt | more   # more a.txt
 ls -alh /bin | more


 显示当前目录下所有文件详细信息         搜索以-开始的行          统计行数
ls -al | grep "^-" | wc -l
```

>   |右侧一般是 more grep  awk 

## 链接

作用:  通过链接文件**间接访问**、修改源文件 **方便快捷**  link

分类: 

​	软 ln -s 源文件 链接文件   <symbols  符号链接>

​	硬 ln 源文件 链接文件 

用法:

```shell
ln -s 1.txt 1s.txt
gedit 1s.txt 
python@ubuntu:~/Desktop/Linux$ cat 1.txt 
hehehehehheHEIHEI

# 通过软链接可以间接访问 、修改源文件数据
# 如果源文件删除了   软连接不可用   硬链接不受影响
ln 1.txt 1h.txt  # 可以通过1h.txt 间接访问和修改源文件

# 硬链接本质
# 硬链接其实是一个文件数据的别名  硬链接数就是一个文件数据的名字的数量
rm 文件 # 只是删除文件数据的一个别名 而数据只有在没有名字的情况下才会删除
```

>   工作建议:   创建  跨目录的链接文件      建议都写成 绝对路径方式
>
>   工作中软链接常用 软链接可以指向一个目录 硬链接 不可以

## 文本搜索grep

作用: 根据文本数据去文件中搜索

格式: grep 选项 "文本数据" 文件名

选项: 

-i 忽略大小写  

-n 显示行号

-v 反选条件

用法: 

```shell
leo@ubuntu:~/Desktop/Linux$ grep "itcast.cn" grep.txt
www.itcast.cn
itcast.cn
python@ubuntu:~/Desktop/Linux$ grep -i "itcast.cn" grep.txt
www.itcast.cn
WWW.ITCAST.CN
itcast.cn
ITCAST.CN
python@ubuntu:~/Desktop/Linux$ grep -ni "itcast.cn" grep.txt
1:www.itcast.cn
2:WWW.ITCAST.CN
6:itcast.cn
7:ITCAST.CN
python@ubuntu:~/Desktop/Linux$ grep -niv "itcast.cn" grep.txt
3:ia
4:ib
5:a.com.cn
11:itheima.com
12:www.itheima.com

# 管道可以结合 grep 对前面命令的输出结果进行筛选
python@ubuntu:~/Desktop/Linux$ ls | grep "txt" 
12.txt
1h.txt
1s.txt
2.txt
3.txt
4.txt
a.txt
grep.txt
#  grep结合正则使用 
# 查询文件中 以itcast.cn的开始行并且显示行号 忽略大小写
python@ubuntu:~/Desktop/Linux$ grep -ni "^itcast.cn" grep.txt
# 查询文件中 以cn的结束的行并且显示行号 忽略大小写
python@ubuntu:~/Desktop/Linux$ grep -ni "cn$" grep.txt
# 查询文件中 i字母后为任意非换行字符的 数据
python@ubuntu:~/Desktop/Linux$ grep -ni "i." grep.txt
```

## 查找文件find 

作用: 根据文件特征(名字)查找文件

形式: find 路径 选项 参数

会在路径参数对应的**路径及其所有的子目录**当中去查找

用法:

```shell
find . -name ".py"  # 在当前下查找名字叫.py的所有文件
find / -name ".py"  # 在/下查找名字叫.py的所有

sudo find / -name ".py"  # sudo 命令....  以系统管理员权限运行后面命令 输入 python 用户密码

# 大多数情况下可能并不知道文件的完整名字  此时可以使用通配符(非正则)
*   任意(0)个任意字符     a*    *.txt
?   一个任意字符      a?     ?.txt
python@ubuntu:~/Desktop/Linux$ find . -name "?.txt"
python@ubuntu:~/Desktop/Linux$ find . -name "*.txt"
```

>   通配符在 Linux 命令中可以和很多命令合用 
>
>   ls  cd cp mv 
>
>   leo@ubuntu:~/Desktop/Linux$ ls 1?.txt
>   12.txt  1h.txt
>
>   leo@ubuntu:~/Desktop/Linux$ ls 1*.txt
>   12.txt  1h.txt  1.txt

## gz和bzip2文件操作

格式:  tar 选项 压缩包名字  […..]

常用选项: 

​	-c  create打包

​	-v 显示详细过程

​	-f 指定压缩包名字  紧跟压缩包名字

​	-x 解包

​	-z gzip算法格式

​	-j  bzip2算法格式

​	-C 解压到指定路径   紧跟目的路径

>   -f 选项之后必须立马跟上 压缩包的名字

```shell
# 将当前目录下所有文件和目录 打包压缩成 1.tar.gz
tar -zcvf 1.tar.gz *
# # 将当前目录下所有文件和目录 打包压缩成 1.tar.bz2
tar -jcvf 1.tar.bz2 *

# 解压缩gz 文件
tar -zxvf  1.tar.gz
# bz2 文件
tar -jxvf 1.tar.bz2 

# -C 解压到指定路径
tar -jxvf 1.tar.bz2 -C ~/Desktop/
```

## zip文件操作

```shell
# 压缩当前目录下所有的txt 文件成 my.zip
zip my.zip *.txt   
# 解压当前目录下 my.zip
unzip my.zip
# 解压当前目录下 my.zip 到 桌面
unzip my.zip -d ~/Desktop/
```

>   unzip my.zip
>
>   unzip my.zip -d ~/Desktop/

## chmod文件权限

每个文本所拥有的的 读read r 写 write w 执行 eXecute x的权利。

```shell
leo@ubuntu:~/Desktop/Linux/Test$ ll
drwxrwxr-x 4 python python 4096 7月  20 11:47 ./
drwxrwxr-x 9 python python 4096 7月  20 11:26 ../
-rw-rw-r-- 1 python python    0 7月  20 11:25 12.txt
-rw-rw-r-- 1 python python   18 7月  20 11:25 1h.txt
-rw-rw-r-- 1 python python   13 7月  20 11:25 2.txt
-rw-rw-r-- 1 python python  714 7月  20 11:25 3.txt

python1 用户   python2 用户  python 组
python3 用户   itheima 组

rw-        rw-         r-- 分为三组   每一组有三个权限分别是读 写 执行
-表示占位 无权限
文件所属用户 同组用户权限  其他(非所属用户 非同组用户)
user  u    group  g    other o                    所有 all a

# 修改文件的权限
# 1   字母法 方式1 小白都会使用
chmod augo+-=rwx   文件名
chmod u+x 2.txt
#chmod u + x 2.txt

# 2 数字法 方式 2 高手都用这种
r    4
w    2
x    1
# 用一个数字来表示一组权限 如果需要设置一个权限 需要将这个权限对应的值加到这个数字中
# 0表示该组没有任何权限

chmod 755 2.txt   # rwx r-x r-x
chmod 644 2.txt   # rw-r--r--
chmod 640 2.txt   # rw-r-----
```

## ps命令



## 用户基本操作

>   root 用户   超级系统管理员  拥有系统最高权限

```shell
# sudo  命令  可以让一个命令以 系统管理员root权限运行<安装卸载软件>
sudo mkdir haha

# sudo -s 切换到 root 用户使用
exit   退出登录用户;退出终端

whoami 查看当前用户的名字

passwd 用户名  修改指定用户的密码 一般需要输入这个用户原密码
		root 用户修改所有普通用户都不用知道原密码

which 指令  这个指令程序所在的路径
reboot 重启
shutdown -r 20:25 定时重启
shutdown -r now 关机后重启
shutdown -r +10 10分钟后重启
```

## 用户管理

>   用户管理和用户组管理 都需要 root 权限  即 sudo 命令

```shell
# 创建用户    创建用户时如果不指定用户组 会自动创建一个同名组
python@ubuntu:~$ useradd laowang -m 
python@ubuntu:~$ useradd laowang -m -g python

#验证用户   
python@ubuntu:~$ cat /etc/passwd
python@ubuntu:~$ id laowang      # 发现laowang 用户已经创建成功

# 验证组信息  
python@ubuntu:~$ cat /etc/group # 发现新增了 laowang 组

# 设置用户密码   sudo passwd laowang   

# 切换到新用户需要先设置这个用户的密码
#切换用户 
python@ubuntu:~$ su laowang  # 需要输入 laowang 的密码  不切换当前路径
python@ubuntu:~$ su - laowang #输入laowang 的密码  当前路径切换为用户主目录

# exit 退出登录的用户

# 如果需要一个用户使用 sudo  需要这个添加 sudo 这个附加组 
# 修改用户所在普通组 和 附加组  usermod 用户名 -g 普通组 -G 附加组

# 以 root 权限运行( 设置老王的附加组为 sudo)  
python@ubuntu:~$ sudo usermod laowang -G sudo
# 以 root 权限运行( 设置老王的附加组为 sudo) 并且设置老王的组为 python
python@ubuntu:~$ sudo usermod laowang -G sudo -g python

```

操作附加组

	useradd laowang -m 

删除用户 

	userdel 删除用户时 -r 能够删除用户主目录

>   在删除用户时  用户必须不能被占用(需要把占用的用户 使用 exit 退出 )

>   用户组  -g  家庭
>
>   附加组  -G  组织

## 用户组管理

```shell
# 创建用户组  
sudo groupadd heihei

# 修改用户组
sudo usermod -g 普通组 用户名

# 删除用户组
sudo groupdel heihei

# 查看用户组
cat /etc/group
```

## 远程登录

[FinalShell](https://www.hostbuf.com/)

```bash
# 1 在服务器上安装 
sudo apt-get install openssh-server<虚拟机自带>

# 2 在客户端需要安装 ssh 工具
windows 双击 exe 一直下一步 直到完成
运行-cmd-ssh  显示参数说明安装完成

# 3 在服务器中获取服务器 IP
ip a

# 4 在客户端中登录服务器    黑窗口中输入 ssh 用户名@服务器ip地址
ssh python@192.168.134.100
```

## 远程拷贝

```shell
# 上传(客户端到服务器)
scp  -r 本机地址路径  远程主机路径(远程服务器用户名@远程服务器ip地址:绝对路径)
scp -r 1.py leo@192.168.134.100:/home/python/Desktop/

# 下载(服务器到客户端)
scp  -r 远程主机路径 本机地址路径  
scp -r leo@192.168.134.100:/home/python/Desktop/1.py .
```

# Shell

# Ubuntu22.04 Tips

## 安装软件

```shell
# 在线
	sudo apt-get install sl
	sudo apt install sl

# 离线<明天学习网络需要使用>
	sudo dpkg -i mNetAssist-release-amd64.deb 
```

## 卸载

```shell
# 在线
sudo apt-get remove sl

# 离线
sudo dpkg –r 安装包
```

## 设置软件安装源

```shell
https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/
# /etc/apt/sources.list

# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
```

```
### 3.3 相对和绝对路径

相对路径  从当前所在目录出发描述的路径  cd ../../Desktop

绝对路径  从系统根目录/出发描述的路径    cd /home/python/Desktop



命令中  Tab 键作用     自动补齐文件、目录名

>   清屏      ctrl l     《clear》  
```





