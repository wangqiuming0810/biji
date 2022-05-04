# 人人开源项目下载运行



### 运行后端环境

下载地址

```
https://gitee.com/renrenio/renren-fast
```

打开idea，利用git拉取代码

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存失败,源站可能有防盗链机制,建议将图片保存下来直接上传上传(im3nPI9tv945-1632813737429)(C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210928150731685.png)(C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210928150731685.png)][外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-92lbtw0W-1632813737431)(C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210928150748876.png)]](https://img-blog.csdnimg.cn/2e6810a0ed1546038019308fe088b27b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiH5LyP5bCP5aSq6Ziz,size_20,color_FFFFFF,t_70,g_se,x_16)

![在这里插入图片描述](https://img-blog.csdnimg.cn/f91b4e66fc234675bc43db9b9b57f2a5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiH5LyP5bCP5aSq6Ziz,size_20,color_FFFFFF,t_70,g_se,x_16)



克隆地址：

```
https://gitee.com/renrenio/renren-fast.git
```

下载完毕，运行

- 创建 renren_fast 数据库

- 运行db下的mysql文件
- 修改 application-dev.yml ，更新MySQL账号和密码

![在这里插入图片描述](https://img-blog.csdnimg.cn/08af421417a04e5d8296408edb03c8b4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiH5LyP5bCP5aSq6Ziz,size_20,color_FFFFFF,t_70,g_se,x_16)

- 运行路径src/main/java下的 RenrenApplication.java ，main函数



后端运行完成



### 运行前端

安装配置环境node.js

IDE：VS code



按照上面的一样利用idea，git拉取代码，下载完成后，VS code打开整个文件夹

![在这里插入图片描述](https://img-blog.csdnimg.cn/64d9eab0a4d7454dbdbb8137caa23caa.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiH5LyP5bCP5aSq6Ziz,size_20,color_FFFFFF,t_70,g_se,x_16)



打开终端

输入，安装依赖环境指令

```
npm install
```

运行项目

```
npm run dev
```



运行成功，会自动跳转到，没有的话，手动跳转

```
http://localhost:8001
```

账号、密码

```
admin
admin
```



结束。

