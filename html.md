# html

1. 页面导入样式时，使用 `<link>` 和 `@import` 有什么区别？[链接](https://github.com/haizlin/fe-interview/issues/1)

<details>
<summary>答案</summary>

* `<link>` 是 html 标签，规定当前文档和外部资源之间的关系，一般写在 `<head>` 元素中，而 `@import` 是 css 的 `@规则` 语句，用于在 css 中引入一个外部样式表，一般写在 `<style>` 元素和 css 文件的开头。
* `<link>` 引入的 css 会先于 `@import` 加载。
* `<link>` 可以被动态添加和移除，`@import` 不能。
* 它们的浏览器兼容性不一样，`@import` 要求需要高于 Internet Explorer 浏览器 5.5 以上。（现在基本可以忽略这个问题）

注意：有很多回答都说 `link引入的样式页面加载时同时加载` ，这样的说法不严谨，观察浏览器打开网站加载资源的顺序可以发现，等到文档下载完成之后才会去下载其他资源文件（css js 图片 等），在文档下载完成和开始下载其他资源文件中间，会有段时间没有下载请求，所以页面加载的同时是有可能和样式加载是重叠的，但还是有一个明显的先后顺序，毕竟最优先要把 html 文档下载下来才能去做其它事。
</details>
<br><br>

2. html 的元素有哪些？[链接](https://github.com/haizlin/fe-interview/issues/4)

<details>
<summary>答案</summary>

* 在 w3c 的规范文档 4.01 规范（[链接](https://www.w3.org/TR/html401/struct/global.html#h-7.5.3)）中是这么描述块级元素（block-level）和行内元素（inline-level）之间的区别的：

1. 内容模型： 通常，块级元素会包含行内元素或其他块级元素。而行内元素只能包含行内元素和数据。这种结构上的包含继承区别可以使块级元素创建比行内元素更”大型“的结构。

2. 格式：默认情况下，行内元素不会以新行开始，而块级元素会新起一行。

3. 内容的定向：unicode双向算法对于文本块会要求一个基础的文本方向。要为块级元素指定基础方向，就需要使用html元素的 `dir` 属性，`dir`属性的默认值是 `ltr`（从左往右）。

一旦为块级元素设置了 `dir` 属性，它会继续影响这个元素和它所有嵌套的块级元素，也就是说块级元素会继承 `dir` 属性。在嵌套元素身上设置新的 `dir` 属性才能覆盖掉继承的值。

如果要为整个文档设置基础文本方向，就在 `html` 元素上设置 `dir` 属性。

而对于行内元素来说，它不会继承 `dir` 属性。这就是说，一个没有 `dir` 属性的行内元素不会为了遵守双向算法而去为内嵌的元素开启一个额外层级。

下面是块级元素：

* `<address>` 表示其中的 HTML 提供了某个人或某个组织（等等）的联系信息。
* `<article>` HTML5 表示文档、页面、应用或网站中的独立结构，其意在成为可独立分配的或可复用的结构，如在发布中，它可能是论坛帖子、杂志或新闻文章、博客、用户提交的评论、交互式组件，或者其他独立的内容项目。​​。
* `<aside>` HTML5 表示一个和其余页面内容几乎无关的部分，被认为是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。其通常表现为侧边栏或者标注框。
* `<audio>` HTML5 用于在文档中嵌入音频内容。
* `<blockquote>` 块级引用元素，代表其中的文字是引用内容。。
* `<canvas>` HTML5 被用来通过JavaScript（Canvas API 或 WebGL API）绘制图形及图形动画。
* `<dd>` 用来指明一个描述列表  `<dl>` 元素中一个术语的描述。这个元素只能作为描述列表元素的子元素出现，并且必须跟着一个 `<dt>` 元素。
* `<div>` 是一个通用型的流内容容器，在不使用CSS的情况下，其对内容或布局没有任何影响。
* `<dl>` 包含术语定义以及描述的列表。
* `<fieldset>` 用于对表单中的控制元素进行分组。
* `<figcaption>` HTML5 是与其相关联的图片的说明/标题，用于描述其父节点 `<figure>`元素里的其他数据。
* `<figure>` HTML5 代表一段独立的内容，通常来引用图片。
* `<footer>` HTML5 区段尾或页尾。
* `<form>` 表单。
* `<h1> <h2> <h3> <h4> <h5> <h6>` 标题。
* `<header>` HTML5 用于展示介绍性内容，通常包含一组介绍性的或是辅助导航的实用元素。它可能包含一些标题元素，但也可能包含其他元素，比如 Logo、搜索框、作者名称，等等。
* `<hgroup>` HTML5 标题组。
* `<hr>` 水平分割线。
* `<noscript>` 不支持脚本或禁用脚本时显示的内容。
* `<ol>` 有序列表。
* `<output>` HTML5 表示计算或用户操作的结果。
* `<p>` 段落。
* `<pre>` 预格式化文本。
* `<section>` HTML5 一个页面区段。
* `<table>` 表格。
* `<tfoot>` 表脚注。
* `<ul>` 无序列表。
* `<video>` HTML5 视频。

下面是行内元素：

* `<b>` 提醒注意（Bring Attention To）元素（注意，这个元素的语义并不是粗体，粗体请使用 css 样式 font-weight）
* `<i>` 表现一系列带有不同语义的文本，它的典型样式显示为斜体。
* `<small>` 使文本的字体变小一号。HTML5中，除了它的样式含义，这个元素被重新定义为表示边注释和附属细则，包括版权和法律文本。
* `<abbr>` 缩写元素。可以通过可选的 title 属性提供完整的描述。
* `<cite>` 表示一个作品的引用，且必须包含作品的标题。
* `<code>` 呈现一段计算机代码. 默认情况下, 它以浏览器的默认等宽字体显示。
* `<dfn>` 定义元素。表示一个术语的定义。
* `<em>` 着重元素。标记出需要用户着重阅读的内容， `<em>` 元素是可以嵌套的，嵌套层次越深，则其包含的内容被认定为越需要着重阅读。
* `<kbd>` 键盘输入元素用于表示用户输入，它将产生一个行内元素，以浏览器的默认 monospace 字体显示。
* `<strong>` 表示文本十分重要，一般用粗体显示。
* `<samp>` 标识计算机程序输出，通常使用浏览器缺省的 monotype 字体
* `<var>` 表示数学表达式或编程上下文中的变量名称。尽管该行为取决于浏览器，但通常使用当前字体的斜体形式显示。
* `<a>` 锚元素。用于创建超链接。
* `<bdo>` 双向文本替代元素改写了文本的方向性, 使文本以不同的方向渲染呈现出来。
* `<br>` 在文本中生成一个换行（回车）符号。
* `<img>` 图片。
* `<map>` 和 `<area>` 配合定义一个图像映射(一个可点击的链接区域)。
* `<object>` 表示引入一个外部资源，这个资源可能是一张图片，一个嵌入的浏览上下文，亦或是一个插件所使用的资源。
* `<q>` 表示一个封闭的并且是短的行内引用的文本. 这个标签是用来引用短的文本，所以请不要引入换行符; 对于长的文本的引用请使用 `<blockquote>` 替代.
* `<script>` 用于嵌入或引用可执行脚本。这通常用作嵌入或者指向 JavaScript 代码。
* `<span>` 短语内容的通用行内容器，并没有任何特殊语义。
* `<sub>` 定义了一个文本区域，出于排版的原因，与主要的文本相比，应该展示得更低并且更小。
* `<sup>`定义了一个文本区域，出于排版的原因，与主要的文本相比，应该展示得更高并且更小。
* `<buttom>` 表示一个可点击的按钮。
* `<input>` 用于为基于Web的表单创建交互式控件。
* `<label>` 表示用户界面中某个元素的说明。
* `<select>` 表示一个提供选项菜单的控件。
* `<textarea>` 表示一个多行纯文本编辑控件。

***

* 块级元素和行内元素只是过去规范的定义。如今最新的 html 规范对元素的分类是根据元素所包含内容来决定的。这就是内容模型（Content models）。详见 WHATWG 维护的 [html 规范](https://html.spec.whatwg.org/multipage/dom.html#content-models) 以及 [MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Content_categories)。


根据内容模型进行的分类主要有三种：

1. 主内容类，描述了很多元素共享的内容规范；

元数据内容（Metadata content）: `<base>, <link>, <meta>, <noscript>, <script>, <style>, <title>`
流式元素（Flow content）:` <a>, <abbr>, <address>, <article>, <aside>, <audio>, <b>,<bdo>, <bdi>, <blockquote>, <br>, <button>, <canvas>, <cite>, <code>, <data>, <datalist>, <del>, <details>, <dfn>, <div>, <dl>, <em>, <embed>, <fieldset>, <figure>, <footer>, <form>, <h1>, <h2>, <h3> , <h4>, <h5>, <h6>, <header>, <hgroup>, <hr>, <i>, <iframe>, <img>, <input>, <ins>, <kbd>, <label>, <main>, <map>, <mark>, <math>, <menu>, <meter>, <nav>, <noscript>, <object>, <ol>, <output>, <p>, <pre>, <progress>, <q>, <ruby>, <s>, <samp>, <script>, <section>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <svg>, <table>, <template>, <textarea>, <time>, <ul>, <var>, <video>, <wbr>, Text`
章节元素（Sectioning content）: ` <article>, <aside>, <nav>, <section>`
标题元素（Heading content）: `<h1>, <h2>, <h3> , <h4>, <h5>, <h6>, <hgroup>`
短语元素（Phrasing content）: ` <abbr>, <audio>, <b>, <bdo>, <br>, <button>, <canvas>, <cite>, <code>, <datalist>, <dfn>, <em>, <embed>, <i>, <iframe>, <img>, <input>, <kbd>, <label>, <mark>, <math>, <meter>, <noscript>, <object>, <output>, <progress>, <q>, <ruby>, <samp>, <script>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <svg>, <textarea>, <time>, <var>, <video>, <wbr>, plain text `
嵌入元素（Embedded content）: `<audio>, <canvas>, <embed>, <iframe>, <img>, <math>, <object>, <svg>, <video>`
交互元素（Interactive content）: `<a>，<button>，<details>，<embed>，<iframe>，<label>，<select>, <textarea>`


2. 表单相关的内容类，描述了表单相关元素共有的内容规范；

`<button> <fieldset><input> <label> <meter> <object> <output> <progress> <select> <textarea>`

3. 特殊内容类，描述了仅仅在某些特殊元素上才需要遵守的内容规范，通常这些元素都有特殊的上下文关系。

`<script> <template> <del>, <ins>`

</details>
<br><br>

3. HTML全局属性(global attribute)有哪些？[链接](https://github.com/haizlin/fe-interview/issues/7)

<details>
<summary>答案</summary>

|  属性  | 描述  |
| ------ | ------ |
|  accesskey  | 为当前元素生成快捷键 |
|  autocapitalize  | 控制用户的文本输入是否和如何自动大写 |
|  class  | 以空格分隔的元素的类名（classes ）列表，它允许 CSS 和 Javascript 通过类选择器或DOM方法来选择和访问特定的元素 |
|  contenteditable  | 表示元素是否可被用户编辑，值为 true 或 false |
|  data-*  | 自定义数据属性，HTMLElement.dataset 属性可以访问这些数据 |
|  dir  | 指示元素中文本方向 |
|  draggable  | 指示是否可以 使用 Drag and Drop API (en-US) 拖动元素。 |
|  hidden  | 表示一个元素尚未或者不再相关。例如，它可以被用来隐藏一个页面元素直到登录完毕。如果一个元素设置了这个属性，它就不会被显示。 |
|  id  | 唯一标识符 |
|  inputmode  | 提供了用户在编辑元素或其内容时可能输入的数据类型的提示 |
|  is  | 允许您指定标准HTML元素应该像已注册的自定义内置元素一样 |
|  lang  | 元素语言的定义 |
|  style  | CSS样式 |
|  tabindex  | 元素是否可以获取输入焦点（可聚焦），是否应该参与顺序键盘导航 |
|  title  | 包含表示与其所属元素相关信息的文本 |



* autocapitalize 控制用户的文本输入是否和如何自动大写，它可以有以下的值：
    * off or none，没有应用自动大写（所有字母都默认为小写字母）。
    * on or sentences，每个句子的第一个字母默认为大写字母;所有其他字母都默认为小写字母。
    * words，每个单词的第一个字母默认为大写字母;所有其他字母都默认为小写字母。
    * characters，所有的字母都应该默认为大写。
* dir 指示元素中文本方向
    * ltr, 指从左到右，用于那种从左向右书写的语言（比如英语）；
    * rtl, 指从右到左，用于那种从右向左书写的语言（比如阿拉伯语）；
    * auto, 指由用户代理决定方向。
* inputmode 提供了用户在编辑元素或其内容时可能输入的数据类型的提示
    * "none" 无虚拟键盘。在应用程序或者站点需要实现自己的键盘输入控件时很有用。
    * "text"使用用户本地区域设置的标准文本输入键盘。
    * "decimal"小数输入键盘，包含数字和分隔符（通常是“ . ”或者“ , ”），设备可能也可能不显示减号键。
    * "numeric"数字输入键盘，所需要的就是0到9的数字，设备可能也可能不显示减号键。
    * "tel"电话输入键盘，包含0到9的数字、星号（*）和井号（#）键。表单输入里面的电话输入通常应该使用 `<input type="tel">` 。
    * "search"为搜索输入优化的虚拟键盘，比如，返回键可能被重新标记为“搜索”，也可能还有其他的优化。
    * "email"为邮件地址输入优化的虚拟键盘，通常包含"@"符号和其他优化。表单里面的邮件地址输入应该使用 `<input type="email">` 。
    * "url"为网址输入优化的虚拟键盘，比如，“/”键会更加明显、历史记录访问等。表单里面的网址输入通常应该使用 `<input type="url">` 。

[参考链接](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes)
</details>
<br><br>

