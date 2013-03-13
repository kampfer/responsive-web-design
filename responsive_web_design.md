#响应式网页设计

    2013-03-15 l.w.kampfer@gmail.com

---

###"响应式网页设计"的概念

2010年，Ethan Marcotte提出了"[响应式网页设计][1]"（Responsive Web Design）这个名词，指可以自动识别屏幕宽度、并做出相应调整的网页设计。

![Responsive Web Design][2]

Ethan Marcotte的[例子][3]

[bootstrap][4]

[1]: http://www.alistapart.com/articles/responsive-web-design/
[2]: http://image.beekka.com/blog/201205/bg2012050107.jpg
[3]: http://www.alistapart.com/d/responsive-web-design/ex/ex-site-flexible.html
[4]: http://twitter.github.com/bootstrap/

---

#"响应式网页设计"的目的?

>Responsive web design (RWD) is a web design approach aimed at crafting sites to provide 
an optimal viewing experience—easy reading and navigation with a minimum of resizing, panning, 
and scrolling—across a wide range of devices (from desktop computer monitors to mobile phones).

---

#"响应式网页设计"到底是怎么做到的？

---

###允许网页宽度自动调整

在html代码的头部，加入一行viewport元标签

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

什么是viewport?

1. visual viewport
2. layout viewport

[A tale of two viewports — part one][5]

[A tale of two viewports — part two][6]

[5]: http://www.quirksmode.org/mobile/viewports.html
[6]: http://www.quirksmode.org/mobile/viewports2.html

---

###不使用绝对宽度

使用百分比宽度：

    .row-fluid .span1 {
      width: 6.382978723404255%;
      *width: 6.329787234042553%;
    }

---

###相对大小的字体

字体也不能使用绝对大小（px），而只能使用相对大小（em）。

    h1 {
        font-size: 1.5em;
    }
    或
    h1 {
        font-size: 150%;
    }

---

###流动布局（fluid grid）

"流动布局"的含义是，各个区块的位置都是浮动的，不是固定不变的。

    .main {
        float: right;
        width: 70%; 
    }
    .leftBar {
        float: left;
        width: 25%;
    }

float的好处是，如果宽度太小，放不下两个元素，后面的元素会自动滚动到前面元素的下方，不会在水平方向overflow（溢出），避免了水平滚动条的出现。

---

###选择加载CSS

---

###CSS的@media规则

---

###图片的自适应（fluid image）

---

#"响应式网页"的不足

1.  更多的下载资源
2.  对开发人员更高的要求

---