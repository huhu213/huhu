#HTML5

##新特性
* canvas标签
* 媒介回放的video/audio标签
* 本地离线存储
* 新的特殊内容元素：article, footer, header, nav, section
* 新的表单控件: calendar, date, time, email, url, search
* 浏览器支持: Safari, Chrome, Firefox, Opera, IE9

##基础
###声明
>     <!DOCTYPE html> 
     
HTML4中，在DOCTYPE中需要加入解析规范，比如
>     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

###新增主体结构元素(块元素)
* article

代表文档、页面或应用程序中独立、完整、独自被外部元素引用的内容。可以使一段文字，或者一个插件等。

>     <article>
>     <header>作者</header>
>     <p>评论</p>
>     <footer>时间</footer>
>     </article>

* aside

表示article之外的内容，与article

* bdi——Bi-directional Isolation，隔离一段文本

设置一段文本，使其脱离父元素的文本方向设置。如下例子：
>     <ul>
>         <li>Name: <bdi>Joseph</bdi> 80 points</li>
>         <li>Name: <bdi>إيان</bdi> 90 points</li>
>     </ul>

第二个li中，由于名字中包含特殊字符，若不用bdi标签包裹，则90会在特殊字符前面出现。

* details 显示一段详细信息

>    <details>
>         <summary>This is a summary.</summary>
>         <p>Huhu</>
>    </details>

summary标签用于指定标题，默认标题是详细信息。details有一个open属性，用于指定details是否显示 

* figure

规定独立的流内容(图像、图标、照片、代码等)。<figcaption>位<figure>元素定义标题。<figure>元素内容应该与主内容相关，同时元素位置相对于主内容是独立的，删除该元素对主内容没有影响。

* footer&header
* mark——部分文本的高亮显示
* nav定义导航链接
* progress进度条，标记进度
* section定义文档某个区域，比如章节、头部、底部或其他区域

###新增多媒体元素
* canvas: 定义图形，基于JavaScript的绘图API
* audio: 定义音频内容，支持MP3、Wav、Ogg三种格式
* video: 定义视频内容，支持MP4、WebM、Ogg
* source: 定义多媒体资源<video>和<audio>
* embed: 定义嵌入的内容，比如插件
* track: 为video和audio之类的媒介规定外部文本轨道，即字母轨道，只有IE9+，chrome以及opera支持

###新增表单元素
*datalist: 与input配合使用，表示input的可能的值






