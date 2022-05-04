### Javascript：直接写入HTML输出流

### Javascript：对事件的反应

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    
</head>
<body>
    <!-- 直接插在HTML代码中 -->
    <script>
        document.write("html文本输入流");
        function myfun(){
            x=document.getElementById("demo");
            x.innerHTML="我就是改变之后的内容"
        }
    </script>
    <!-- 对事件的反应 -->
    <button type="button" onclick="alert('hello world！')">点击</button>
    <br>
    <p id="demo">
        看我看我
    </p>
    <button type="button" onclick="myfun()">点击有惊喜</button>
</body>
</html>
```



**也叫脚本语言，外部脚本不能包含script标签**



## JavaScript输出

**1.使用window.alert();你可以弹出警告框来显示数据：**

```c
window.alert(1+2);
```



**2.操作HTML元素**

如需从 JavaScript 访问某个 HTML 元素，您可以使用 document.getElementById(*id*) 方法。

请使用 "id" 属性来标识 HTML 元素，并 innerHTML 来获取或插入元素内容：

```javascript
document.getElementById("demo").innerHTML="我就是修改之后的内容";
document.getElementById("demo").innerHTML="段落已修改。";
```



**3.写入HTML文档**

```
dcument.write();
```



**4.输出到控制台**

```
console.log();
```



JavaScript的命名的方法采用的都是驼峰命名法。



## JavaScript对象

```javascript
var person = {
        firstName:"John",
        lastName:"Doe",
        age:50,
        eyeColor:"blue"
};
```

**访问对象属性**

```
person.lastName;
person["lastName"];
```

**不要创建 String 对象。它会拖慢执行速度，并可能产生其他副作用：**



JavaScript的比较运算符，数据的类型是被忽略的。

‘==’ 

‘===’强等于





## DOM

documen 代表当前的页面。





##  jQuery、

$(选择器).action()



直接调用库里的事件。



```
1. 30-seconds-of-code 网站：https://github.com/30-seconds/30-seconds-of-code
2. 33-js-concepts 网站：https://github.com/leonardomso/33-js-concepts
3. javascript-questions  网站:https://github.com/lydiahallie/javascript-questions
4. JavaScript 30  网站：https://github.com/wesbos/JavaScript30
5. ES6 入门教程 网站：https://es6.ruanyifeng.com/
6. JavaScript 教程 网站：https://wangdoc.com/javascript/
7. MDN  网站：https://developer.mozilla.org/zh-CN/
8. clean-code-javascript 网站：https://github.com/ryanmcdermott/clean-code-javascript
9. TypeScript 入门教程 网站：https://ts.xcatliu.com
10. w3school   网站：https://www.w3school.com.cn/js/index.asp
```

