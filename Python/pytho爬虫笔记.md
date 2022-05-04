

# 测试urllib

```python
import urllib.request

#获取一个get请求
# response = urllib.request.urlopen("http://www.baidu.com")
# print(response.read().decode('utf-8'))  #对获取到的网页源码进行utf-8解码


#获取一个post请求
# 模拟浏览器用户提交请求
# import urllib.parse
# data = bytes(urllib.parse.urlencode({"hello":"world"}),encoding="utf-8") 键值对
# response = urllib.request.urlopen("http://httpbin.org/post",data= data)
# print(response.read().decode("utf-8"))

#超时处理
# try:
#     response = urllib.request.urlopen("http://httpbin.org/get",timeout=0.01)
#     print(response.read().decode("utf-8"))
# except urllib.error.URLError as e:
#     print("time out!")


# response = urllib.request.urlopen("http://www.baidu.com")
# #print(response.status)
# print(response.getheader("Server"))

# 模拟所有信息

# url = "http://httpbin.org/post"
# 防止被识别，改成浏览器
# headers = {
# "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.122 Safari/537.36"
# }
# data = bytes(urllib.parse.urlencode({'name':'eric'}),encoding="utf-8")
# req = urllib.request.Request(url=url,data=data,headers=headers,method="POST")
# response = urllib.request.urlopen(req)
# print(response.read().decode("utf-8"))


url = "https://www.douban.com"
headers = {
"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.122 Safari/537.36"
}
req = urllib.request.Request(url=url,headers=headers)
response = urllib.request.urlopen(req)
print(response.read().decode("utf-8"))
```

# 测试BS4

```python

'''
BeautifulSoup4将复杂HTML文档转换成一个复杂的树形结构,每个节点都是Python对象,所有对象可以归纳为4种:

- Tag
- NavigableString
- BeautifulSoup
- Comment
'''


from bs4 import BeautifulSoup

file = open("./baidu.html","rb")
html = file.read().decode("utf-8")
bs = BeautifulSoup(html,"html.parser")

#print(bs.title)
#print(bs.a)
#print(bs.head)

#print(type(bs.head))

#1.Tag  标签及其内容；拿到它所找到的第一个内容


# print(bs.title.string)
#
# print(type(bs.title.string))

#2.NavigableString  标签里的内容（字符串)

#print(bs.a.attrs)



#print(type(bs))
#3.BeautifulSoup   表示整个文档


#print(bs.name)
#print(bs)


# print(bs.a.string)
# print(type(bs.a.string))

#4.Comment  是一个特殊的NavigableString ，输出的内容不包含注释符号


#-------------------------------

#文档的遍历

#print(bs.head.contents)
#print(bs.head.contents[1])

#更多内容，搜索BeautifulSoup文档



#文档的搜索

#(1)find_all()
#字符串过滤：会查找与字符串完全匹配的内容
# t_list = bs.find_all("a")

import re
#正则表达式搜索：使用search（）方法来匹配内容
#t_list= bs.find_all(re.compile("a"))


# 方法  ： 传入一个函数（方法),根据函数的要求来搜索  (了解）
# def name_is_exists(tag):
#     return tag.has_attr("name")
#
# t_list = bs.find_all(name_is_exists)
#
#
# for item in t_list:
#     print(item)

#print(t_list)


#2.kwargs   参数

#t_list= bs.find_all(id="head")
#t_list = bs.find_all(href="http://news.baidu.com")
#t_list = bs.find_all(class_=True)

# for item in t_list:
#     print(item)


#3.text参数

#t_list= bs.find_all(text = "hao123")
#t_list = bs.find_all(text =["hao123","地图","贴吧"])

#t_list = bs.find_all(text = re.compile("\d"))  #应用正则表达式来查找包含特定文本的内容（标签里的字符串）


#4.limit 参数

# t_list = bs.find_all("a",limit=3)
#
# for item in t_list:
#     print(item)


#css选择器

#t_list = bs.select('title')   #通过标签来查找

#t_list = bs.select(".mnav")     #通过类名来查找

#t_list = bs.select("#u1")   #通过id来查找

#t_list = bs.select("a[class='bri']")  #通过属性来查找

# t_list = bs.select("head > title")  #通过子标签来查找

t_list = bs.select(".mnav ~ .bri")

print(t_list[0].get_text())

# for item in t_list:
#     print(item)


```



