#Backbone

###简介

MVC模式(Model-View-Controller)支持将数据从表示层或文档对象模型DOM中分离出来，Backbone是一个支持MVC应用程序的轻量级库。

###Router

Backbone和AngularJS一样，在单页面应用程序中应用较多。单页面程序中，页面通过不同的状态来改变展示出来的View。Backbone使用hash segment来表示不同的状态。

Backbone提供一个Router组件路由客户端状态。Backbone.Router可以扩展，并且包含一个hash map(routes属性)将状态和活动关联起来。

>
>    var Router = Backbone.Router.extend({
>    
>    	routes: {
>			"": "index",
>			"/teams": "getTeams",
>			"eror": "fouOfour"
>		},
>		index: function() {
>			//home page
>		},
>		getTeams: function() {
>			//get teams
>		}	
>    })

其中，每个hash segment不仅仅可以指代具体的状态，也可以是函数，比如getTeams()。

应用程序通过Backbone.history.start()被实例化。Backbone.hitory对象包含Backbone.History函数，该函数负责匹配路由。start()方法触发后，Backbone.history的fragment属性被创建，用于管理浏览器历史等。

###View

Backbone中的视图可以扩展Backbone.View函数并显示模型中存储的数据。一个视图提供一个由el属性定义的HTML元素。该属性可以是由 tagName、className 和 id 属性相组合而构成的，或者是通过其本身的 el 值形成的。

一个视图和一个模型相关联。

> 
>     app.LayoutView = Backbone.View.extend({
>         initModule: function() {}
>     });

具体的app视图可以通过扩展LayoutView定义。
> 
>     var MainView = app.LayoutView.extend({
>         el: document.body,
>         events: {},
>         login: function(){},
>         redirect: function(){},
>         toggleView: function(){}
>     })

Backbone也支持客户端模版的使用。
> 
>     <%if (item.module && item.module != 'applist') {%>
>     <%if (/overview/.test(item.module)) {%>
>         <a class="sidebar-top js-sidebar-top" href="<iitem.module%>" target="_blank" data-privilege="<%-item.has_privilege%>">
>     <%} else if (/admin_stat/.test(item.module)) {%>
>         <a class="sidebar-top js-sidebar-top" href="<%-item.module%>" target="_blank">
>     <%} else {%>
>         <a class="sidebar-top js-sidebar-top" href="#<%-item.module%>">
>     <%} %>
>     <%}else {%>
>         <a class="sidebar-top js-sidebar-top">
>     <%}%>


Backbone.View中的Render()方法可以自定义el属性指定的元素的渲染方式，也可以将rander方法bind到模型变更事件中。

> 
>     MainView = Backbone.View.extend({
>         init: function() {
>             this.model.bind("change", this.render, this);
>         }
>     })


Backbone.View的events属性监听当前模型的事件。

>     MainView = Backbone.View.extend({
>         el: document.body,
>         events: {
>             "click js-sidebar": "showSidebar"
>         }
>     })

events属性每一项由两部分组成：
* 事件类型和触发事件的选择器
* 事件处理函数