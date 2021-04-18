# css

1. 圣杯布局和双飞翼布局的理解和区别，并用代码实现 [链接](https://github.com/haizlin/fe-interview/issues/2)

<details>
<summary>答案</summary>

* 圣杯布局和双飞翼布局解决的问题是一样的，就是两边顶宽，中间自适应的三栏布局。
* 圣杯布局，为了中间 div 内容不被遮挡，将中间 div 设置了左右 padding-left 和 padding-right 后，将左右两个 div 用相对布局 position: relative并分别配合 right 和 left 属性，以便左右两栏 div 移动后不遮挡中间 div。双飞翼布局，为了中间 div 内容不被遮挡，直接在中间 div 内部创建子 div 用于放置内容，在该子 div 里用 margin-left 和 margin-right 为左右两栏 div 留出位置。

圣杯：

```html
<body>
<div id="hd">header</div>
<div id="bd">
  <div id="middle">middle</div>
  <div id="left">left</div>
  <div id="right">right</div>
</div>
<div id="footer">footer</div>
</body>

<style>
#hd{
    height:50px;
    background: #666;
    text-align: center;
}
#bd{
    /*左右栏通过添加负的margin放到正确的位置了，此段代码是为了摆正中间栏的位置*/
    padding:0 200px 0 180px;
    height:100px;
}
#middle{
    float:left;
    width:100%;/*左栏上去到第一行*/
    height:100px;
    background:blue;
}
#left{
    float:left;
    width:180px;
    height:100px;
    margin-left:-100%;
    background:#0c9;
    /*中间栏的位置摆正之后，左栏的位置也相应右移，通过相对定位的left恢复到正确位置*/
    position:relative;
    left:-180px;
}
#right{
    float:left;
    width:200px;
    height:100px;
    margin-left:-200px;
    background:#0c9;
    /*中间栏的位置摆正之后，右栏的位置也相应左移，通过相对定位的right恢复到正确位置*/
    position:relative;
    right:-200px;
}
#footer{
    height:50px;
    background: #666;
    text-align: center;
}
</style>
```

双飞翼

```html
<body>
<div id="hd">header</div> 
  <div id="middle">
    <div id="inside">middle</div>
  </div>
  <div id="left">left</div>
  <div id="right">right</div>
  <div id="footer">footer</div>
</body>

<style>
#hd{
    height:50px;
    background: #666;
    text-align: center;
}
#middle{
    float:left;
    width:100%;/*左栏上去到第一行*/     
    height:100px;
    background:blue;
}
#left{
    float:left;
    width:180px;
    height:100px;
    margin-left:-100%;
    background:#0c9;
}
#right{
    float:left;
    width:200px;
    height:100px;
    margin-left:-200px;
    background:#0c9;
}

/*给内部div添加margin，把内容放到中间栏，其实整个背景还是100%*/ 
#inside{
    margin:0 200px 0 180px;
    height:100px;
}
#footer{  
   clear:both; /*记得清楚浮动*/  
   height:50px;     
   background: #666;    
   text-align: center; 
} 
</style>
```
</details>
<br><br>

2. 在页面上隐藏元素的方法有哪些？[链接](https://github.com/haizlin/fe-interview/issues/8)

<details>
<summary>答案</summary>

|  方法  | 是否占据空间  | 是否响应事件 | 补充说明 |
| ------ | ------ | ------ | ------ |
|  display: none;  |  否 |  否  |  会引起回流和重绘  |
|  visibility: hidden;  |  是 |  否  |  -  |
|  opacity: 0;  |  是 |  是  |  会引起重绘  |
|  position: absolute;top: -100px;将元素移除可见区域  |  是 |  -  |  -  |
|  transform: scale(0);将元素缩放为 0 尺寸  |  是 |  否  |  -  |
|  z-index: -999;层级调低的同时在同样的位置上用其他元素覆盖  |  是 |  否  |  -  |
|  ransform: rotateY(90deg);或transform: rotateX(90deg);使元素在 x/y 轴不可见  |  是 |  -  |  -  |
</details>
<br><br>