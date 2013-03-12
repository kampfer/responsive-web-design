#响应式网页设计

    2013-03-15 l.w.kampfer@gmail.com

---

###"响应式网页设计"的概念

2010年，Ethan Marcotte提出了"[响应式网页设计][1]"（Responsive Web Design）这个名词，指可以自动识别屏幕宽度、并做出相应调整的网页设计。

![Responsive Web Design][2]

Ethan Marcotte失败的[例子][3]

一个成功的[例子][4]

[1]: http://www.alistapart.com/articles/responsive-web-design/
[2]: http://image.beekka.com/blog/201205/bg2012050107.jpg
[3]: http://www.alistapart.com/d/responsive-web-design/ex/ex-site-flexible.html
[4]: http://twitter.github.com/bootstrap/

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

    width: xx%;

或者

    width:auto;

---

###相对大小的字体

---

###流动布局（fluid grid）

---

###选择加载CSS

---

###CSS的@media规则

---

###图片的自适应（fluid image）