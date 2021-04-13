# learn-haizlin-fe-interview

学习整理 [haizlin](https://github.com/haizlin) 的[前端题](https://github.com/haizlin/fe-interview)

<br><br><br>

***

1. `html` 页面导入样式时，使用 `<link>` 和 `@import` 有什么区别？[链接](https://github.com/haizlin/fe-interview/issues/1)

<details>
<summary>答案</summary>

* `<link>` 是 html 标签，规定当前文档和外部资源之间的关系，一般写在 `<head>` 元素中，而 `@import` 是 css 的 `@规则` 语句，用于在 css 中引入一个外部样式表，一般写在 `<style>` 元素和 css 文件的开头。
* `<link>` 引入的 css 会先于 `@import` 加载。
* `<link>` 可以被动态添加和移除，`@import` 不能。
* 它们的浏览器兼容性不一样，`@import` 要求需要高于 Internet Explorer 浏览器 5.5 以上。（现在基本可以忽略这个问题）

注意：有很多回答都说 `link引入的样式页面加载时同时加载` ，这样的说法不严谨，观察浏览器打开网站加载资源的顺序可以发现，等到文档下载完成之后才会去下载其他资源文件（css js 图片 等），在文档下载完成和开始下载其他资源文件中间，会有段时间没有下载请求，所以页面加载的同时是有可能和样式加载是重叠的，但还是有一个明显的先后顺序，毕竟最优先要把 html 文档下载下来才能去做其它事。
</details>
<br><br>

2. `css` 圣杯布局和双飞翼布局的理解和区别，并用代码实现 [链接](https://github.com/haizlin/fe-interview/issues/2)

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

3. `js` 用递归算法实现，数组长度为5且元素的随机数在 2-32 间不重复的值？[链接](https://github.com/haizlin/fe-interview/issues/3)

这一题是起源题，描述：<br>

这是一道大题目，把考点拆成了4个小项；需要侯选人用递归算法实现（限制15行代码以内实现；限制时间10分钟内完成）：

* a) 生成一个长度为5的空数组arr。
* b) 生成一个（2－32）之间的随机整数rand。
* c) 把随机数rand插入到数组arr内，如果数组arr内已存在与rand相同的数字，则重新生成随机数rand并插入到arr内[需要使用递归实现，不能使用for/while等循环]
* d) 最终输出一个长度为5，且内容不重复的数组arr。

<details>
<summary>答案</summary>

```js
function randomArr (count, min, max, arr = []) {
    if (arr.length < count) {
        let t = Math.floor(Math.random() * (max - min + 1)) + min;
        while (arr.includes(t)) {
            t = Math.floor(Math.random() * (max - min + 1)) + min
        }
        arr.push(t);
        return randomArr(count--, min, max, arr);
    } else {
        return arr;
    }
}
```

不允许使用循环，改写一下：

```js
function randomArr (count, min, max, arr = []) {
    if (arr.length < count) {
        let t = Math.floor(Math.random() * (max - min + 1)) + min;
        if (arr.includes(t)) {
            return randomArr(count, min, max, arr);
        } else {
            arr.push(t);
            return randomArr(count--, min, max, arr);
        }
    } else {
        return arr;
    }
}
```

优化一下代码行数：

```js
function randomArr (count, min, max, arr = []) {
    let t = Math.floor(Math.random() * (max - min + 1)) + min;
    if (!arr.includes(t)) {
        arr.push(t);
    }
    return arr.length < count ? randomArr(count, min, max, arr) : arr;
}
```

衍生知识点：尾递归优化<br>

如果生成的是小数，而不是整数，这样实现就会有个缺点，没有尾递归优化，当调用次数太多的时候会调用栈溢出。于是写一个包装函数进行优化：

```js
function tco(f) {
  var value;
  var active = false;
  var accumulated = [];

  return function accumulator() {
    accumulated.push(arguments);
    if (!active) {
      active = true;
      while (accumulated.length) {
        value = f.apply(this, accumulated.shift());
      }
      active = false;
      return value;
    }
  };
}

const randomArr = tco(function (count, min, max, arr = []) {
    if (arr.length < count) {
        let t = Math.random() * (max - min + 1) + min;
        while (arr.includes(t)) {
            t = Math.random() * (max - min + 1) + min
        }
        arr.push(t);
        return randomArr(count--, min, max, arr);
    } else {
        return arr;
    }
})
```

这样优化后就不会调用栈溢出了。
</details>
<br><br>