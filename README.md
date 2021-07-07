# webQuestion

常问的js面试题

1.js基本数据类型
基本数据类型：number string boolean undefined null bigint symbol 
引用数据类型：object array function

2.基本数据类型和引用数据类型的区别
1）变量的不同内存分配。
基本数据类型是将值存在栈中，他们的值直接存在变量访问的位置。
引用数据类型存在堆中，存储的变量值是一个指针，指向存储对象的内存地址。
2）复制值不同。
基本类型直接复制复制后原始值和新值互不影响
引用类型直接复制的话，新复制的值是一个原值所在堆内存中的地址，修改新数据的值的话会影响原数据
可以利用深拷贝进行复制
3）传递值的区别
基本数据类型通过 = 进行值传递 
对象是通过引用传递，而不是值传递。也就是说，变量赋值只会将地址传递过去。

3.js里面的深浅拷贝
浅拷贝只复制指向某个对象的指针，而不复制对象本身。深拷贝就是能够实现真正意义上的数组和对象的拷贝。
浅拷贝：object.assign() 将所有可枚举属性的值从一个或多个对象复制到源对象
深拷贝：Json.parse(json.Stringfy())  递归

4.new的过程
1）创建实例对象
2）给实例对象属性复制，其__proto__的隐式原型链指向其prototype的显示原型链
3）this上下文指向新的实例
4）执行构造函数
5）构造函数有无return 无return（即return undefined）或return类型为基本类型，则最终return还是新建的实例对象 
若return为一个引用类型，则最终return这个引用类型

5.this指向问题  this永远指向一个对象，this取决于函数调用的位置
1）以函数的方法调用时，this指向window
2)以方法的形式调用，this指向调用方法的那个对象
3）以构造函数调用时，this就是新创建的实例对象
4）call apply bind 自定义this
5)箭头函数没有this this指向包含箭头函数最近一层的函数的this

6.call apply bind 的区别
call和apply是改变了函数的this上下文之后便执行了该函数 
bind是返回了改变this上下文的新函数
call和apply传参不同 第一个参数都是要改变上下文的对象 call第二个参数是列表 apply是数组或类数组

7.事件捕获和事件冒泡
事件捕获是从外向内依次触发 事件冒泡是从内向外依次触发
阻止冒泡：event.stopPropagation()
事件委托利用的就是事件冒泡 将子元素的事件绑定在父元素上，减少事件绑定的次数提升性能
但是注意：祖先元素不会直接处理事件，而是根据event.target得到发生事件的后代元素，通过这个后代元素调用回调函数

8.闭包 闭包存在于嵌套的内部函数中。 闭包就是一个函数有权限访问另一个函数作用域中的变量
作用：延长局部作用域中变量的声明周期 使函数外部可以访问函数内部的数据
缺点：内存泄漏 解决：及时释放引用的外部词法环境
应用：将一个函数作为另一个函数的返回值;将函数作为实参传递给另一个函数调用。
将所有的数据和功能都封装在一个函数内部(私有的)，只向外暴露一个包含n个方法的对象或函数。
模块的使用者, 只需要通过模块暴露的对象调用方法来实现对应的功能。

9.继承
构造函数继承 原型链继承 组合继承 原型式继承 寄生式继承 寄生组合式继承
1）构造函数继承 子类利用call或apply继承父类的构造函数
特点：1、只继承了父类构造函数的属性，没有继承父类原型的属性。
　　　2、可以继承多个构造函数属性（call多个）。
　　　3、在子实例中可向父实例传参。
缺点：1、只能继承父类构造函数的属性。
　　　2、无法实现构造函数的复用。（每次用每次都要重新调用）
　　　3、每个新实例都有父类构造函数的副本，臃肿
2）原型链继承 子类实例的原型继承父类的实例
特点：1、实例可继承的属性有：实例的构造函数的属性，父类构造函数属性，父类原型的属性。
缺点：1、新实例无法向父类构造函数传参。
　　　2、继承单一。
　　　3、所有新实例都会共享父类实例的属性。（原型上的属性是共享的，一个实例修改了原型属性，另一个实例的原型属性也会被修改！

3）组合继承 结合了两个前面2种继承的优点（传参和复用） 缺点就是调用了两次构造函数

