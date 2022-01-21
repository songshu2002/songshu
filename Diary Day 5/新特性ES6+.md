## 1.let 命令

let 用来申明变量, 但与传统的var有所不同

- 变量不能重复申明



```csharp
let star='罗志祥';
let star='小猪'  //error
```

- let 有块级作用域



```jsx
{
    let girl='周扬青'
}
console.log(girl) //error
```

- 不存在变量提前



```jsx
console.log(song)   //error
let song='恋爱达人'
```

- 不影响作用域链



```jsx
let school='abc'
function fn(){
    console.log(school) //abc
}
```

在双层for循环中 , 及时计数器相同,也能互不影响



```jsx
let arr = [1,2,3]

for(let i = 0;i < arr.length; i++){
    for(let i = 0;i < arr.length; i++){
        console.log(i)
        //打印9 次 , 一次为012012012
    }
}
```



## 2.const

const 一般用于申明常量

- 一定要赋初始值
- 一般常量使用大写（潜规则）
- 也具有块级作用域(与let一样)
- 常量的值不能修改



```cpp
const a = 1
a = 2 //error
```

但是可以修改原有属性中的属性值



```csharp
const obj = {
  name: '张三',
  car: {
    pace: '100W',
    name: '奥迪rs7',
  },
}

obj.name = '李四' 
```

## 2.解构赋值

ES6 允许按照一定模式从数组和对象中提取值，对变量进行赋值，这被称为解构赋值。

- 数组的解构



```jsx
const F4 = ['小沈阳', '刘能', '赵四', '宋小宝']
let [a, b, c, d] = F4
console.log(a) //小沈阳
console.log(b) //刘能
console.log(c) //赵四
console.log(d)  //宋小宝
```

- 对象的解构



```jsx
const F4 = {
  name: '赵本山',
  age: '不详',
  xiaopin: function () {
    console.log('我可以演小品')
  },
}
let { name, age, xiaopin } = F4
console.log(name) //赵本山
console.log(age) //不详
console.log(xiaopin) //[Function: xiaopin]
```

## 3.模板字符串

- 采用 `` 的形式定义字符串
   申明



```rust
let str = `我也是一个字符串`
console.log(str, typeof str) //我也是一个字符串 string
```

内容中可以直接出现换行符



```xml
let str = `<ul>
            <li>冉海锋</li>
            <li>冉海锋</li>
           </ul>`；
```

变量拼接



```jsx
let lovest = '冉海锋';
let out = `${lovest}是最帅的`;
console.log(out)  //冉海锋是最帅的
```

## 4.对象的简化写法

- ES6允许在大括号里面，直接写入变量和函数，作为对象的属性和方法,这样的书写更加简洁



```jsx
let name = 'aaa'
let change = function () {
  console.log('aaa')
}

const school = {
  name,
  change,
  improve() {
    console.log('bbb')
  },
}
console.log(school)
/**
 * {
    name: 'aaa',
    change: [Function: change],
    improve: [Function: improve]
  }
 */
```

1. 箭头函数

- ES6允许使用箭头（=>）定义函数
   箭头函数中不会创建自己的this,始终指向上一层作用域



```jsx
function A() {
  console.log(this.name)
}

let B = () => {
  console.log(this.name)
}

name = '拉钩教育'
const school = {
  name: 'lagou',
}

//直接调用
A() //拉钩教育
B() //undefined
```

- 不能作为构造实例化对象



```jsx
let A = (name, age) => {
  this.name = name
  this.age = age
}
let me = new A('xiao', 123) //error
```

- 不能使用arguments变量



```jsx
let fn = () => {
  console.log(arguments)
}
fn(1, 2, 3) //error
```

省略小括号，当形参有且只有一个的时候



```jsx
let add = n => {
    return n + 1;
}
```

省略花括号，当代码体只有一条语句的时候，此时return也必须省略



```jsx
let add = n => n+1;
```

6.函数参数默认值

- 可以给形参赋初始值，一般位置要靠后（潜规则）



