---
Title: 编写高质量Javascript的要点-Review深入理解Javascript系列(一)
date: 2017-6-9 14:14:20
status: public
---

### 知识点!!!

#### 最小全局变量Minimizing Global

全局变量命名易与第三方的脚本引起冲突,所以尽可能少的使用全局变量是很重要的.相关策略有:命名空间模式或是函数立即自动执行，但是要想让全局变量少最重要的还是始终使用var来声明变量。

#### 几种不经意之间声明的全局变量示例(反例)

```js
//第一种
function sum(x,y){
    result = x+y;//隐式声明了全局变量result
    return result;
}

//第二种
function foo(){
    //这边是首先声明了全局变量b,赋值0,又将b的引用指向a;
    var a=b=0;
}
```

#### 隐式全局变量与明确定义的全局变量的差别

> 通过`var`声明的全局变量,通过`delete`操作符是无法删除的

> 没有通过`var`声明的隐式全局变量,可以通过`delete`删除

注:
在技术上，隐式全局变量并不是真正的全局变量，但它们是全局对象的属性。属性是可以通过delete操作符删除的，而变量是不能的

#### 全局对象的访问

在浏览器中,全局对象可以通过`window`的属性来访问.

在任何层级的作用域中访问全局对象:

```js
var global = (function(){
    return  this;
}());
//这个方法可以随时访问全局对象,因为其被当做函数调用了,this总是指向全局对象.
```

#### 声明变量的小技巧:单`var`形式

举个栗子吧:

```js
function foo(){
    var a=1,
        b=2,
        c=a+b,
        obj={},
        $dom = document.getElementById('demo'),
        k,m;
    //....
}
```

#### 预解析:`var`的散布问题(Hosting:A Problem with Scattered vars)

对于JavaScript，只要你的变量是在同一个作用域中（同一函数），它都被当做是声明的，即使是它在var声明前使用的时候。

栗子:

```js
a = 'hehehe';
function foo(){
    console.log(a);//undefined
    var a = 'abcd';//a在此被当作了局部变量,虽然是在之后声明的
    console.log(a);//abcd
}

foo();
```

Javascript代码执行分为两个阶段:

> 1.变量,函数声明以及正常格式的参数创建,这是一个解析和进入上下文的阶段
> 2.代码执行,函数表达式和不合格的标识符被创建.

#### `for`循环的优化(For Loops)

`HTMLCollections`指`DOM`方法返回的对象.如:

```js
document.getElementsByName();
document.getElementsByClassName();
document.getElementsByTagName();
document.images;
document.links;
document.forms;
document.forms[0].elements;//页面第一个表单的所有域
```

HTML集合,在每次访问其长度时会实时的查询`DOM`,`DOM`操作相对来说比较昂贵.

```js
//优化的for循环写法,缓存数组的长度.
for(var i=0,len=array.length;i<len;i++){
    //...
}
```


还有进一步的微操作:

* 少了一个变量
* 向下数到0，通常更快，因为和0做比较要比和数组长度或是其他不是0的东西作比较更有效率

```js

var i,myArray=[];
for(i=myArray.length;i--){

}

var myarray = [],
    i = myarray.length;
while (i–-) {
   // 使用myarray[i]做点什么
}

```


#### `for-in`循环(for in loops)

