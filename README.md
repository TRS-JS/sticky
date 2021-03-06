# Sticky

---

[![Build Status](https://travis-ci.org/aralejs/sticky.png?branch=master)](https://travis-ci.org/aralejs/sticky)
[![Coverage Status](https://coveralls.io/repos/aralejs/sticky/badge.png?branch=master)](https://coveralls.io/r/aralejs/sticky)

实现侧边栏跟随滚动的效果，当滚动条滚动到一定距离时，指定区域变为 sticky 效果开始跟随页面。

例如 [brunch.io](http://brunch.io/) 和 [bootstrap](http://twitter.github.com/bootstrap/getting-started.html) 页面左边侧边栏的效果，或着请看 [演示](/sticky/examples/)。

实现原理是支持 `position: sticky` 的直接使用 CSS 实现, 不支持的浏览器(除 IE6 外)使用 `position: fixed`，对 IE6 进行 js 模拟。

> 原 `arale/fixed` 改名为 `arale/sticky`。

---


## 使用说明

### Sticky(element, marginTop, callback)

```javascript
seajs.use(["$", "sticky"], function($, sticky) {
    sticky("#stick", 30, function(status) {
        if (status) {
            seajs.log("stick");
        } else {
            seajs.log("unstick");
        }
    });
});
```

`element` 是指需要跟随滚动的目标元素，接受 jQuery selector 对象。

`marginTop` 指当元素距离当前可视窗口顶部的距离等于这个值时，开始触发跟随状态。

`callback` 当元素更改状态之后的回调函数, 具有一个参数 status, 为 true 表示是 stick 状态, 为 false 为 unstick 状态.

> 有几下三点注意:
>
>  1) 当 `marginTop` 设置的值超过元素本身在文档中的高度时, 就变为全局 fixed 效果
>
>  2) Sticky 对某些情况下的元素会向 DOM 中插入占位元素, 所以务必在 DOM ready 之后初始化该组件
>
>  3) 对于 ``position: static or relative`` 且 ``display`` 不为 ``none`` 的情况下, 会在当前元素后面插入宽高与元素相同的占位符.


### Sticky.fixed(element)

```javascript
seajs.use(["sticky"], function(sticky) {

    sticky.fix("#element-need-to-fixed");

});
```

`element` 是指需要 fixed 的目标元素，接受 jQuery selector 对象。

> 注意: 请自行设置元素的 `left, top` 等 CSS 属性。
