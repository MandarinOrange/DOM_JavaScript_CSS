# DOM_JavaScript_CSS
DOM编程、JavaScript和CSS的交互

# DOM
是Document Object Model（文档对象模型）的缩写。DOM把整个HTML看成是一个由节点组成“树状”的文档，通过DOM可以动态改变文档内容。
# DOM常用操作
1、查看节点
1）访问指定节点的方法
getElementById( ) ：返回一个节点对象
getElementsByName( )：返回多个（节点数组）
getElementsByTagName( ) ：返回多个（节点数组）

2）查看/修改属性节点
getAttribute("属性名") 
setAttribute("属性名","属性值") 
注意：也可以使用   元素.属性名 来使用属性或给属性赋值

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>使用getAttribute获取属性值</title>
    <style type="text/css">
        img {
            border: 0px;
            float: left;
            padding: 3px;
        }

        body {
            margin: 0px;
            font-size: 12px;
            line-height: 20px;
        }

        input {
            margin-top: 5px;
        }
    </style>
    <script type="text/javascript">
        function getPath(){
            var img = document.getElementById("fruit");//获取图片节点
            var path = img.getAttribute("src");//获取图片src的属性值
            alert(path);
        }

        function showLoveFruits(){
            var enjoys = document.getElementsByName("enjoy");
            var result = "";
            for(var i=0;i<enjoys.length;i++){
                if(enjoys[i].checked){
                    result += enjoys[i].value+"\n";
                }
            }
            alert(result);
        }

        function setPath(){
            var img = document.getElementById("fruit");//获取图片节点
            img.setAttribute("src","images/grape.jpg");
        }
    </script>
</head>

<body>
    <img src="images/fruit.jpg" alt="水果图片" aa="bb" id="fruit"/>

    <h1 id="love">选择你喜欢的水果：</h1>
    <input name="enjoy" type="checkbox" value="apple"/>苹果
    <input name="enjoy" type="checkbox" value="banana"/>香蕉
    <input name="enjoy" type="checkbox" value="grape"/>葡萄
    <input name="enjoy" type="checkbox" value="pear"/>梨
    <input name="enjoy" type="checkbox" value="watermelon"/>西瓜
    <br/>
    <input name="btn" type="button" value="显示图片路径" onclick="getPath()"/>
    <br/>
    <input name="btn" type="button" value="喜欢的水果" onclick="showLoveFruits()"/>
    <br/>
    <input name="btn" type="button" value="改变图片" onclick="setPath()"/>
</body>
</html>

```

3）层次关系节点
parentNode：获取父节点
firstChild：获取第一个子节点
lastChild：获取最后一个子节点
firstElementChild：获取第一个元素节点
lastElementChild：获取最后一个元素节点

页面加载后，用node.js清空空白节点：
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>根据层次关系查找节点</title>
  <script type="text/javascript" src="node.js"></script>
  <script type="text/javascript">
    function showText(){
      var table = document.getElementById("myTable");//获取table节点
      var name = table.lastChild.lastChild.firstChild.innerHTML;
      alert(name);
    }

    window.onload = function(){
      var b = document.getElementById("myBody");
      clearWhitespace(b);//清空节点
    }
  </script>
</head>

<body id="myBody">
<table width="200" border="1" id="myTable">
  <thead>
    <tr>
      <td>姓名</td>
      <td>课程</td>
      <td>成绩</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>欧阳兰</td>
      <td>语文</td>
      <td>88</td>
    </tr>
    <tr>
      <td>白杨</td>
      <td>数学</td>
      <td>96</td>
    </tr>
  </tbody>
</table>

<input type="button" name="" value="最后一行第一个单元格内容" onclick="showText()" />
</body>
</html>

```
不用node.js清空空白节点，而使用lastElementChild：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>根据层次关系查找节点</title>
  <script type="text/javascript">
    function showText(){
      var table = document.getElementById("myTable");//获取table节点
      var name = table.lastElementChild.lastElementChild.firstElementChild.innerHTML;
      alert(name);
    }
  </script>
</head>

<body id="myBody">
<table width="200" border="1" id="myTable">
  <thead>
    <tr>
      <td>姓名</td>
      <td>课程</td>
      <td>成绩</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>欧阳兰</td>
      <td>语文</td>
      <td>88</td>
    </tr>
    <tr>
      <td>白杨</td>
      <td>数学</td>
      <td>96</td>
    </tr>
  </tbody>
</table>

<input type="button" name="" value="最后一行第一个单元格内容" onclick="showText()" />
</body>
</html>

