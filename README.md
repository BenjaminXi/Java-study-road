# front-end-written-examination
##校招笔试总结
## <a name='HTTP'>HTTP</a>
####cookie是什么？cookie的作用？
* Cookie：当前识别用户，实现持久会话的最好方式。Cookie可以笼统地分为两类：会话cookie和持久cookie。前者为临时cookie，记录了用户访问站点时的设置和偏好，用户退出浏览器时，会话cookie就删除了。持久cookie的生存时间更长一些，存储在硬盘上，浏览器退出，计算机重启时仍然存在。通常会用持久cookie维护某个用户周期性访问的站点的站点的配置文件或登录名。这两者的唯一区别是它们的过期时间。
* Cookie的作用：当用户首次访问web服务器时，web服务器对用户一无所知。Web服务器会希望用户再次访问，所以给用户拍上一个独有的cookie，这样以后就可以识别出用户了。Cookie中包含了由name=value这样的信息列表，通过set-cookie HTTP响应首部将其贴到用户身上。Cookie通常包含一个服务器为了进行跟踪而产生的识别码。浏览器会记住从服务器返回的set-cookie首部中cookie内容，并将cookie集存储在浏览器的cookie数据库中，将来用户返回同一站点时，浏览器会挑中那个服务器贴到用户身上的那些cookie，并在一个cookie请求首部中将其传回去。

## <a name='Javascript'>Javascript</a>
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
