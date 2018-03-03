---
layout: post
title: 关于innerText、textContent以及innerHTML的区别
date: 2018-03-02
description: "了解下这三者的区别，方便接下来更好的使用"
tag: HTML
---

***

### **textContent 和 innerText 的区别：**

`textContent `属性【标准】，IE 8 及更早的版本不支持此属性，其他浏览器都支持；

 网上很多博客文章里面提到 `innerText` 除了 Firefox 的所有浏览器属性都支持，查看了下 `MDN` 发现 `Firefox 45`及以上版本是支持这个属性的；
 
 因此在IE中，用` innerText` 代替 `textContent` 属性。

* `textContent` 会获取所有元素的内容，包括 <script> 和 <style> 元素，然而 `innerText` 不会。
* `innerText` 意识到样式，并且不会返回隐藏元素的文本，而 `textContent` 会。
* 由于 `innerText` 受 CSS 样式的影响，它会触发回流（`reflow`），但 `textContent` 不会。

### **textContent 和 innerHTML 的区别：**

`innerHTML` 返回 `HTML` 文本，通常，为了在元素中检索或写入文本，人们使用`innerHTML`。但是，`textContent` 通常具有更好的性能，因为文本不会被解析为HTML。此外，使用 `textContent` 可以防止 `XSS` 攻击。

### **innerText 和 innerHTML 的区别：**

`innerText` 返回或者设置DOM元素的文本; `innerHTML` 返回或者设置DOM元素的子元素

取值时 `innerText` 只会获取节点里面的文本信息，而 `innerHTML`  会获取节点下面的所有内容，包括 `标签`、`文本` 还有 `空格`。`innerHTML` 是符合 W3C 标准的属性，所有浏览器兼容，而 `innerText` 在 IE 浏览器中的兼容性更好，因此，尽可能地去使用 `innerHTML`，而少用 `innerText`.

IE中的 `innerText` 是需要对 `innerHTML` 的值进行： 
1. HTML转义（等同于 `XML` 转义，对 `<`、`&`等 `转义字符` 进行处理）； 
2. 经过 `HTML解释` 和 `CSS样式解释`； 
3. 随后又剔除格式信息 
之后留下的 `纯文本`。 
而 Firefox 中的 `textContent` 没有2、3步，在经过了 `HTML转义` 之后直接剔除所有 html 标签后得到的纯文本。

**关于outerHTML**

`outerHTML` 获取描述包括其后代的元素的序列化HTML片段。

举个栗子：

![](/images/posts/html/textContent-innerText-innerHTML-html.png "textContent、innerText和innerHTML的html代码")

js代码如下：

    var test = document.getElementById("test");
    console.log("testContent: " + test.textContent);
    console.log("innerText: " + test.innerText);
    console.log("innerHTML: " + test.innerHTML);
    console.log("outerHTML: " + test.outerHTML);

结果如下图：

![](/images/posts/html/textContent-innerText-innerHTML-js.png "结果展示")