```jsx
function add(a,b,c=12){
    return a+b+c; 
}
let result = add (1,2);
console.log(result) // 15
```

与解构赋值结合



```jsx
function A({host='127.0.0.1',username,password,port}){
    console.log(host+username+password+port)
}
A({
    username:'ran',
    password:'123456',
    port:3306
})
```

## 7.rest参数



```rust
let fn = (...args) => {
  console.log(args) // [ 1, 2, 3 ]
}

fn(1, 2, 3)
```

rest参数 一般放在最后



```jsx
let fn = (a, ...args) => {
  console.log(a) //1
  console.log(args) // [  2, 3 ]
}

fn(1, 2, 3)
```

如果不是放在最后则会报错



```jsx
let fn = (...args,a) => { //error
  console.log(a) 
  console.log(args)
}
fn(1, 2, 3)
```

可以对rest 参数重新赋值



```rust
let fn = (...args) => {
  args = 1
  console.log(args) //1
}
fn(1, 2, 3)
```

## 8.扩展运算符

- 扩展运算符与rest参数一样 都是用...表示
   扩展运算符是能将数组展开



```jsx
let arr = [1, 2, 3]
console.log(...arr) //1 2 3
```

数组的合并



```jsx
const A = ['aa','bb'];
const B = ['cc','dd'];
const C = [...A,...B];
console.log(C)   //[aa,bb,cc,dd]
```

数组的克隆



```cpp
const A = ['a','b','c'];
const B = [...A];
console.log(B)   //[a,b,c]
```

将伪数组转换为真正的数组



```dart
const A = documents.querySelectorAll('div');
const B = [...A];
console.log(B) // [div,div,div]
```

扩展运算符,也可以用来展开对象和字符串等, 方法与数组类似
 值得注意的是, 扩展运算符在拷贝对象时为部分只有第一层是深拷贝其他层级为浅拷贝



```bash
let person = {
  name: '张三',
  age: 18,
  car: {
    name: '奥迪RS7',
  },
}

let person2 = { ...person }

person.name = '李四'
console.log(person) //{ name: '李四', age: 18, car: { name: '奥迪RS7' } }
console.log(person2) // { name: '张三', age: 18, car: { name: '奥迪RS7' } }

person.car.name = 'AMG c63'
console.log(person) //{ name: '李四', age: 18, car: { name: 'AMG c63' } }
console.log(person2) // { name: '李四', age: 18, car: { name: 'AMG c63' } }
```



## 9. Symbol

ES6引入了一种新的原始数据类型 Symbol，表示独一无二的值。它是JavaScript语言的第七种数据类型，是一种类似于字符串的数据类型。

Symbol特点：

- Symbol的值是唯一的，用来解决命名冲突的问题
- Symbol值不能与其他数据进行运算
- Symbol定义的对象属性不能使用for…in循环遍历，但是可以使用Reflect.ownKeys或来获取对象的所有键名,或者通过Object.getOwnPropertySymbols来获取所有Symbol键名
   创建



```jsx
let s = Symbol('aa');
let s2= Symbol('aa');
console.log(s===s2)   //false

let s3 = Symbol.for('bb');
let s4 = Symbol.for('bb');
comsole.log(s3===s4) ///true
```

不能与其他数据进行运算



```csharp
let result = s + 100  //error
let result = s > 100  //error
let result = s + s  //error
```

Symbol内置值



```jsx
class Person {
    static [Symbol.hasInstance](param){
        console.log(param);
        console.log("我被用来检测了")；
        return false;
    }
}
let o = {};
console.log(o instanceof Person); //我被用来检测了，false
```

给对象添加方法方式一：



```jsx
let game = {
  name: 'ran',
}
let methods = {
  up: Symbol(),
  down: Symbol(),
}
game[methods.up] = function () {
  console.log('aaa')
}
game[methods.down] = function () {
  console.log('bbb')
}
console.log(game) // name: 'ran',Symbol(),Symbol()
```

