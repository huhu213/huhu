#CSS选择器

主要有以下这些，粗体的选择符表示是CSS3中新增的

###元素选择符

* 通配选择符(*) * {}
* 类型选择符(E) h1 {}
* ID选择符(#id) #test {}
* 类选择符(.className) .test {}

###关系选择符

* 包含选择符(A B) 

  A元素包含的所有B元素
  
* 子选择符(A>B) 

  A元素的儿子元素中的B元素

* 相邻选择符(A+B) 

  紧跟着A的B元素
  
* 兄弟选择符
  
  所有与A是兄弟的元素B，而不仅仅是相邻的

###属性选择符

* E[att]：具有att属性的E元素
* E[att="val"]：具有属性att且值为val的E元素
* E[att~="val"]：具有att属性，且att属性值(以空格分开)中有一个是val的E元素
* **E[att^="val"]**：具有att属性，且值以val开头的E元素
* **E[att$="val"]**：具有att属性，且值以val结尾的E元素
* **E[att\*="val"]**：具有att属性，且值中包含字符串val的E元素
* E[att|="val"]：具有att属性，且值以val开头，以-为连接符的E元素，若只包含一个val值，也会被选择

###伪类选择符

* E:link：超链接未被访问前的样式
* E:hover：悬停元素的样式
* E:active：元素被激活(鼠标点击与释放之间发生的事件)的样式
* E:focus：元素成为输入焦点时的元素(input textarea等)//webkit会默认给focus状态的元素加上outline样式
* E:lang(fr)：匹配使用特殊语言的元素E
* **E:not(s)**：匹配不包含s选择符的元素E

比如给除了最后一个li元素加上底边框
>
>     .demo li:not(:last-child) {
>         border-bottom: 1px solid #CCCCCC;
>     }

* **E:root**：匹配E元素在文档中的根元素，HTML中，根元素永远是HTML
* E:first-child：匹配父元素的第一个子元素且该元素是E元素，若不是，则该选择符失效
* **E:last-child**：匹配父元素的最后一个子元素且该子元素是E，若不是，则该选择符失效
* **E:only-child**：匹配父元素的唯一一个子元素且该子元素是E
* **E:nth-child(n)**：匹配父元素的第n个子元素且该子元素是E，若不是，则该选择符失效
* **E:nth-last-child(n)**：匹配父元素的倒数第n个子元素且该子元素是E，若不是，则该选择符失效
* **E:first-of-type**：匹配父元素第一个E元素，不需要是第一个元素
* **E:last-of-type**：匹配父元素最后一个E元素，不需要是最后一个元素
* **E:only-of-type**：匹配父元素唯一一个E元素，不需要是唯一的子元素
* **E:nth-of-type(n)**：匹配父元素第n个E元素，不需要是第n个元素
* **E:nth-last-of-type(n)**：匹配父元素倒数第n个E元素，不需要是倒数第n个元素
* **E:empty**：匹配不包含任何子元素(包含text及诶单)的元素E
* **E:checked**：匹配被选中的E元素(input中的type=checkbox和radio的元素)
* **E:enabled**：匹配可用元素E(input框等)
* **E:disabled**：匹配不可用元素E(input等)
* **E:target**：匹配先关URL指向的E元素，URL后面跟锚点#，指向文档内某个具体的元素，该被链接的元素就是目标元素

###伪对象选择器(Pseudo-Element Selector)

* E:first-letter/E::first-letter：设置块级元素内第一个字符的样式，通常**用来配合font-size和属性float属性设置首字下沉的样式**

* CSS3中，伪类选择器使用:单冒号，伪对象选择器使用::双冒号
> 
>     p:first-letter {
>         font-size: 200%;
>         color: #8A2BE2;
>     }

* E:first-line/E::first-line：设置块级元素内第一行的样式
* E:before/E::before：设置对象前(依据对象树的逻辑结构)发生的内容，用来和content属性一起使用，且必须定义content属性
>
>     p::before {
>          content: "test";
>     }
> 
>     p::after {
>          content: "test";
>     }     

* E:after/E::after：设置对象后发生的内容，与content属性一起使用，且必须定义content属性
* **E::placeholder**：设置占位符的样式
>
>     input::-webkit-input-placeholder {
	        color: #999;
        }
        input:-ms-input-placeholder { // IE10+
	        color: #999;
        }
        input:-moz-placeholder { // Firefox4-18
	        color: #999;
        }
        input::-moz-placeholder { // Firefox19+
	        color: #999;
        }
 
 * **E::selection**：::selection只能定义被选择时的background-color，color以及text-shadow
 

