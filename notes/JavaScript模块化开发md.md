#JS模块化开发

模块化开发指的是将复杂问题分解为一些列高内聚，低耦合的子问题，将每个子问题的实现封装成为一个模块，可以在其他应用程序中被调用。

一个模块化系统必须具备的三个部分：

* 定义封装新的模块
* 定义新模块对其他模块的依赖
* 对其他模块的引入支持

由于模块在应用程序之间可以互相调用，因此需要统一的API保证加载的正确性，也就是模块化开发的必须遵循一定的规范，目前通行的JS模块化开发的规范主要有以下几种：

***
## CommonJS

###官方文档链接[CommonJS](http://www.commonjs.org/)

官方JavaScript标准定义了基于浏览器的API，比如dates，math等，但是没有文件系统、IO系统、数据库和服务器接口、打包管理等API。CommonJS期望通过提供一个类似Python、Ruby以及Java一样丰富的标准库，使得利用CommonJS库编写的程序能在各类JS解释器上运行起来，而不仅仅是客户端浏览器。**NodeJS**采用了该规范。

**CommonJS是服务器端模块的规范，根据规范，一个单独的js文件就是一个模块，每个模块都是一个单独的作用域，除非定义为global的变量，模块之间是不可见的。**

CommonJS规范下，可以使用JS开发服务器端JS应用程序，命令行工具，图形界面应用程序，混合应用程序等。

require和exports是内置的两个对象，用于声明模块依赖和模块导出。

Sample如下：

**math.js**
> 
> 实现加法
> 
>     exports.add = function() {
>         var sum = 0, i = 0, args = arguments, l = args.length;
>         while(i < l) {
>             sum += args[i];
>         }
>         return sum;
>     }

**increment.js**
 
> 
> 依赖math模块，并调用其add函数，实现参数自加
>     
>     var add = require("math").add();
>     
>     exports.increment = function(val) {
>        return add(val, 1);
>     }

**main.js**
 
> 
> 程序主文件
>     
>     var inc = require("increment").increment;
>     console.log(inc(5));

通过Sample可以看到，模块依赖在模块化开发中非常重要。目前主流的类库，比如国外的YUI3类库，淘宝的KISSY类库，都是通过配置文件指定需要的模块。在配置文件中通过requires声明需要的模块。

###CommonJS中Modules风格模块定义不适合于浏览器端

CommonJS中，Modules风格的模块定义有可能是同步加载的，必须在依赖的模块都获取后，当前的模块才能执行，否则可能会出错。当模块文件运行在服务器时，由于依赖的模块组件都在本地，可以快速地获取到，不会影响执行速度，也可以方便地执行模块的同步/异步加载(**NodeJS遵循该风格**)。

而浏览器需要通过网络加载获取依赖模块，因此当依赖的包很多时，对页面加载速度会有很大的影响。CommonJS中提出了新的风格，Modules/Wrappings，即包装模块定义。[Modules/Wrappings](http://wiki.commonjs.org/wiki/Modules/Wrappings)

定义模块用module，有一个方法declare

1. declare接受一个函数类型的参数，比如f
2. f有三个参数，分别是require, exports以及module
3. f使用返回值和exports导出API
4. f如果是对象类型，则该对象作为模块输出

**A basic wrapped module**
>      module.declare(function(require, exports, module) {
>          expotrs.foo = "bar";
>      })

**A wrapped module returning a value**
>     module.declare(function(require) {
>         return {foo: "bar"};
>     })   

**A wrapped module with an object factory**
>     module.declare {
>         foo: "bar"
>     })

***
## AMD

###官方文档[AMD](https://github.com/amdjs)
Asynchronous Module Definition，异步模块定义，所有模块异步加载，模块加载不堵塞其他语句的执行，所有依赖某些模块的语句均放在回调函数中。**也可以说，AMD是专门为浏览器中的JavaScript环境设计的规范**

AMD定义了define和require全局标识符，可以自己实现，其中自定义的define函数需要包含一个属性amd，是一个对象，即define.amd = {}

define(id?, dependencies?, factory)

