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

字体也不使用绝对大小（px），而只能使用相对大小（em）。

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
    
    <link rel="stylesheet" type="text/css"
    media="screen and (min-width: 400px) and (max-device-width: 600px)"
    href="smallScreen.css" />

    @import url("tinyScreen.css") screen and (max-device-width: 400px);

---

###CSS的@media规则

    @media screen and (max-device-width: 400px) {
        .column {float: none;
            width:auto;
        }
        #sidebar {
            display:none;
        }
    }

---

###更进一步--bootstrap的做法

1.  Modify the width of column in our grid
2.  Stack elements instead of float wherever necessary
3.  Resize headings and text to be more appropriate for devices

---

###图片的自适应（Responsive IMGs）

    img { max-width: 100%;}

    ####race condition

    Techniques that rely on adjusting the image source attribute 
    via javascript need to make sure that the modification happens 
    before the image requests start.

---

####1. Dynamic Base Tag

    The <base> tag specifies the base URL/target for all relative URLs 
    in a document. There can be at maximum one <base> element in a 
    document, and it must be inside the <head> element.

缺陷:

Google Chrome was downloading both the mobile and desktop images

一个[Demo](http://jsbin.com/umulij/8)

---

####2. Temporary images(*)
    
    Another early technique was to have the src of imgs pointing to a 
    temporary image and then having javascript replace the source with 
    the correct file path. In most cases, the image was an one pixel 
    transparent gif set up with caching which would hopefully prevent 
    the browser from requesting it more than once no matter how many 
    times it was referenced in the page.

---

####3. CSS3 image

在CSS3中，任何元素都可以使用content属性

    <img src="image.jpg" 
    data-src-600px="image-600px.jpg" 
    data-src-800px="image-800px.jpg" alt="">

    @media (min-device-width:600px) { 
        img[data-src-600px] {
            content: attr(data-src-600px, url); 
        }
    }
    @media (min-device-width:800px) {
        img[data-src-800px] {
            content: attr(data-src-800px, url);
        }
    }

---

####4. URL parameters

    <img src="small.jpg?full=large.jpg" />

.htaccess

    RewriteEngine On
    #large cookie, large image
    RewriteCond %{HTTP_COOKIE} rwd-screensize=large
    RewriteCond %{QUERY_STRING} large=([^&]+)
    RewriteRule .* %1 [L]

####5. Data attributes(*)

    <img src=”small.r.jpg” data-fullsrc=”large.jpg” />

---

####6. Assumed file structure
    
    the images are put on the server in a regular fashion. 
    For example, all small images might be in /images/sml/ 
    whereas large images are in /images/lrg/.

可以考虑和Temporary images一起使用

####7. Dynamic file names

    pass the dimensions that you want in the url and get back
    an image at that size. Javascript will modify the filename 
    from something like ‘boat.jpg’ to ‘boat-480×200.jpg’.

---

####8. Set a cookie

    Javascript is inserted into the head of the document so that 
    it evaluates as soon as possible. After it determines the screen 
    size, it sets a cookie. Every subsequent image request sent from 
    the browser will include the cookie. The server can use the cookie 
    to determine the best image to sent back to the user.

    duplicate files will be downloaded by IE9. Firefox will download 
    duplicate files if the script is external, but not if it internal. 

[test](http://filamentgroup.com/examples/responsive-images-new/demos/A-Default/demo.html)

---

####9. Noscript tag

    <noscript data-large='Koala.jpg' data-small='Koala-small.jpg' data-alt='Koala'>
        <img src='Koala.jpg' alt='Koala' />
    </noscript>

    $('noscript[data-large][data-small]').each(function(){
        var src = screen.width >= 500 ? $(this).data('large') : $(this).data('small');
        $('<img src="' + src + '" alt="' + $(this).data('alt') + '" />').insertAfter($(this));
    });

---

#"响应式网页"的争论

响应式网页设计被提出以来，争论就不断，其实核心问题只有两个个：太多的资源请求和有限的终端支持之间的矛盾、响应式的网页设计和移动终端在用户体验和视觉风格上的差异。

---

#"响应式网页"的应用场景？？

    神飞：
    我的想法是，具体问题具体分析，比如，强内容的网站，
    完全可以尝试响应式网站，而重视觉和功能的网站，
    则可以尝试建立一个独立的移动网站。

---

###参考资料
1.  [自适应网页设计（Responsive Web Design）](http://www.ruanyifeng.com/blog/2012/05/responsive_web_design.html)
2.  [Responsive IMGs Part 2](http://blog.cloudfour.com/responsive-imgs-part-2/)
3.  [Responsive IMGs — Part 1](http://blog.cloudfour.com/responsive-imgs/)
4.  [响应式网页设计](http://www.qianduan.net/responsive-web-design.html)
5.  [wiki](http://en.wikipedia.org/wiki/Responsive_web_design)
6.  [bootstrap](http://twitter.github.com/bootstrap/)
