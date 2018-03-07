### es6常见用法

1.变量声明const和let：
-

**es5写法：**

es6以前声明变量是用var，无论声明在何处，都会被视为声明在函数最顶部，不在函数内则会声明为全局变量，这就是函数变量提升(变量提升：函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部。)，例如：

```js
var bool = true;
function aa() {
	console.log(bool); // true
    if(bool) {
        var test = 'hello man'; 
    } else {
        console.log('结果0：'+test); // bool为false时，值为undefined
    }
    console.log('结果1：'+test); // bool为false时，值为undefined,bool为true时，值为hello man
}
aa();
console.log('结果2：'+test); // 变量没有初始化，所以浏览器报错test is not defined
```

以上代码实际上是：

```js
var bool;
bool = true;
function aa() {
	var test;
	console.log(bool); // true
    if(bool) {
        test = 'hello man';
    } else {
        console.log('结果0：'+test);
    }
    console.log('结果1：'+test);
}
aa();
console.log('结果2：'+test);
```

**es6写法：**

我们通常用let表示变量、const表示常量。let和const都是块级作用域，理解块级作用域：

* 在一个函数内部
* 在一个代码块内部

*Note：*可以说是｛｝花括号内的代码块即为let和const的作用域

代码如下：

```js
var bool = true;
function aa() {
	console.log(bool); // true
    if(bool) {
        let test = 'hello man'; 
    } else {
        console.log('结果0：'+test); // bool为false时，值为undefined
    }
    console.log('结果1：'+test); // 此时报错test is not defined
}
aa();
console.log('结果2：'+test); // 结果1报错，以后的代码都不运行，导致结果2不运行，实际上结果2也是要报错提示test is not defined
```

*Note：*let的作用域是它所在的当前代码块，但是不会被提升到当前函数的最顶部

关于const定义常量是不可变的，例如：

```js
const name = 'roko';
name = 'joy';	// 再次赋值会报错Assignment to constant variable
```

说一道面试题：

```js
var funcs = []
for (var i = 0; i < 10; i++) {
    funcs.push(function() { console.log(i) })
}
funcs.forEach(function(func) {
    func()
})

代码执行输出10次结果都是10
```

解决办法有：

1.
```js
var funcs = []
for (let i = 0; i < 10; i++) {
    funcs.push(function() { console.log(i) })
}
funcs.forEach(function(func) {
    func()
})

执行结果为1、2、3、4、5、6、7、8、9
```

2.
```js
var funcs = []
for (var i = 0; i < 10; i++) {
	(function(i){	    		
		funcs.push(function() { console.log(i) })
	})(i)
}
funcs.forEach(function(func) {
    func()
})

执行结果为1、2、3、4、5、6、7、8、9
```

模版字符串
-

es5前都是用“+”来拼接字符串，有点不雅观和累赘，es6则用${}来替代“+”的拼接方式了，好处有以下几个：

1.基本的字符串格式化。将表达式嵌入字符串中拼接，代码如下：

```js
// es5
var name = 'roko'
console.log('my name is ' + name) // my name is roko

// es6
const name = 'roko';
console.log(`my name is ${name}`) // my name is roko
```

2.es5时我们常用反斜杠(\\)来做多行字符串或字符串一行一行拼接。es6则用引号（\`\`）直接搞定还可以可以保留空格，代码如下：

```js
// es5
var template0 = "<div>\
    <span>hello world</span>\
</div>";
console.log(template0)

// es6
const template1 = `<div>
    <span>hello world</span>
</div>`
console.log(template1)
```

关于字符串的es6还有几个常用的方法，代码如下：

```js
// includes：判断是否包含然后返回布尔值
let str1 = 'abcdefg';
console.log(str1.includes('bc')) // true

// repeat：获取字符串重复n次,如果重复的次数是小数点则需要取证处理如：Math.floor(n)
let str2 = 'ha'
console.log(str2.repeat(3)) // hahaha
```

函数
-

在es5中我们给函数定义参数默认值是这样的：

```js
function action(num) {
    num = num || 200
    // 当传入num时，num为传入的值
    // 当没传入参数时，num即有了默认值200
    return num
}
console.log(action(10)) // 10
console.log(action()) // 200
console.log(action(0)) // 200
```

*Note：*当num传入值为0（false）时，此时打印出来的值为200跟我们实际要的效果不一样

es6为参数提供了默认值。在定义函数时便初始化了这个参数，以便在参数没有被传递进去时使用，代码如下：

```js
function action(num = 100) {
	console.log(num)
}
action(5) // 5
action(0) // 0
action() // 100
```

箭头函数
-

箭头函数最直观的三个特点：

* 不需要function关键字来创建函数
* 省略return关键字
* 继承当前上下文的this关键字

代码如下：

```js
// 例如：
[1,2,3,5].map(x => console.log(x + 1));

// 等同于
[1,2,3,5].map((function(x){
	return console.log(x + 1)
}).bind(this))


```

当函数有且仅有一个参数的时候可以省掉括号，函数有且仅有一个一个表达式时可以省略{},代码如下：

```js
var people = name => `hi ${name}`
console.log(people('roko'))
```

作为参考：

```js
var people = (name, age) => {
	const fullName = 'H-${name} is ${age}'
	return fullName
}
console.log(people('roko', 20))
```

*Note：*缺少()或{}就会报错

拓展的对象功能
-

es6以前我们对象都是以键值对的形式书写的，是可能出现键值对重名的。例如：

```js
// es5
function people1(name, age) {
	return {
		name: name,
		age: age
	}
}
console.log(people1('roko',20))

// es6
let people2 = (name, age) => {
	return {
		name,
		age
	}
}
console.log(people2('joy',21))
```

es6的对象字面量赋值语法相比于es5时有所改进的，代码如下：

```js
// es5
var people1 = {
	name: 'roko',
	getName: function() {
		console.log(this.name)
	}
}
people1.getName()

// es6
const people2 = {
	name: 'joy',
	getName() {
		console.log(this.name)
	}
}
people2.getName()
```

更方便的数据访问--解构
-

数组和对象是js中最常见也是最重要表示形式。为了简化提取信息，es6新增了解构，这是将一个数据结构分解为更小的部分的过程,代码如下：

```js
// es5
var people1 = {
	name: 'roko',
	age: 20
}
var name = people1.name
var age = people1.age
console.log(name + '---' + age)

// es6
// 对象
const people1 = {
	name: 'joy',
	age: 21
}
const {name, age} = people1
console.log(`${name}---${age}`)
const people3 = {
	name: 'kk',
	age: 44,
	getName() {
		return `${this.name}---${this.age}`
	}
}
const {name, age, getName} = people3
console.log(`${name}---${age}---${getName()}`)

// 数组
const color = ['red', 'blue']
const [color1, color2] = color
console.log(`${color1}---${color2}`)

```

