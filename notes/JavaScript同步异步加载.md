#JS文件同步和异步加载

###同步加载
JavaScript默认加载模式是同步的，是阻塞的，当前js没有加载完毕会阻塞浏览器的后续处理，停止后续的解析，因此停止了后续文件的加载、渲染、代码执行。

由于JS可能会输出，修改DOM，重定向等行为，因此默认同步执行能保证加载的安全性。

一般的做法是将\<script>标签放在页面末尾</body>之前，尽可能让页面展示出来。

###异步加载
异步加载又称非阻塞加载，浏览器下载并执行js时，不阻塞后续的操作。

详细介绍见这篇博客[JavaScript的同步与异步加载](http://yiyanwan77.iteye.com/blog/1671597)

比较简单的方式是，在script tag中，添加async和defer属性。

####async属性
HTML5中新增属性，表示在js加载完成后尽快执行，不保证JS的执行顺序，将在onload事件之前完成。(onload事件表示包括页面，各类资源全部加载完成时触发的事件)

没有async属性时，js文件立即下载并执行，同时block浏览器的后续处理；加上async属性，表示js文件异步加载并执行，同时后续处理继续进行。

####defer属性
该属性声明脚本文件中将不含有document.write或者其他dom修改。浏览器立即下载js文件和其他有defer属性的js文件，而不阻塞页面后续的处理。**和async属性不同的是，defer属性声明的脚本保证是按顺序依次执行的**


#CSS文件加载

Google Developers上的介绍如下[Render Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css?hl=en)

render blocking指的是，对于需要的外部样式，浏览器是否会等待它并保持现有的页面渲染结果，**并不是指CSS文件的下载被阻塞！！！**

默认来说，CSS文件的加载是会堵塞渲染进程的，即在渲染页面时，是阻塞的。一些情况下动态变化的CSS样式，则是非阻塞的，比如:
>     <link href="style.css" rel="stylesheet">
>     <link href="print.css" rel="stylesheet" media="print">
>     <link href="other.css" rel="stylesheet" media="(min-width: 40em)">

以上三种情况下，第一种是阻塞的，只有当CSS下载完成后，才会按定义的样式来渲染页面；第二和第三种是非阻塞的，只有在特定的media条件下，动态地加载CSS文件。