给对象添加方法方式二



```jsx
let youxi = {
  name: '狼人杀',
  [Symbol('say')]: function () {
    console.log('阿萨德')
  },
}
console.log(youxi) // name:'狼人杀',Symbol(say)
```

## 10.迭代器

- 迭代器(lterator)是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署lterator接口，就可以完成遍历操作。
- 原理：创建一个指针对象，指向数据结构的起始位置，第一次调用==next（）==方法，指针自动指向数据结构第一个成员，接下来不断调用next（），指针一直往后移动，直到指向最后一个成员，没调用next（）返回一个包含value和done属性的对象



```bash
const arr = ['AA', 'BB', 'CC', 'DD']
let iterator = arr[Symbol.iterator]()
console.log(iterator.next()) //{{value:'AA'，done:false}}
console.log(iterator.next()) //{{value:'BB'，done:false}}
```



```jsx
const banji = {
  name: '终极一班',
  stus: ['aa', 'bb', 'cc', 'dd'],
  [Symbol.iterator]() {
    let index = 0
    let _this = this
    return {
      next: () => {
        if (index < this.stus.length) {
          const result = { value: _this.stus[index], done: false }
          //下标自增
          index++
          //返回结果
          return result
        } else {
          return { value: undefined, done: true }
        }
      },
    }
  },
}
for (let v of banji) {
  console.log(v) // aa bb cc dd
}
```



## 12.Promise

成功回调



```jsx
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    let data = '数据库数据'
    // resolve(data);
    reject(data)
  })
})

p.then(
  function (value) {
    //成功则执行第一个回调函数，失败则执行第二个
    console.log(value) //数据库数据
  },
  function (reason) {
    console.error(reason)
  }
)
```

失败回调



```jsx
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    let data = '数据库数据'
    resolve(data)
    // reject(data)
  })
})

p.then(
  function (value) {
    //成功则执行第一个回调函数，失败则执行第二个
    console.log(value)
  },
  function (reason) {
    console.error(reason) //数据库数据
  }
)
```

使用promise封装ajax请求



```tsx
function ajax (data) {
  return new Promise((resolve, rejects) => {
    // 创建一个XMLHttpRequest对象去发送一个请求
    const xhr = new XMLHttpRequest()
    // 判断请求类型，请求的地址就是参数传递的url
    if(data.methods==="post"){
       xhr.open(data.methods, data.url, true);
          xhr.send(JSON.stringify(data.param));
       }else{
          xhr.open(data.methods, data.url, true);
          xhr.send();
       }
     }
    // 设置返回的类型是json，是HTML5的新特性
    // 我们在请求之后拿到的是json对象，而不是字符串
    xhr.responseType = 'json'
    // html5中提供的新事件,请求完成之后（readyState为4）才会执行
    xhr.onload = () => {
      if(this.status === 200) {
        // 请求成功将请求结果返回
        resolve(this.response)
      } else {
        // 请求失败，创建一个错误对象，返回错误文本
        rejects(new Error(this.statusText))
      }
    }
    // 开始执行异步请求
    xhr.send()
  })
}

//发送请求
let data = {
  url: '', //请求地址
  methods: 'post',
  param: formData,
}
let p = ajax(data)
p.then(
  (res) => {
    //请求成功
    res.data.forEach((val, index) => {
      cent.innerHTML += `<span id='' class='zxz-portry_content_span'>${val}</span>`
    })
  },
  (reason) => {
    //请求失败
    alert(reason.msg)
  }
)
```

## 13.Set集合

