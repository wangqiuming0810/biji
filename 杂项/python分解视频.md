
分解视频需要使用到 Open cv2 这个包，之前安装过 Anaconda，所以我们在 Anaconda的基础之上安装这个包就行了。

因为国外国外的官网比较 慢，所以我们可以利用清华镜像的，

打开cmd，以管理员身份运行



1. 添加清华镜像

   ```
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
   ```

2. 安装opencv

   ```
   conda install opencv
   ```



当然你如果没有安装Anaconda，你也可以直接安装，cv2

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple opencv-python
```

但是我安装的时候老是提示我的 pip 版本 比较低，安装到一半就失败了，后面改成conda安装就可以了

如果你也是这样的话，你也可以安装conda，来安装，然后再pycharm改变一下解释器，导入conda的包

官网指令：

```
pip install opencv-python
```
上下两个指令，选择一个就可以了，不用都执行，上面那个清华镜像比较快



![在这里插入图片描述](https://img-blog.csdnimg.cn/52f4d70b03964e00ac60631b9180b94a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5LiH5LyP5bCP5aSq6Ziz,size_20,color_FFFFFF,t_70,g_se,x_16)

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-aokKtyHE-1638782791594)(C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20211206172356506.png)][外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-ZpnOVp5I-1638782791595)(C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20211206172437966.png)]](https://img-blog.csdnimg.cn/11a272f203e641a7953a2877afdf30ad.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5LiH5LyP5bCP5aSq6Ziz,size_20,color_FFFFFF,t_70,g_se,x_16)

写代码了，用代码分解视频，一帧一帧分解出来的，



代码：

```python
import cv2

mp4 = cv2.VideoCapture("test.mp4")  # 读取视频,路径
is_opened = mp4.isOpened()  # 判断是否打开
print(is_opened)
fps = mp4.get(cv2.CAP_PROP_FPS)  # 获取视频的帧率
print(fps)
width = mp4.get(cv2.CAP_PROP_FRAME_WIDTH)  # 获取视频的宽度
height = mp4.get(cv2.CAP_PROP_FRAME_HEIGHT)  # 获取视频的高度
print(str(width) + "x" + str(height))
cnt = 0
while is_opened:
    if cnt == 100:  # 截取前100帧，每4帧一张图片，这个可以自己改，数字可以自己改
        break
    else:
        cnt += 1
    (flag, frame) = mp4.read()  # 读取图片
    file_name = "iamge" + str(cnt) + ".jpg"
    print(file_name)
    if flag == True and cnt%4==0:
        cv2.imwrite(file_name, frame, [cv2.IMWRITE_JPEG_QUALITY])  # 保存图片会保存在当前py所在文件的地方
print("转换完成")

```

