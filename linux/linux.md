<h1>linux</h1>
- # **1、文件目录操作指令**

  - su   切换用户

  - ls 显示全部文件

    - ls -a   显示全部文件，并把隐藏的文件显示出来
    - ll   显示全部文件并显示文件的详细信息

  - clear   清屏

  - cd   切换目录

  - touch   新建空文件

  - echo   添加内容到文件中
    - echo "xxxxxxxxxxx" > xxx（覆盖）
    - echo "xxxxxxxxxxx" >> xxx（追加内容）
    
  - mkdir   创建目录
    
    - -p   创建多级目录
    
  - rm 
    - rmdir 删除空文件夹
    - 删除普通文件
    - -rf 强制删除文件
    - -r 连同文件夹一起删除
    
  - cp 拷贝文件

    - -r 连同文件夹一同复制

  - mv 
    - 移动文件
    - 修改文件名
    
  - pwd 显示当前目录

  - grep 查找指定字符串

    - cat xxx | grep "xxx"

  - wc 显示文档行数，字数，字符数

    -  -c统计字节数- l统计行数-w统计词数 
    -  wc -c xxx

  - find 查找指定文件
    
    - find <指定目录> <指定条件> <指定动作>
    
      whereis 加参数与文件名
    
      locate 只加文件名
    
      find 直接搜索磁盘，较慢
    
      find / -name “string*”
    
  - tree 显示目录树
    
    - yum install tree（安装tree命令）
    
  - cat 显示文件内容
    - cat -n xxx 每行以标号显示
    - cat > xxx 编辑内容
    - tac 倒序显示
    - cat aaa  > bbb 复制内容到bbb（覆盖）	
    - cat aaa  >> bbb 复制内容到bbb（追加）

- # **2、系统管理命令**

  - stat	显示指定文件的相关信息
    - stat 文件名
  - who、w 显示在线登录用户
  - whoami 显示用户自己的身份
  - hostname 显示主机名
  - uname 显示系统信息
    - uname -a 显示全部信息 (内核名称，主机名，内核版本号，内核版本，硬件名，处理器类型，硬件平台类型，操作系统名称)
  - top 显示当前系统中耗费资源最多的进程 动态显示过程，实时监控
  - ps 显示瞬间进程状态
    - ps -aux 显示所有瞬间进程状态
    - kill -9 xxxx 结束进程
  - du 显示指定的文件（目录）已使用的磁盘空间的总量 .可以使用--help查看帮助
    - du
    - du familyA
    - du -h familyA
  - df 显示文件系统磁盘空间的使用情况
    - df
    - df -h 空闲空间
  - free 显示当前内存和交换空间的使用情况 	
  - ifconfig 显示网络接口信息 
  - ping 测试网络的连通性 
  - netstat 显示网络状态信息，查看网络是否连通

- # **3、备份压缩命令**

  - zip

    - ``` shell
      - zip（yum install zip）
        - zip -r xxx.zip /目标文件
      - unzip(yum install unzip)
        - unzip xxx.zip
      ```

  - tar(打包/解包命令) 

    - ``` shell
      - tar -cvf xxx.tar /目标文件（仅打包，不压缩）
      - tar -xvf xxx.tar（解压缩）
      - tar -zcvf xxx.tar.gz /目标文件（打包后，以gzip压缩）
      - tar -zxvf xxx.tar.gz（gzip解压缩并解包）
      - tar -jcvf xxx.tar.bz2 /目标文件（打包后，以bzip2压缩）
      - tar -jxvf xxx.tar.gz（bzip2解压缩并解包）
      ```

  - gzip

    - ``` shell
      - gzip xxx.tar(压缩后最终格式：xxx.tar.gz)直接将源文件压缩，不保留源文件
      - gzip -l xxx.tar.gz(查看压缩包详细信息)
      - gzip -dv xxx.tar.gz(解压缩文件)
      - gzip -v -9 xxx.tar(高压缩比)
      - gzip -v -1 xxx.tar(低压缩比)
      ```

  - bzip2

    - ``` /shell
      - bzip2 -z xxx.tar(压缩后最终格式：xxx.tar.bz2)
      - bzip2 -z xxx.tar.bz2(解压缩)
      ```