* id: 模块标识符，可选，不存在则默认为定义在加载器中被请求脚本的标识
* dependencies: 模块依赖关系
* function(){}/object{}，需要进行实例化的一个函数或对象

**Sample**
>     define("blockingNoises", ["require", "exports", "tomatoPotato"], fucntion(require, exports, romatoPotato) {
>        export.block = function() {
>            return tomatoPotato.block();
>        }
>     })

使用AMD模式开发简单三层结构：基础库/UI层/应用层

**base.js —— 无依赖的模块**
>     define(function() {
>         return {
>             mix: function(source, target) {
>             }
>         }
>     })

**ui.js —— 有依赖的模块**
>     define(["base"], function(base) {
>         return {
>             show: function() {
>                 //to do with module base
>             }
>         }
>     })

**data.js —— 数据对象模块**
>     define({
>         users: [],
>         options: []
>     })

**app.js —— 程序入口**
>     define(['data', 'ui'], function(data, ui) {
>         //init here, main entrance
>     })

具名模块，即指定模块名称的定义方式通常不推荐，一般由打包工具合并多个模块到一个js文件中时使用

包装模块：兼容CommonJS的Modules/Wrappers
>     define(function(require, exports, module) {
>         var base = require('base');
>         exports.show = function() {
>             //to do with module base
>         }
>     })

###实现AMD规范的库有RequireJS， curl等，同时也有一些库支持AMD规范，即将自己作为一个模块存在，比如jQuery，MooTools， firebug等。

***
##CMD

###官方文档[CMD](https://github.com/cmdjs)

Common Module Definition, 通用模块定义，该规范明确了模块的基本书写格式和基本交互规则。全局函数define用于定义模块。

**AMD是依赖关系前置，CMD则是按需加载**

CMD规范中，一个模块就是一个文件。模块定义方式如下：
>     define(factory);

factory是被定义的模块，可以是**函数、对象或字符串**

* factory是对象或字符串时，表示该模块的接口就是该对象或字符串
* factory是函数时，表示该函数是模块的构造方法，执行该构造方法可以得到模块对外的接口。
>     define(function(require, exports, module) {
>         //...module code
>     })

####require —— require(id)
* require是一个函数，接收依赖模块标识符，返回模块接口或者null
* **同步加载执行**

####require.asyn —— require.async(id, callback?)
* require.asyn，接收一系列依赖模块的标识符以及一个可选的回调函数；用来在模块内部异步加载模块，并在加载完成后执行指定毁回调函数，回调函数按依赖顺序接收依赖模块的接口或者null
* **异步加载执行**

####define

define.cmd， 一个空对象，可用来判定当前页面是否有CMD模块加载器
>     if(typeof define === "function" && define.cmd)

####exports
* 对象，用来向外提供模块接口
>     define(function(require, exports) {
>         exports.foo = "bar";
>         exports.f = function() {};
>     })
> 除了通过exports给exports对象增加成员， 也可以使用return语句直接提供对外的接口
>     define(function(require) {
>         return {
>             foo: "bar",
>             f: function() {}
>         }
>     })

**！！！在factory内部给exports重新赋值时，并不改变module.exports的值，直接给exports赋值无效，不能用来更改模块接口。**
>     define(function(require, exports) {
>          exports = {
>              a: "aaa",
>              f: function() {}
>          }
>     })
>   以上的写法是无效的，需要通过return或者给module.exports赋值

**exports的赋值需要同步执行，不能放在回调函数里。**
>     //x.js
>     define(function(require, exports, module) {
>          //wrong use
>          setTimeOut(function() {
>               module.exports = {a: "hello"}
>          })
>     })
>     //y.js
>     define(function(require, exports, module) {
>          var x = require('./x');
>          
>          //无法立刻得到模块x的属性a
>          console.log(x.a);
>     })

####module
* 对象，存储了和模块相关的一些属性和方法
* module.uri: 根据模块系统的路径解析规则得到的模块的绝对路径，当define函数中id缺失时，module.id = module.uri
* module.dependencies，数组，表示当前模块的依赖
* module.exports：当前模块对外提供的接口

###实现CMD规范的库有Sea.js
    






















