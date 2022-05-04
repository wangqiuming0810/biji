# 分解视频的代码：

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
i = 0
cnt = 0
while is_opened:
    if cnt == 100:  # 截取前10张图片，这个参数是可以自己改的，间隔多久，自己理解理解代码意思，自行改动
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

# 安装CV2

这个代码需要用到 cv2 这个包，所以你得先安装一下cv2。



打开cmd ，命令提示符，输入下面的指令：

```
pip install opencv-python
```

如果中途下载没有断，并且最后有successful 之类的英文提示安装成功，说明你成功了，也不用往下看了。

![image-20211217161033571](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20211217161033571.png)

出现这个样子，就不用往下看了。



但是如果你中途下载比较慢，

![image-20211217161124495](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20211217161124495.png)

你可以试一下下面的指令,使用清华镜像：

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple opencv-python
```

下载成功就可以，如果提示你，你的pip版本过低，你就可以，更新一下pip版本，

![img](file:///C:\Users\wang\Documents\Tencent Files\527734202\Image\C2C\P3IBHE4R}HTTDHH1QGLTW4W.png)

```
python -m pip install --upgrade pip  
```

然后在执行一遍上面的指令：





最后成功：

![image-20211217161033571](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20211217161033571.png)



就ok了，你可以写代码了。

代码运行成功是这样的。

![image-20211217161502428](C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20211217161502428.png)

~~如果出现其他问题，可能我也没见过，可以自己百度一下。~~



