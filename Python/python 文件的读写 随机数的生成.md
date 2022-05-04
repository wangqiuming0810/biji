这里介绍的是比较简单的读写，例如：将生成的随机数，写到文件中。

要用到：

```python
f1 = open("in.txt", 'r')   
# 读入地址，r为读入
f2 = open("out.txt",'w')
# 文件不存在就新建一个文件
# 写入 ,写入的内容必须是字符串
f2.write()
```



随机数生成代码：

```python
import random

# f1 = open("in.txt", 'r')
f2 = open("out.txt",'w')
i=0
while i<10:
    num = random.randint(1, 10)
    f2.write(str(num)+'\n')
    i+=1
print(f2)
print("生成随机数成功！")
f2.colse()
```