10.作用域和作用域链
js采用的是词法作用域(静态作用域) 包括：全局作用域 函数作用 es6块级作用域
全局作用域就是全局可以使用 函数作用域就是函数内部可以使用 let 或 const声明的变量只在 let 或 const命令所在的代码块 {} 内有效，在 {} 之外不能访问。
作用：隔离变量 不同作用域下同名变量互不影响
作用域链:通过词法环境的对外部词法环境的引用（scope）将作用域链起,变量可通过作用域链逐层向上查找

11.原型和原型链
*显式原型和隐式原型
每个函数对象都有一个prototype,他默认指向一个Object实例对象，即显式原型
每个实例对象都有一个__proto__,即隐式原型，它指向构造函数的prototype
构造函数的prototype等于实例对象的__proto__
**当访问一个实例对象的某种属性时，现在自身的属性上找，找到返回，找不到的话沿着原型链找，找到返回，找不到返回undefined

12.执行上下文
全局执行上下文
1）在执行全局代码前将window确定为全局执行上下文对象
2）预解析 var 提前声明不赋值，添加为window的属性 function 提前声明且定义，添加为window的方法 this上下文指向window
3）压栈，执行全局代码
函数执行上下文
1）在调用函数准备执行函数体之前，创建对应的函数执行上下文对象
2）预解析 形参，arguments，this赋值，添加为函数执行上下文的属性 var 提前声明不赋值，添加为函数执行上下文的属性 function 提前声明且定义，添加为函数执行上下文的方法
3）压栈，执行函数代码
执行上下文栈
1）在全局代码执行前，JS引擎会创建执行栈来存储所有的执行上下文对象
2）在全局执行上下文确定后，将其压栈
3）在函数执行上下文创建后，将其压栈
4)在当前函数执行完后，将栈顶出栈，仍然在内存中，等待垃圾回收机制回收
5）所有代码执行完后，栈中只剩window

13.typeOf和instanceof
typeof返回的是该类型的字符串表达  (number、string、undefined、boolean、function、object)
typeof(null)返回的是object
typeof对象的话,除了函数返回的都是object

A instanceof B 检验A是不是B的实例 是的话返回true 不是的话返回false
*instanceof只能判断是不是实例而不能判断具体是那种类型
eg：[] instanceof object // true

14.如何判断是否是数组
eg：let arr = []
1)object.prototype.toString.call(arr).splice(-1,1) // []
2)isArray
!!!会存在多个全局环境的问题
3)利用构造函数 arr.constructor === Array
4）arr instanceof Array 

15.垃圾回收
1)标记清除
当变量进入JS执行栈环境标记为 '进入环境' ，标记为'进入环境'的变量不可被回收
当变量从JS执行栈出栈，则标记为'离开环境'，离开环境的变量可以被回收
2)引用清除
堆对象被变量引用的次数为0时，回收其占用的内存空间
引用清除存在循环引用的问题

16.DOM增删改查
1)创建
createDocumentFragment() //创建一个DOM片段 
createElement() //创建一个具体的元素 
createTextNode() //创建一个文本节点 
2）添加、移除、替换、插入 
appendChild() 
removeChild() 
replaceChild() 
insertBefore() 
3）查找 
getElementsByTagName() //通过标签名称 
getElementsByName() //通过元素的Name属性的值 
getElementById() //通过元素Id，唯一性

17.js封装 闭包封装和原型链封装
1、对象原型封装
基本思想是在原函数中建立getter和setter方法，之后在原函数的原型进行其他操作。
好处：只能通过get和set访问函数中的数据，实现额真正的封装，实现了属性的私有化
劣处：这样做所有的方法都在对象中，会增加内存的开销
2、闭包封装
基本思想：构建闭包函数，在函数内部返回匿名函数，在匿名函数内部构建方法，在每次进行实例化调用的时候，其实都是每次都是调用返回函数的子函数，同时能保持对对象中的属性的共享
好处：可以做到实例对象向对象属性的共享并且保持私有
坏处：所有的get和set都存储在对象中，不能存储在prototype中，会增加开销

18.本地对象 内置对象 宿主对象
本地对象指的是可以实例化的 例如array object regexp
内置对象指的是Math global 等不可实例化的
宿主对象指的是 window document等

