# js

1. 用递归算法实现，数组长度为5且元素的随机数在 2-32 间不重复的值？[链接](https://github.com/haizlin/fe-interview/issues/3)

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

2. 写一个方法去掉字符串中的空格？[链接](https://github.com/haizlin/fe-interview/issues/6)

写一个方法去掉字符串中的空格，要求传入不同的类型分别能去掉前、后、前后、中间的空格。

<details>
<summary>答案</summary>

* 去除中间空格使用了 ES2018 新增特性正则表达式的后行断言（lookbehind ），对浏览器有兼容性要求，具体兼容性请去 [caniuse](https://www.caniuse.com/?search=lookbehind) 查看。

```js
function trim (str, type = 'default') {
    if (str === '') return '';
    str = String(str);
    const reg = {
        left: /^ */g,
        right: / *$/g,
        both: /^ *| *$/g,
        middle: /(?<=[^ ]+) *(?=[^ ]+)/g,
        default: / */g
    };

    return str.replace(reg[type], '');
}
```
</details>
<br><br>

3. 去除字符串中最后一个指定的字符 [链接](https://github.com/haizlin/fe-interview/issues/9)

<details>
<summary>答案</summary>

```js
function removeStr (str, char) {
    let reg = new RegExp(`${char}(?=([^${char}]*)$)`)
    return str.replace(reg, '')
}

removeStr('ssdddfff123fcc', '123f')
```

```js
function delLast (str, del) {
    let index = str.lastIndexOf(del);
    return str.substring(0, index) + str.substring(index + del.length, str.length);
}
delLast('ssdddfff123fcc', '123f')
```
</details>
<br><br>