```

2、创建和增加节点
createElement(nodeName)：创建节点,nodeName表示节点名称 
appendChild(node)：末尾追加方式插入node节点
insertBefore(nodeA,nodeB)：在nodeB节点前插入nodeA节点
cloneNode(boolean)：克隆节点   
注意：参数为true表示节点及子节点都会被克隆   参数为	false不会克隆子节点

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<title>增加节点</title>
	<script type="text/javascript">
		function addPic(){
			var img = document.createElement("img");//创建图片节点
			img.setAttribute("src","images/newimg.jpg");//设置图片的src属性值

			var fruitImg = document.getElementById("sixty1");
			document.body.insertBefore(img,fruitImg);
		}

		function copyPic(){
			var fruitImg = document.getElementById("sixty1");
			var cloneImg = fruitImg.cloneNode(false);//浅克隆
			document.body.appendChild(cloneImg);
		}
	</script>
</head>

<body>
	<h2>喜欢的水果</h2>
	<input id="b1" type="button" value="增加一幅图片" onclick="addPic()"/>
	<input id="b2" type="button" value="复制原图" onclick="copyPic()"/><br />

	 <img src="images/sixty1.jpg" id="sixty1" alt="水果"/>
	<img src="images/sixty2.jpg" id="sixty2" alt="果篮" />

</body>
</html>

```

3、删除和替换节点
removeChild()：删除节点  
replaceChild(nodeA,nodeB) ：替换节点，nodeA节点替换nodeB节点

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title>操作表格</title>
    <style type="text/css">
        body {
            font-size: 13px;
            line-height: 25px;
        }

        table {
            border-top: 1px solid #333;
            border-left: 1px solid #333;
            width: 300px;
        }

        td {
            border-right: 1px solid #333;
            border-bottom: 1px solid #333;
        }

        .center {
            text-align: center;
        }

    </style>
    <script type="text/javascript" src="node.js"></script>
    <script type="text/javascript">
        //清除空白节点
        window.onload = function () {
            clearWhitespace(document.body);
        }
        //添加行
        function addRow(){
            var newTr = document.createElement("tr");//创建一个行节点
            var newTd1 = document.createElement("td");
            var newTd2 = document.createElement("td");
            newTd1.innerHTML = "幸福从天而降";
            newTd2.innerHTML = "&yen;26.00";
            newTd2.setAttribute("class","center");//加样式

            newTr.appendChild(newTd1);//将td添加到tr中
            newTr.appendChild(newTd2);

            var table = document.getElementById("myTable");//获取表格节点
            var lastTr = table.firstChild.lastChild;//获取最后一个tr
            table.firstChild.insertBefore(newTr,lastTr);//table.firstChild获取的是tbody
        }
        //删除行
        function delRow(){
            var table = document.getElementById("myTable");
            var trs = table.firstElementChild.getElementsByTagName("tr");
            var delTr = trs[1];//获取第二行
            table.firstChild.removeChild(delTr);
        }
        //修改标题样式
        function updateTitle(){
            var table = document.getElementById("myTable");
            var firstTr = table.firstChild.firstChild;//获取第一行
            firstTr.setAttribute("class","center");
            firstTr.setAttribute("bgcolor","gray");
        }
        //复制行
        function copyRow(){
            var table = document.getElementById("myTable");
            var lastTr = table.firstChild.lastChild;//获取最后一行
            var cloneTr = lastTr.cloneNode(true);
            table.firstChild.appendChild(cloneTr);
        }
        //替换最后一行
        function replaceRow(){
            var newTr = document.createElement("tr");//创建一个行节点
            var newTd1 = document.createElement("td");
            var newTd2 = document.createElement("td");
            newTd1.innerHTML = "水浒传";
            newTd2.innerHTML = "&yen;53.00";
            newTd2.setAttribute("class","center");//加样式

            newTr.appendChild(newTd1);//将td添加到tr中
            newTr.appendChild(newTd2);

            var table = document.getElementById("myTable");
            var lastTr = table.firstChild.lastChild;//获取最后一行
            table.firstChild.replaceChild(newTr,lastTr);//新行将最后一行替换
        }
    </script>

</head>

<body>
<table border="0" cellspacing="0" cellpadding="0" id="myTable">
    <tr>
        <td>书名</td>
        <td>价格</td>
    </tr>
    <tr>
        <td>看得见风景的房间</td>
        <td class="center">&yen;30.00</td>
    </tr>
    <tr>
        <td>60个瞬间</td>
        <td class="center">&yen;32.00</td>
    </tr>
</table>
<input name="b1" type="button" value="增加一行" onclick="addRow()" />
<input name="b2" type="button" value="删除第二行" onclick="delRow()" />
<input name="b3" type="button" value="修改标题样式" onclick="updateTitle()" />
<input name="b4" type="button" value="复制最后一行" onclick="copyRow()" />
<input name="b4" type="button" value="替换最后一行" onclick="replaceRow()"/>
</body>
</html>

```
# 常见样式
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801120612355.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801120617166.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)
## 样式表类型
1、行内样式表
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801120708995.png)

2、内嵌样式表
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801120713455.png)

3、外部样式表
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801120721819.png)
## JavaScript访问样式的常用方法
在网页中，我们经常会使用JavaScript来灵活的改变元素的样式，增加用户的体验。
访问样式的常用步骤如下：
1、使用getElement系列方法访问元素
2、改变样式属性：
1）style属性
语法：HTML元素.style.样式属性＝"值"
例如：

```javascript
document.getElementById("titles").style.backgroundColor="#ff0000";
```

2）className属性
语法：HTML元素.className=”样式选择器名称”
例如：

```javascript
document.getElementById("titles").className="over";
```
鼠标移上改变图片边框样式：
```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=gb2312"/>
    <title>改变图片边框样式</title>
    <style type="text/css">
        .out {
            border: solid 1px #eeeeee;
        }

        .over {
            border: solid 2px #F60;
        }
    </style>