19.ajax和jsonp
ajax是一种发送http请求与后端进行异步通信的技术
ajax的同源策略：协议 域名 端口号一致
jsonp
定义：一种可以实现跨域发送http请求的数据通信格式，可以嵌在ajax中使用。
原理：利用script标签可以跨域链接资源的特性。

20.事件循环
js执行过程中分为主线程和工作线程
主线程：也就是 js 引擎执行的线程，这个线程只有一个，页面渲染、函数处理都在这个主线程上执行。
工作线程：也称幕后线程，这个线程可能存在于浏览器或js引擎内，与主线程是分开的，处理文件读取、网络请求等异步事件。
所有的任务可以分为同步任务和异步任务，同步任务，顾名思义，就是立即执行的任务，同步任务一般会直接进入到主线程中执行；
而异步任务，就是异步执行的任务，比如ajax网络请求，setTimeout 定时函数等都属于异步任务，异步任务会通过任务队列的机制(先进先出的机制)来进行协调。
同步和异步任务分别进入不同的执行环境，同步的进入主线程，即主执行栈，异步的进入任务队列。主线程内的任务执行完毕为空，会去任务队列读取对应的任务，推入主线程执行。 上述过程的不断重复就是我们说的 Event Loop (事件循环)

# `Es6面试题`
1.var let const
var挂载在window上，let和const不是
var存在变量提升，let和const没有
var没有块级作用域的概念 可以跨块访问 let和const形成块级作用域
作用域内 var可以重复声明同一个变量 let和const不行
const 声明的是一个常量 不能修改
eg : const person = {
       name:'cc',
       age:'18'
     }
    person.name = "xx"
console.log(person) //{name:"xx",age:18}
此时person保存的的是内存地址的指针 所以数据改变了

2.解构赋值
按照一定的模式，从数组或者对象中提取值，对变量进行赋值，只要左右两边模式相同，左边的变量就会被赋值

3.数组去重
let arr = [1,1,2,2,3]
1)for (let i = 0; i < arr.length; i++) {
          if (arr.indexOf(arr[i]) !== i) {
            arr.splice(i, 1)
            i--
          }
        }
        return arr
//arr.indexOf(i)返回的是i在数组中第一次出现的位置的索引

2)Array.from(new Set(arr))
//Array.from 是将类数组对象或可遍历对象转换成真正的数组
  set 允许存储对象的唯一值
  
3）arr.filter((item, index) => arr.indexOf(item) === index)  

let arr = [1,1,2,3]
4）arr.reduce((prev, cur) => prev.includes(cur) ? prev : [...prev, cur], [])
//includes prev是否包含cur 包含就返回true
pre 是初始值 用于计算返回的结果 cur是数组的每一项

4.数组扁平化 用于将嵌套的数组“拉平”，变成一维的数组。该方法返回一个新数组，对原数据没有影响。
实现数组扁平化的方法
1）arr.flat(Infinity) 括号内的参数代表拉平的层数
2）利用递归
flatArr(arr){
  let tempArr = []
  arr.map( item => {
    if(Array.isArray(item)){
      tempArr.concat(flatArr(item))
    }else {
      tempArr.push(item)
    }
  )
  return tempArr
}

5.判断一个对象是否是空对象
String(obj) === '[object Object]' && Reflect.ownKeys(obj).length === 0
eg:let obj = {name:'cc'} //String(obj) [object object]
//Reflect.ownKeys()方法返回target对象自己的属性键的数组
扩展 object.prototype.toString.call() 也可以判断是不是对象

6.几种遍历的方法及区别
1)forEach
对数组里面的每一项执行提供的函数 不可中断 无返回值
2)for in
用于遍历数组或对象的属性 对数组或对象的属性进行循环操作
3)for of
可以用来循环遍历 数组 对象 字符串 map set 
4)object.keys()
Object.keys 返回一个所有元素为字符串的数组，其元素来自于从给定的object上面可直接枚举的属性。

7.箭头函数
1)箭头函数本身没有this，箭头函数的this继承的是外部函数的this
2)箭头函数没有prototype
3)箭头函数没有construct内部方法，不能用new调用
什么时候使用箭头函数？
非对象的方法且不用做构造函数时，使用箭头函数
