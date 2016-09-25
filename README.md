# front-end-written-examination
##校招笔试总结
##目录
* [1.HTTP](#HTTP)
	* [1.1Cookie](#cookie)
	* [1.2HTTP请求](#HTTP请求)
* [2.JavaScript](#JavaScript)
* [3.CSS](#CSS)

## <a id="HTTP">HTTP</a>
####<a id="cookie">Cookie是什么？Cookie的作用？</a>
* Cookie：当前识别用户，实现持久会话的最好方式。Cookie可以笼统地分为两类：会话cookie和持久cookie。前者为临时cookie，记录了用户访问站点时的设置和偏好，用户退出浏览器时，会话cookie就删除了。持久cookie的生存时间更长一些，存储在硬盘上，浏览器退出，计算机重启时仍然存在。通常会用持久cookie维护某个用户周期性访问的站点的站点的配置文件或登录名。这两者的唯一区别是它们的过期时间。
* Cookie的作用：当用户首次访问web服务器时，web服务器对用户一无所知。Web服务器会希望用户再次访问，所以给用户拍上一个独有的cookie，这样以后就可以识别出用户了。Cookie中包含了由name=value这样的信息列表，通过set-cookie HTTP响应首部将其贴到用户身上。Cookie通常包含一个服务器为了进行跟踪而产生的识别码。浏览器会记住从服务器返回的set-cookie首部中cookie内容，并将cookie集存储在浏览器的cookie数据库中，将来用户返回同一站点时，浏览器会挑中那个服务器贴到用户身上的那些cookie，并在一个cookie请求首部中将其传回去。

####<a id ="HTTP请求">HTTP请求的全过程。</a>
1. 浏览器从URL中解析出服务器的主机名；
2. 浏览器从将主机名转换为IP地址；
3. 浏览器将端口号从URL中解析出来；
4. 浏览器建立一条与web服务器的TCP连接；
5. 浏览器向服务器发送一条HTTP请求报文；
6. 服务器向浏览器回送一条HTTP响应报文；
7. 关闭连接，浏览器显示文档。

####HTTP请求头信息。
HTTP报文包含三部分：起始行，头部和主体。HTTP报文分为两类：请求报文和响应报文。起始行包含方法、状态码、原因短语和版本号。首部向请求和响应报文添加了一些附加信息，本质上，是一些名/值对的列表。首部可以分为以下几类：通用首部、请求首部、响应首部、实体首部和扩展首部。

请求首部用于说明谁在发送请求、请求来自何处、或者客户端的喜好及能力，浏览器根据请求首部，为客户端提供更好的响应。
* 信息性首部中有client-IP、From、Host、Refer、UA-Color、UA-CPU、UA-DISP、UA-OS、UA-Pixels、User-Agent。
* Accept首部为客户端提供了将其喜好和能力告知服务器的方式，包括Accept、Accept-Charset、Accept-Encoding、Accept-Language、TE。
* 条件请求首部为请求加上了限制，包括：Except、If-Match、If-Modified-Since、If-None-Match、If-Range、If-Unmodified-Since、Range。
* 安全请求首部对请求进行质询/响应认证，包括：Authorization、Cookie、Cookie2。
* 代理请求首部包括：Max-Forward、Proxy-Authorization、Proxy-Connection。

## <a id='JavaScript'>JavaScript</a>
####Json数据如下：person = [{name:"甲",dateOfBirth:"1991-01-01",sex:"male"},{name:"乙",dateOfBirth:"1992-01-01",sex:"female"},{name:"丙",dateOfBirth:"1989-08-21",sex:"female"},{name:"丁",dateOfBirth:"1991-06-22",sex:"female"}];，筛选出sex为female的数据。
```
var person = [{name:"甲",dateOfBirth:"1991-01-01",sex:"male"},{name:"乙",dateOfBirth:"1992-01-01",sex:"female"},{name:"丙",dateOfBirth:"1989-08-21",sex:"female"},{name:"丁",dateOfBirth:"1991-06-22",sex:"female"}];
var girls = person.filter(function(item){
  return item.sex =="female";
})
console.log(girls);
```
####Json数据同上，从筛选出的girls中按照dateOfBirth排序
```
girls.sort(function(a,b){return a.dateOfBirth>b.dateOfBirth?1:-1;});
console.log(girls);
```
####求12589到25689之间的整数，满足各位数字之和为5的倍数的个数。
```
var count =0;
for(var i=12589;i<=25899;i++){
	var result=0;
	var a =i%10;
	var b =Math.floor((i/10)%10);
	var c =Math.floor((i/100)%10);
	var d =Math.floor((i/1000)%10);
	var e =Math.floor(i/10000);
	result = a+b+c+d+e;
	if(result%5==0)
		count++;
}
console.log("总数为"+count);
```
####请把以下用于连接字符串的JavaScript代码修改为更高效的方式
```
var htmlString = ‘ < div class=”container” > ’ + ‘ < ul id=”news-list” > ’;
for (var i = 0; i < NEWS.length; i++) {
htmlString += ‘ < li > < a href=”’ +NEWS[i].LINK + ‘” > +NEWS[i].TITLE + ‘ < /a > < /li > ’;
}
htmlString += ‘ < /ul > < /div > ’;
```
分析：考点1-JavaScript的字符串连接机制；考点2-NEWS.length需要缓存，不然每次循环都要重新计算一次length。
```
var htmlString=[];
htmlString.push(‘ < div class=”container” > ’ + ‘ < ul id=”news-list” > ’);
for(var i = 0, len = NEWS.length; i < len; i++){
var news = NEWS[i];
htmlString.push('<li><a href="'+ news.LINK+'">'+ news.TITLE+'</a></li>');
}
htmlString=htmlString.join(""); 
```
####尝试实现注释部分的Javascript代码，可在其他任何地方添加更多代码（如不能实现，说明一下不能实现的原因）：
```
var Obj = function(msg){
    this.msg = msg;
    this.shout = function(){
        alert(this.msg);
    }  
    this.waitAndShout = function(){
        //隔五秒钟后执行上面的shout方法
    }
}
```
解：
```
var Obj = function(msg){
    this.msg = msg;
    this.shout = function(){
        alert(this.msg);
    };    
    this.waitAndShout = function(){
        var that = this;
        setTimeout(function(){that.shout();},5000);
        //隔五秒钟后执行上面的shout方法
    }
    return this;
}
Obj("shouting").waitAndShout();
```
ps：在[jsbin](http://jsbin.com)中只能显示一次，无法循环，待定。
#### 完成后续代码，计算两个数组的交集，并指出该算法的时间复杂度和空间复杂度。
```
var arr1=[1,2,3,3,4,2,3,5];
var arr2=[3,4,4,3,5,7,8];
var arr3=[];
//计算arr1和arr2两个数组的交集，将结果保存到arr3中
console.log(arr3);
```
解：
```
var arr1=[1,2,3,3,4,2,3,5];
var arr2=[3,4,4,3,5,7,8];
var arr3=[];
var len1=arr1.length,len2=arr2.length;
for(var i=0;i<len1;i++){
	for(var j=0;j<len2;j++){
		if(arr1[i]==arr2[j] && arr3.indexOf(arr1[i])==-1){
		arr3.push(arr1[i]);}
	}
}
//计算arr1和arr2两个数组的交集，将结果保存到arr3中
console.log(arr3);
```
时间复杂度为O(len1*len2)
####求下列程序输出
```
var a = function(){
  this.b=1
}
a();
console.log(b);
a.b=2;
a.prototype.b=3;
var c = new a();
console.log(c.b);
```
输出为:1 1 
####求下列程序输出
```
a=1,b=2,c=2;
while(a<b<c){
  t=a;a=b;b=t;c--;
}
console.log(a,b,c);
```
分析：1<2<2,先计算1<2为true，返回1,再计算1<2,a与b值对调，a=2，b=1，c=1。再循环，条件再次满足，a=1，b=2，c=0。输出：1 2 0。

## <a id="CSS">CSS</a>
####CSS选择符有哪些？
1. 元素选择器，如html,p,h2
2. 逗号选择器，包含多个不同的选择器
3. 通配选择器（*）
4. 类选择器（.classname），多类选择器（.classname1.classname2）
5. ID选择器（#），一个ID只能在文档中出现一次
6. 属性选择器
	* 单个属性选择，如a[href]
	* 多个属性选择如a[href][title]，选择多个属性的a元素
	* 属性值选择，如planet[moos="1"]
	* 部分属性值选择，
		* 元素选择，如p[class~="warning"]，选择class属性中包含warning的元素
		* 子串匹配属性选择，如[foo^="bar"],foo属性以bar开头的元素；[foo$="bar"],foo属性以bar结尾的元素；[foo*="bar"]，foo属性包含bar子串的元素
		* 特定属性选择，如[lang|="en"]，lang属性以en-开头的所有元素
7. 后代选择器，用空格来表示，解释为“...作为...的一部分”，但必须从右向左，如h1 em解释为em作为h1的一部分
8. 子代选择器，用大于号表示。
9. 兄弟元素选择器，如 h1+p 读作紧接在h1元素后面出现的所有段落，h1要与p元素有相同的父元素。
10. 伪类选择器，（冒号）
	* 链接伪类，如 a:link和a:visited
	* 动态伪类，可以应用到任何元素，有3个动态伪类，":focus",":hover",":active"
	* 结合使用伪类，如 a:link:hover
11. 伪元素选择器，（冒号）
	* 设置首字母样式，p:first-letter
	* 设置第一行样式，p:first-line
	* 设置之前，h1:before
	* 设置之后，h2:after

####选择器的优先级如何计算？
同一个元素可以使用两个或多个规则来选择，每个规则都有自己的选择器，只有规则的特殊性更高才能胜出，选择器的具体特殊性如下：
* 内联样式：1,0,0,0
* 对于选择器给定的ID属性值：0,1,0,0
* 类，属性选择，伪类：0,0,1,0
* 元素和伪类：0,0,0,1

如果特殊性相等的两个规则应用到同一个元素，遵循以下规则：
1. 按权重和来源排序：读者的!important > 创作人员的!important > 创作人员的正常声明 > 读者的正常声明 > 用户代理声明
2. 按特殊性排序，较高特殊性的权重大于较低特殊性的的元素
3. 按顺序排序，声明在样式表或文档中越后出现，权重越大。