</head>

<body>
<table border="0" cellspacing="0" cellpadding="0">
    <tr>
        <td><img src="images/new_01.jpg" class="out" onmouseover="this.className='over'" onmouseout="this.className='out'"  /></td>
        <td><img src="images/new_02.jpg" class="out" onmouseover="this.className='over'" onmouseout="this.className='out'" /></td>
        <td><img src="images/new_03.jpg" class="out" onmouseover="this.className='over'" onmouseout="this.className='out'" /></td>
    </tr>
</table>
</body>
</html>

```

## style常用的属性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801121003789.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801121009121.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)
使用style改变样式：
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title>使用style改变样式</title>
    <style type="text/css">
        li {
            font-size: 12px;
            color: #ffffff;
            background-image: url(images/bg1.gif);
            background-repeat: no-repeat;
            text-align: center;
            height: 33px;
            width: 104px;
            line-height: 38px;
            float: left;
            list-style: none;
        }
    </style>

</head>

<body>
<ul>
    <li onmouseover="this.style.backgroundImage='url(images/bg2.gif)'" onmouseout="this.style.backgroundImage='url(images/bg1.gif)'">资讯动态
    </li>
    <li onmouseover="this.style.backgroundImage='url(images/bg2.gif)'" onmouseout="this.style.backgroundImage='url(images/bg1.gif)'">产品世界
    </li>
    <li onmouseover="this.style.backgroundImage='url(images/bg2.gif)'" onmouseout="this.style.backgroundImage='url(images/bg1.gif)'">市场营销
    </li>
</ul>
</body>
</html>

```
<li>内容过长，我们可以使用javaScript循环来实现：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=gb2312"/>
    <title>使用style改变样式</title>
    <style type="text/css">
        li {
            font-size: 12px;
            color: #ffffff;
            background-image: url(images/bg1.gif);
            background-repeat: no-repeat;
            text-align: center;
            height: 33px;
            width: 104px;
            line-height: 38px;
            float: left;
            list-style: none;
        }
    </style>
    <script type="text/javascript">
        window.onload = function(){
            var lis = document.getElementsByTagName("li");
            for(var i = 0;i<lis.length;i++){
                lis[i].onmouseover = function(){
                    this.style.backgroundImage = 'url(images/bg2.gif)';
                }
                lis[i].onmouseout = function(){
                    this.style.backgroundImage = 'url(images/bg1.gif)';
                }
            }
        }
    </script>

</head>

<body>
<ul>
    <li >资讯动态
    </li>
    <li>产品世界
    </li>
    <li>市场营销
    </li>
    <li>最新技术
    </li>
</ul>
</body>
</html>

```

## 获取样式属性值
获取行内样式的方法：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801121035289.png)

获取内嵌样式的方法
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080112104196.png)


## 获取浏览器滚动条滚动的距离
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801121054146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)

注意：获取scrollTop、scrollLeft属性的时候需要考虑浏览器兼容性问题
谷歌浏览器获取方式：
	document.body.scrollTop
火狐、IE浏览器获取方式：
	document.documentElement.scrollTop

实现浮动广告，使其在屏幕的固定位置，那么广告与顶端的距离 = 初始的top值 + 滚动条滚动的距离：

```html
<!DOCTYPE HTML>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=gb2312"/>
    <title>随鼠标滚动的广告图片</title>
    <style type="text/css">
        #main {
            text-align: center;
        }

        #adver {
            position: absolute;
            left: 50px;
            top: 30px;
            z-index: 2;
        }
    </style>
    <script type="text/javascript">
        var initTop;//广告div初始的top
        var adv;//广告div
        function getInitTop(){
            adv = document.getElementById("adver");//获取广告div节点
            if(adv.currentStyle){//IE浏览器
                initTop = adv.currentStyle.top;
            }else{//火狐、谷歌浏览器....
                initTop = document.defaultView.getComputedStyle(adv,null).top;
            }
            initTop = parseInt(initTop);//去除后面的px
        }

        //浏览器滚动条滚动时触发
        window.onscroll= function(){
            var sTop;//滚动条滚动的距离
            if(document.body.scrollTop){//谷歌浏览器
                sTop = document.body.scrollTop;
            }else{//火狐、IE....
                sTop = document.documentElement.scrollTop;
            }
            adv.style.top = initTop+sTop+"px";
        }
    </script>
</head>
<body onload="getInitTop()">
    <div id="adver" class="adver"><img src="images/adv.jpg"/></div>
    <div id="main"><img src="images/main1.jpg"/><img src="images/main2.jpg"/><img src="images/main3.jpg"/></div>
</body>
</html>

```
项目下载地址：[https://github.com/MandarinOrange/DOM_JavaScript_CSS](https://github.com/MandarinOrange/DOM_JavaScript_CSS)
