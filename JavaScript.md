## <a id='JavaScript'>JavaScript</a>
#### Json数据如下：person = [{name:"甲",dateOfBirth:"1991-01-01",sex:"male"},{name:"乙",dateOfBirth:"1992-01-01",sex:"female"},{name:"丙",dateOfBirth:"1989-08-21",sex:"female"},{name:"丁",dateOfBirth:"1991-06-22",sex:"female"}];，筛选出sex为female的数据。
```
var person = [{name:"甲",dateOfBirth:"1991-01-01",sex:"male"},{name:"乙",dateOfBirth:"1992-01-01",sex:"female"},{name:"丙",dateOfBirth:"1989-08-21",sex:"female"},{name:"丁",dateOfBirth:"1991-06-22",sex:"female"}];
var girls = person.filter(function(item){
  return item.sex =="female";
})
console.log(girls);
```
#### Json数据同上，从筛选出的girls中按照dateOfBirth排序
```
girls.sort(function(a,b){return a.dateOfBirth>b.dateOfBirth?1:-1;});
console.log(girls);
```
#### 求12589到25689之间的整数，满足各位数字之和为5的倍数的个数。
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
#### 请把以下用于连接字符串的JavaScript代码修改为更高效的方式
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
#### 尝试实现注释部分的Javascript代码，可在其他任何地方添加更多代码（如不能实现，说明一下不能实现的原因）：
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
#### 求下列程序输出
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
#### 求下列程序输出
```
a=1,b=2,c=2;
while(a<b<c){
  t=a;a=b;b=t;c--;
}
console.log(a,b,c);
```
分析：1<2<2,先计算1<2为true，返回1,再计算1<2,a与b值对调，a=2，b=1，c=1。再循环，条件再次满足，a=1，b=2，c=0。输出：1 2 0。

#### 输出斐波那契数列前100个数（不使用全局变量）

#### 实现一个函数，实现不定参数输入输出，fn(a)输出为2016-09-26 MYBLOG A；fn(a,b,c)输出2016-09-27 MYBLOG A B C