ES6提供了新的数据结构set(集合）。它类似于数组，但成员的值都是唯一的，集合实现了iterator接口，所以可以使用「扩展运算符』和「 for…of…』进行遍历，集合的属性和方法:

- size返回集合的元素个数
- add增加一个新元素，返回当前集合
- delete删除元素，返回boolean值has检测集合中是否包含某个元素，返回boolean值



```jsx
let s = new Set()
let s2 = new Set(['A', 'B', 'C', 'D'])

//元素个数
console.log(s2.size) //4

//添加新的元素
s2.add('E')

//删除元素
s2.delete('A')

//检测
console.log(s2.has('C')) //true

//清空
s2.clear()

console.log(s2) //Set(0) {}
```

Set 常用与数组去重



```jsx
let arr = [1, 2, 3, 4, 5, 1, 2]

console.log(new Set(arr)) //Set(5) { 1, 2, 3, 4, 5 }
```

得到的是个Set集合, 如要转换成数组,可通过扩展运算符



```jsx
let arr = [1, 2, 3, 4, 5, 1, 2]

console.log([...new Set(arr)]) //[ 1, 2, 3, 4, 5 ]
```

深度数组去重



```jsx
let arr = [{ name: '123' }, { name: '123' }, { name: '234' }]

//先将数组中的元素全部转为字符串
let arr2 = arr.map((item) => JSON.stringify(item))
//将数组去重后转为对象
let arr3 = [...new Set(arr2)].map((item) => JSON.parse(item))
console.log(arr3) // [ { name: '123' }, { name: '234' } ]
```

## 14. Map集合

ES6提供了Map数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map也实现了iterator接口，所以可以使用『扩展运算符』和「for…of…』进行遍历。Map的属性和方法。



```tsx
let m = new Map()
m.set('name', 'ran')
m.set('change', () => {
  console.log('改变！')
})
let key = {
  school: 'atguigu',
}
m.set(key, ['成都', '西安'])

//size
console.log(m.size) //3

//删除
m.delete('name')

//获取
console.log(m.get('change')) //[Function (anonymous)]

// //清空
// m.clear()

//遍历
for (let v of m) {
  console.log(v)
  //[ 'change', [Function (anonymous)] ]
  //  [ { school: 'atguigu' }, [ '成都', '西安' ] ]
}
```

## 15. Class

ES6提供了更接近传统语言的写法，引入了Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。基本上，ES6的class可以看作只是一个语法糖，它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。



```jsx
class person {
  constructor(brand, price) {
    this.brand = brand
    this.price = price
  }

  call() {
    console.log('我可以打电话')
  }
}

let A = new person('1+', 1999)
console.log(A) //person { brand: '1+', price: 1999 }
```

静态成员



```jsx
class Person {
  static name = '手机'
}
let nokia = new Person()
//静态成员无法通过实例化访问
console.log(nokia.name) //undefined

console.log(Person.name) //手机
```

构造函数继承



```jsx
function Phone(brand, price) {
  this.brand = brand
  this.price = price
}
Phone.prototype.call = function () {
  console.log('我可以打电话')
}
function SmartPhone(brand, price, color, size) {
  Phone.call(this, brand, price)
  this.color = color
  this.size = size
}

//设置子级构造函数原型
SmartPhone.prototype = new Phone()
SmartPhone.prototype.constructor = SmartPhone

//声明子类方法
SmartPhone.prototype.photo = function () {
  console.log('我可以玩游戏')
}
const phone = new SmartPhone('锤子', 2499, '黑色', '5.5inch')
console.log(phone) //SmartPhone { brand: '锤子', price: 2499, color: '黑色', size: '5.5inch' }
```

类的继承



```jsx
class Phone {
  constructor(brand, price) {
    this.brand = brand
    this.price = price
  }
  //父类的成员属性
  call() {
    console.log('我可以打电话')
  }
}
class SmartPhone extends Phone {
  constructor(brand, price, color, size) {
    super(brand, price)
    this.color = color
    this.size = size
  }
  photo() {
    console.log('拍照')
  }

  playGame() {
    console.log('打游戏')
  }
}
const phone = new SmartPhone('小米', 1999, '黑色', '4.7inch')
phone.call() //我可以打电话
phone.photo() //拍照
phone.playGame() //打游戏
```

子类对父类方法的重写



```jsx
class Phone {
  constructor(brand, price) {
    this.brand = brand
    this.price = price
  }
  //父类的成员属性
  call() {
    console.log('我可以打电话')
  }
}
class SmartPhone extends Phone {
  constructor(brand, price, color, size) {
    super(brand, price)
    this.color = color
    this.size = size
  }
  photo() {
    console.log('拍照')
  }

  playGame() {
    console.log('打游戏')
  }

  //重写！
  call() {
    console.log('我可以进行视频通话')
  }
}
const phone = new SmartPhone('小米', 1999, '黑色', '4.7inch')
phone.call() //我可以进行视频通话
phone.photo() //拍照
phone.playGame() //打游戏
```

get 和set的设置



```jsx
class Phone {
  get price() {
    console.log('价格被读取了')
    return 'I LOVE YOU'
  }

  set price(val) {
    console.log('价格被修改了')
    return val
  }
}

//实例化对象
let s = new Phone()
s.price = 12 //价格被修改了
console.log(s.price) //价格被读取了  I LOVE YOU
```

## 16.数值扩展



```jsx
// Number.EPSILON是 JavaScript的最小精度，属性的值接近于 2.22044...E-16
function equal(a, b) {
  if (Math.abs(a - b) < Number.EPSILON) {
    return true
  } else {
    return false
  }
}

console.log(equal(0.1 + 0.2 === 0.3)) //false
console.log(equal(0.1 + 0.2, 0.3)) //true

//二进制和八进制
let b = 0b1010 //2进制
let o = 0o777 //8进制
let d = 100 //10进制
let x = 0xff //16进制
console.log(x) //255

//检测一个数是否为有限数
console.log(Number.isFinite(100)) //true
console.log(Number.isFinite(100 / 0)) //false
console.log(Number.isFinite(Infinity)) //false

//检测一个数值是否为NaN
console.log(Number.isNaN(123)) //false

//字符串转整数
console.log(Number.parseInt('5213123love')) //5213123
console.log(Number.parseFloat('5.123123神器')) //5.123123

//判断是否为整数
console.log(Number.isInteger(5)) //true
console.log(Number.isInteger(2.5)) //false

//将小数部分抹除
console.log(Math.trunc(3.45345345345)) //3

//检测一个数到底是正数、负数、还是0
console.log(Math.sign(100)) //1
console.log(Math.sign(0)) //0
console.log(Math.sign(-123)) //-1
```

## 17. 对象方法扩展



```jsx
//1.Object.is 判断两个值是否完全相等
console.log(Object.is(120, 120)) //true
console.log(Object.is(NaN, NaN)) //false

//2.Object.assign 对象的合并
const a = {
  name: 'ran',
  age: 12,
}
const b = {
  pass: 'i love you',
}
console.log(Object.assign(a, b)) //{name:'ran',age:'12',pass:'i love you'}

//3.Object.setPrototypeOf 设置原型对象 Object.getPrototypeof
const school = {
  name: '拉钩教育',
}
const cities = {
  city: ['北京', '上海'],
}
Object.setPrototypeOf(school, cities) //{ name: 'ran', age: 12, pass: 'i love you' }
console.log(Object.getPrototypeOf(school)) //{ city: [ '北京', '上海' ] }
console.log(school) //{ name: '拉钩教育' }
```

## 18.模块化

- 模块化是指将一个大的程序文件,拆分成许多小的文件，然后将小文件组合起来。
- 模块化的好处：
   1.防止命名冲突
   2.代码复用
   3.高维护性
   4.模块化规范产品
- ES6之前的模块化规范有：
   1.CommonJS ====> NodeJS、Browserify
   2.AMD ====> requireJS
   3.CMD ====> seaJS

模块功能主要有两个命令构成：export和inport

- export命令用于规定模块的对外接口
- inport命令用于输入其他模块提供的功能



```jsx
// src/js/m1.js
export let school = '拉钩教育'
export function teach(){
    console.log('教技能')
}
```



```jsx
import * as m1 from "./src/js/m1.js";
    console.log(m1);
```