- # **4、用户群组操作命令**

  - 用户操作
    - useradd 创建用户
    - userdel 删除用户
      - userdel -r 用户名 连同用户目录一起删除
    - passwd 用户名 修改用户密码
    - cat /etc/passwd 查看用户信息
  - 群组操作
    - groupadd   创建组
    - groupdel   删除组
    - groups 用户名   查看用户所属的群组
    - gpasswd -a 用户名 组名   把用户加入群组
    - gpasswd -d 用户名 组名   把用户踢出群组
    - more /etc/group   查看组信息

- # **5、VIM编辑器命令**

  - vim编辑器
    - vim 文件名
    - 按i进入编辑模式
    - esc切换至命令模式
    - :wq回车保存退出
    - 编辑模式显示行号
      - :set number回车显示行号
      - :set nonumber回车取消显示行号
  - vi编辑器
    - 快捷键使用：
    - a　　在光标后一位开始插入
    - A　　在该行的最后插入
    - I　　在该行的最前面插入
    - gg　　直接跳到文件的首行
    - G　　直接跳到文件的末行 
    - dd　　删除行，如果 5dd ，则一次性删除光标后的5行 
    - yy　　复制当前行, 复制多行，则 3yy，则复制当前行附近的3行 
    - p　　粘贴 
    - v　　进入字符选择模式，选择完成后，按y复制，按p粘贴 
    - ctrl+v　进入块选择模式，选择完成后，按y复制，按p粘贴 
    - shift+v　进入行选择模式，选择完成后，按y复制，p粘贴
    - x 逐个删除  u 撤销删除

- # **6、读写权限命令chmod**

  - 拥有者

    - u：user
    - g：group
    - o：others
    - a：all

  - 权限

    - r：可读，数字表示4
    - w：可写，数字表示2
    - x：可执行，数字表示1
    - -：不具有任何权限，数字表示0
    - <font color = "red">增加权限使用+号，删除权限使用-号，详细权限使用=号</font>

  - 用例：

    - ``` /linux
      chmod u+r somefile #给某文件添加用户可读权限
      chmod u-w somefile #给某文件删除用户可写权限
      chmod abc somefile #a,b,c各为一个数字，分别代表user，group，other的权限
      chmod —R a+r * #将目前目录下的所有档案与子目录设为任何人可读取
      ```

  - chown 改变文件的拥有者

    - ``` /linux
      chown john aa.txt #将文件aa.txt修改拥有用户为john	
      chown :john aa.txt #继续将文件aa.txt修改拥有用户群组为john
      chown -R john somedir #somedir为一个目录，该命令将该目录及子目录和子文件修改拥有用户为john 
      chown -R john:join somedir #同时修改用户和用户群组
      ```

  - chgrp 改变文件的拥有群组

    - ``` /linux
      chgrp john aa.txt #将文件aa.txt修改用户群组为john
      chgrp -R john somedir #somedir为一个目录，该命令将该目录及子目录和子文件修改用户群组为john 
      ```

- # **7、其他命令**

  - less   查看最近的登录历史记录
  - date
    - date +%Y-%m-%d
    - date +%T
  - cal 年份   查看指定年份日历
  - more 文件名   可以翻页查看, 下翻一页(空格) 上翻一页（b） 退出（q） 
  - less 文件名    可以翻页查看,下翻一页(空格) 上翻一页（b），上翻一行(↑) 下翻一行（↓） <u>可以搜索关键字（/keyword）</u>
  - tail -10 文件名   查看文件尾部的十行
  - head -10 文件名   查看文件头部的十行
  - source /etc/profile   让配置文件生效
  - init 0   关闭linux系统
  - reboot   重启
  - systemctl stop firewalld.service   关闭防火墙
  - service iptables status  永久关闭防火墙
  - history 查看用过的命令列表
  - 
