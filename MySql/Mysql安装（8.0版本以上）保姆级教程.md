# MySql的下载

到官网，网址：https://www.mysql.com/

![image-20210901201651604](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901201651604.png)

![image-20210901201808948](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901201808948.png)

![image-20210901201838431](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901201838431.png)

![image-20210901201920251](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901201920251.png)



**下载之后会有一个安装包，把他解压出来，放在一个你比较好找的路径**，如果怕出事，可以按我的完全一样。

![image-20210901202623185](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901202623185.png)



# MySql安装



添加一个全局变量，要是安装过其他软件VScode，python，java之类的应该都会，但咱是保姆级教程，所以说一下。

注：这里必须提前说明一下，我安装的是压缩版的，如果你的不是最好被往下看了。浪费我好多时间第一次搞，和另外别的安装方式错乱了。所以最好你自己找好一种方式安装，别看看这看看那，浪费时间，另外不同的版本的MySql的安装是有细节上的不同的，不注意可能会出现错误。



如果你安装过程出现错误，可以**卸载**。

```
net stop
```

```
mysqld --remove
```

## 1.找到你刚刚解压的那个安装包下bin的路径，复制下来

![image-20210901202715548](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901202715548.png)

```c
D:\mysql-8.0.26-winx64\bin
```



## 2.添加全局变量

回到盘符页面

<img src="C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901203039024.png" alt="image-20210901203039024" style="zoom:80%;" />

**属性->高级系统设置->环境变量->Path->**

<img src="C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901203314560.png" alt="image-20210901203314560" style="zoom:80%;" />

**如果没有Path可以自己创建一个**

**双击Path，把刚刚复制下来的路径添加进去，上下两个Path都添加一下**，

<img src="C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901203546761.png" alt="image-20210901203546761" style="zoom:80%;" />



## 3.创建ini.my文件

<img src="C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901203842083.png" alt="image-20210901203842083" style="zoom:80%;" />

里面存以下内容，没有这个的话，**后面初始化会失败**；

后面如果出现初始化失败的话，可能就是这个文件里的路径出现了问题。这个路径一定要是你刚刚用过的安装mysql的路径。

```mysql
[mysql]
# 设置 mysql 客户端默认字符集
default-character-set=utf8
[mysqld]
# 设置 3306 端口
port = 3306
# 设置 mysql 的安装目录，替换成你自己解压的目录
basedir = D:\\mysql-8.0.26-winx64
# 设置 mysql 数据库的数据的存放目录，，替换成你自己解压的目录
datadir = D:\\mysql-8.0.26-winx64\\data
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为 8 比特编码的 latin1 字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 创建模式
sql_mode = NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

```

## 4.初始化，安装，启动，修改密码

<img src="C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210901204223959.png" alt="image-20210901204223959" style="zoom:80%;" />

**以管理员身份打开命令提示符**,用dos命令切换到mysql安装的路径

```
cd /D D:\mysql-8.0.26-winx64\bin
```

然后按以下操作，一步一步来，不然容易出错。

1.输入,输入后回车

```
mysqld --initialize --console
```

这个时候会弹出一长串东西，如果出现error，错误的话，说明你刚刚的my.ini文件出现了问题。

最后面会有一个随机的密码，因为我安装完了，不好截图。

**这个密码很重要，可以先复制保存下来，我第一次安装就是不知道怎么回事没有这个密码**

如果你不小心关掉了这个窗口，或者没有记到那个密码的话，不用慌，有办法，很多别的博客根本没有说这些东西。

你把data文件夹下的所有东西全部删掉，重新进行一遍初始化，之后又有了。

2.输入安装命令

```
mysqld install
```

3.启动

```
net start mysql
```



### 修改密码

输入

```
mysql -u -root -p
```

![6e31609eb86c0f1b7bf86f03e5ae1e04.png](https://img-blog.csdnimg.cn/img_convert/6e31609eb86c0f1b7bf86f03e5ae1e04.png)

进入MySQL,输入，这个地方的一定大写，你用别人的那个小写的那个代码，会报错，我试过了，用下面这段就行。

```
ALTER USER "root"@"localhost" IDENTIFIED BY "你的密码";
```

把“你的密码”改成你想改的

![dc09a8187d8918b0368ffd7d9e099a54.png](https://img-blog.csdnimg.cn/img_convert/dc09a8187d8918b0368ffd7d9e099a54.png)

quit退出，重新登入，如果可以登入说明你成功了。

恭喜！