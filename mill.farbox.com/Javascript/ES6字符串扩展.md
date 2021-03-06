### 字符串的Unicode表示法
目测用的比较少,略过.

### codePointAt()
一个常识:
> JavaScript内部，字符以UTF-16的格式储存，每个字符固定为2个字节。对于那些需要4个字节储存的字符（Unicode码点大于0xFFFF的字符），JavaScript会认为它们是两个字符。

`codePointAt`方法会正确返回32位的UTF-16字符的码点

### String.fromCodePoint()
> 用于从码点返回对应字符,ES6支持可以识别大于`0xFFFF`的字符

### 字符串遍历器的接口
> 特点:除了遍历字符串，这个遍历器最大的优点是可以识别大于0xFFFF的码点，传统的for循环无法识别这样的码点。

### at()
> 类似`charAt()`,只是添加了可以是吧Unicode编码大于`0xFFFF`的字符

### normailze()
略

### includes(),startWith(),endsWith()

* `includes()`:返回true/false,表示是否找到了参数的字符串
* `startsWith()`:返回true/false,表示字符串是否在源字符串的头部
* `endsWith()`:返回true/false,表示字符串是否在源字符串的尾部

### repeat()
`repeat()`方法返回一个字符串,表示将原字符串重复n次,参数如果是小数会被取整,负数或者Infinity会报错


### padStart(),padEnd()
字符串头部或尾部补全功能,接收两个参数,第一个参数表示字符串的长度,第二个参数表示补全的字符串,
如果第二个参数不传,则自动补全空字符串

### 模板字符串
1. 可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。
2. 模板字符串中嵌套变量使用`${}`包裹变量,可进行变量运算和对象的引用,功能很是强大.
3. 模板字符串中还可以调用函数如:`${fn()}`
4. 模板嵌套

### 标签模板
> 它可以紧跟在一个函数名后面，该函数将被调用来处理这个模板字符串。这被称为“标签模板”功能

例如:
```js
alert`123`
```

### String.raw()
> 往往用来充当模板字符串的处理函数，返回一个斜杠都被转义（即斜杠前面再加一个斜杠）的字符串，对应于替换变量后的模板字符串

参考:
* [ES6](http://es6.ruanyifeng.com/#docs/string)
* [code](http://jsbin.com/peferox/edit?html,js,console)
