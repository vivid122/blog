
##为什么我们需要JS模块化
JS并不是一种模块化的编程语言。它甚至连css都有的@import都没有。因此在web前端js代码十分复杂的今天，js模块化是十分有必要的。因为如果所有的变量都在全局中，那么随着js代码的增多，这种共享全局作用域的行为就会导致命名空间（namespace）的污染。同时，对js代码进行模块化处理，能增强代码的可移植性。在需要进行代码复用时，无需考虑上下文，直接移植封装好的模块，或者在其他地方直接引入整个模块。这样，在出问题或者需要修改的时候，只需要在模块内部进行修改，不会出现牵一发而动全身的麻烦。此外，模块化使得庞大的js代码变得有条理，方便维护和扩展。也方便了测试和维护。模块间互相独立，只暴露了接口，避免外部的干扰。就像把一本书的内容分章节一样，把一大堆代码分清条理层次，不仅可以让代码不被污染，可移植性高，而且可以分单元测试，方便各个模块独立的运行和修改。

##js模块化的发展

**js模块化的基本思想：封装模块；暴露接口；声明依赖。**

#####普通的function写法：
>functions are the only things in JavaScript that create a new scope.
函数是JS中唯一能创建新的作用域的东西……所以说，模块的作用域都是通过函数创建的。
`var math=math({
	count:0;
	m1:function(){
	return a+b;
}
    m2:function(){
	return a-b;
 }
});`
将模块写成一个对象，所有模块成分都放在对象里面。
但是会暴露模块中所有成员，从而使得模块内容易被外部修改。


#####IIFE
Immediately Invoked Function Expressions立即执行函数表达式
基本格式
`(function(){
	//
}());`
解决了直接用function时模块内容会被外部修改的问题，不会暴露模块内部私有成员。并且所占用的内存在执行完成后立即释放。

`var module1=(function(){
return{
	summer:function summer(){
	return 'It is hot!';' 
}
};
}());`

问题是在每个模块中你不得不暴露至少一个全局变量，如果在做一个有很多个模块的应用，那就不是很好了。
此外，function和IIFE并不能声明依赖。并且，以上两种方式的问题是，在JS官方没有模块化标准的情况下，模块化的写法多种多样，严重阻碍了组件的流通。一个社区有自己的一套写法，另一个是另外一套写法，这样就非常混乱了。与模块化的初衷是相悖的。于是就有了common.js的出现。

#####Common.js 
node.js的广泛应用让Common.js的存在感越来越强烈。
Common.js的模块系统的语法比其他的要简单。在Common.js中，一个模块就是一个文件。没有必要为一个函数来包装作用域域，因为每个文件都被赋予了它们自身的作用域。
首先，自由变量exports声明了模块的公用API；

`'use strict';
var foo = function foo (){
	return ture;
};
exports.foo = foo;//把foo暴露给其他模块，也就是提供了接口

然后，用require函数来加载模块:

var foobar = function(){
	console.log('foobar result');
};
exports.foobar = foobar;
var foorbar = require('./foobar');//依赖声明`

然后就可以调用模块提供的方法。

但是Common.js存在的问题是，require是同步的。也就是说，require的文件要完全加载完成才能进行下一步。当要加载的文件非常大时，浏览器就会处在一种假死状态。也就是说，Common.js不适用于浏览器端。这就有了异步的加载需求，即AMD。

######AMD  
Asynchronous Moudule Definition 异步模块定义，所有依赖这个模块的语句都定义在一个回调函数callback中，只有模块加载完成，回调函数才会运行。

AMD也采用require()语句加载模块，但是不同于CommonJS，它要求两个参数：
　>require([module], callback);

第一个参数[module]是一个数组，里面的成员就是要加载的模块；第二个参数callback，就是加载成功之后的回调函数。
AMD的规范是，把模块用一个名为define()的函数包起来，像这样：

   `define([moduleId,] dependencies,definitionFunction);`
   moduleId 模块名，dependencies 模块依赖；definitionFunction 初始化模块的函数。
   比如：
   `define('m0',function(){
      var add = function(a,b){
      return a+b;
  }
      return {
      add: add
  };
});//这定义了一个m0模块；
//加载如下：
   require('m1',[m0],function(m0){
       alert(m0.add(2,3));
});//5`

目前应用ADM规范的主要就是Require.js和Curl.js，实际应用中也都用它们。


#####ES6 Module
最激动人心的是，2015年6月，ECMAScript 6正式发布。JS也有了官方的模块体系。尽管现在还有各种兼容性问题，但ES6 Module的出现无疑让人看到了前端规范化的曙光。

ES6的设计思想是静态加载，也就是在编译的时候确定模块的依赖关系并且输入和输出变量。而Common.js和AMD都是运行时加载。不过，这也导致了没法引用ES6模块本身，因为它不是对象，而是通过export命令显式指定输出的代码。

#######ES6 Module的主要规范：

**1，严格模式**
不管有没有在头部加上"use strict"，ES6模块都自动采用严格模式。

**2，export，import命令**
export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。
`//person.js
export var firstName='Jack';
export var lastName='Chan';
var year = 1970;

export{firstName,lastName,year};//对外输出了三个变量。`
此外还可输出函数或者类（class）。

import命令可以加载定义了接口的模块。
比如：
`import{firstName,lastName,year}from'./person';

function setName(element){
	element.textContent=firstName+' '+lastname；
};`
import大括号里导入的名称必须与import提供的接口名称相同。
此外，还有一些有意思的特性，比如可以使用as关键字，将输入的变量重命名；用*指定一个对象，然后整体加载；用export default指定默认输出，然后加载时import可以指定任意名称引入。具体的就要系统化的学习ES6了，这里只是说明一些主要特性。
但是要注意的是，export和import只能放于模块顶层而不能放在作用域中。因为处于条件代码块之中，就没法做静态优化了，违背了ES6模块的设计初衷。

其实除了Common.js,AMD还有很多模块系统，然而ES6module正宫出来，它们的地位就更低了……


*参考：*
[Programming JavaScript Applications-Chapter 4. Modules]
[Eloquent JavaScript Chapter10 Modules]
[Eloquent JavaScript Chapter10 Modules]
[ECMAScript入门](http://es6.ruanyifeng.com/#docs/module)

*更多补充，等博主上手应用了再说……*