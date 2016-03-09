---
title: js状态机实现tab切换页面
date: 2016-03-09 19:26:40
tags:
---
## tab页的状态机方式实现，不多说直接上代码
[源码](https://github.com/zkboys/little-demo/blob/master/jq_tabs.html)
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jQuery 选项卡</title>
	<style>
		*{
			padding:0;
			margin:0;
		}
		body{
			padding:15px;
		}
		 #tabs{

		 }
		 #tabs>li{
		 	width:100px;
		 	height:30px;
		 	line-height: 30px;
		 	text-align: center;
		 	float:left;
		 	list-style-type: none;
		 	border:1px solid #ccc;
		 	border-bottom:0;
		 	cursor:pointer;
		 }
		 #tabs>li:first-child{
		 	border-top-left-radius:5px;
		 	border-right:0;
		 }
		 #tabs>li:last-child{
		 	border-top-right-radius:5px;
		 	border-left:0;
		 }
		 #tabs>li.active,#tabs>li:hover{
		 	background-color:#eee;
		 }
		 #tabs-content>div{
		 	display:none;
		 	width:500px;
		 	height:200px;
		 	border:1px solid #ccc;
		 	border-bottom-right-radius: 5px;
		 	border-bottom-left-radius: 5px;
		 	border-top-right-radius: 5px;
		 }
		 #tabs-content>div.active{
		 	display: block;
		 }
	</style>

</head>
<body>
	<div id="tabs-wrap">
		<ul id="tabs">
			<li data-tab="users" class='active'>Users</li>
			<li data-tab="groups">Groups</li>
			<li data-tab="position">Position</li>
		</ul>
		<div style="clear:both;"></div>
		<div id="tabs-content">
			<div data-tab="users" class='active'>Users...</div>
			<div data-tab="groups">Groups...</div>
			<div data-tab="position">Position...</div>
		</div>
	</div>


	<script src="jquery-1.10.2.min.js"></script>
	<script type="text/javascript">
	/*
	通过自定义事件方式实现
	选项卡状态切换回调彼此分离，代码更具有扩展性
	js值改变相应的active类，显示隐藏通过css控制
	*/
	jQuery.fn.tabs = function(control){
		var element = $(this);
		control = $(control);
		element.on('click', 'li', function(){
			var tabName = $(this).attr('data-tab');
			//点击选项卡时触发自定义事件
			element.trigger('change.tabs', tabName);
		});
		//绑定自定义事件
		element.on('change.tabs', function(e, tabName){
			element.find('li').removeClass('active');
			element.find('>[data-tab="'+tabName+'"]').addClass('active');
		});
		element.on('change.tabs', function(e, tabName){
			control.find('>[data-tab]').removeClass('active');
			control.find('>[data-tab="'+tabName+'"]').addClass('active')
		});
		var firstName = element.find('li:first').attr('data-tab');
		element.trigger('change.tabs', firstName);
		return this;
	};
	// 切换选项卡的动作和窗口的hash做关联，支持浏览器的前进后退按钮。
	$('ul#tabs').on('change.tabs', function(e, tabName){
		window.location.hash = tabName;
	})
	$(window).on('hashchange', function(){
		var tabName = window.location.hash.slice(1);
		$('ul#tabs').trigger('change.tabs', tabName);
	})
	// 初始化插件
	$('ul#tabs').tabs('#tabs-content');
	// 选中某个选项卡
	$('ul#tabs').trigger('change.tabs', 'position');
	</script>
</body>
</html>

```
