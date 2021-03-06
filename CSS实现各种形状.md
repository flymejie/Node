# [CSS实现各种形状](https://www.cnblogs.com/liangxiaofeng/p/5936760.html)

[CSS3](http://www.htmleaf.com/css3/)的一个非常酷的特性是允许我们创建各种规则和不规则形状的图形，从而可以减少图片的使用。以前只能在Photoshop等图像编辑软件中制作的复杂图形现在使用CSS3就可以完成了。通过使用新的CSS属性，像[transform](http://www.w3schools.com/cssref/css3_pr_transform.asp)和[border-radius](http://www.w3schools.com/cssref/css3_pr_border-radius.asp)，我们可以创建非常漂亮和复杂的图形效果。

#####  圆形

 

要使用CSS来制作一个圆形，我们需要一个`div`，被给它设置一个ID。

```
`<``div` `id``=``"circle"``></``div``>                              `
```

圆形在设置CSS时要设置宽度和高度相等，然后设置`border-radius`属性为宽度或高度的一半即可：

```
`#``circle` `{``    ``width``: ``120px``;``    ``height``: ``120px``;``    ``background``: ``#7fee1d``;``    ``-moz-``border-radius``: ``60px``;``    ``-webkit-``border-radius``: ``60px``;``    ``border-radius``: ``60px``;``}                              `
```

#####  正方形

 

正方形是CSS图形中最简单的图形之一，同样使用一个`div`，并设置一个ID。

```
`<``div` `id``=``"square"``></``div``>                              `
```

正方形的CSS样式只需要设置相同的宽度和高度即可。

```
`#``square` `{``    ``width``: ``120px``;``    ``height``: ``120px``;``    ``background``: ``#f447ff``;``}                              `
```

#####  长方形

 

与正方形一样，CSS长方形也非常简单：

```
`<``div` `id``=``"rectangle"``></``div``>                              `
```

与正方形不同的是，长方形的长度和高度为不同的值。

```
`#rectangle {``    ``width``: ``220px``;``    ``height``: ``120px``;``    ``background``: ``#4da1f7``;``}                              `
```

#####  椭圆形

 

椭圆形是正圆形的一个变体，同样使用一个带ID的`div`来制作。

```
`<``div` `id``=``"oval"``></``div``>                              `
```

设置椭圆形的CSS时，高度要设置为宽度的一半，`border-radius`属性也要做相应的改变：

```
`#oval {``    ``width``: ``200px``;``    ``height``: ``100px``;``    ``background``: ``#e9337c``;``    ``-webkit-``border-radius``: ``100px` `/ ``50px``;``    ``-moz-``border-radius``: ``100px` `/ ``50px``;``    ``border-radius``: ``100px` `/ ``50px``;``}                             `
```

#####  三角形

 

要创建一个CSS三角形，需要使用`border`，通过设置不同边的透明效果，我们可以制作出三角形的现状。另外，在制作三角形时，宽度和高度要设置为0。

```
`<``div` `id``=``"triangle"``></``div``>                              `
```

#####  倒三角形

 

与正三角形不同的是，倒三角形要设置的是`border-top`、`border-left`和`border-right`三条边的属性：

```
`#triangle {``    ``width``: ``0``;``    ``height``: ``0``;``    ``border-top``: ``140px` `solid` `#20a3bf``;``    ``border-left``: ``70px` `solid` `transparent``;``    ``border-right``: ``70px` `solid` `transparent``;``}                              `
```

#####  左三角形

 

左三角形操作的是`border-top`、`border-left`和`border-right`三条边的属性，其中上边和下边要设置透明属性。

```
`#triangle_left {``    ``width``: ``0``;``    ``height``: ``0``;``    ``border-top``: ``70px` `solid` `transparent``;``    ``border-right``: ``140px` `solid` `#6bbf20``;``    ``border-bottom``: ``70px` `solid` `transparent``;``}                             `
```

#####  右三角形

 

右三角形操作的是`border-bottom`、`border-left`和`border-right`三条边的属性，其中上边和下边要设置透明属性。

```
`#triangle_right {``    ``width``: ``0``;``    ``height``: ``0``;``    ``border-top``: ``70px` `solid` `transparent``;``    ``border-left``: ``140px` `solid` `#ff5a00``;``    ``border-bottom``: ``70px` `solid` `transparent``;``}                              `
```

#####  菱形

 

制作菱形的方法有很多种。这里使用的是`transform`属性和`rotate`相结合，使两个正反三角形上下显示。

```
`#diamond {``    ``width``: ``120px``;``    ``height``: ``120px``;``    ``background``: ``#1eff00``;``/* Rotate */``    ``-webkit-``transform``: ``rotate``(``-45``deg);``    ``-moz-``transform``: ``rotate``(``-45``deg);``    ``-ms-``transform``: ``rotate``(``-45``deg);``    ``-o-``transform``: ``rotate``(``-45``deg);``    ``transform``: ``rotate``(``-45``deg);``/* Rotate Origin */``    ``-webkit-``transform-origin``: ``0` `100%``;``    ``-moz-``transform-origin``: ``0` `100%``;``    ``-ms-``transform-origin``: ``0` `100%``;``    ``-o-``transform-origin``: ``0` `100%``;``    ``transform-origin``: ``0` `100%``;``    ``margin``: ``60px` `0` `10px` `310px``;``}                              `
```

#####  梯形

 

梯形是三角形的一个变体，设置CSS梯形时，左右两条边设置为相等，并且给它设置一个宽度。

```
`#trapezium {``    ``height``: ``0``;``    ``width``: ``120px``;``    ``border-bottom``: ``120px` `solid` `#ec3504``;``    ``border-left``: ``60px` `solid` `transparent``;``    ``border-right``: ``60px` `solid` `transparent``;``}                              `
```

#####  平行四边形

 

平行四边形的制作方式是使用`transform`属性使长方形倾斜一个角度。

```
`#parallelogram {``    ``width``: ``160px``;``    ``height``: ``100px``;``    ``background``: ``#8734f7``;``    ``-webkit-``transform``: skew(``30``deg);``    ``-moz-``transform``: skew(``30``deg);``    ``-o-``transform``: skew(``30``deg);``    ``transform``: skew(``30``deg);``}                              `
```

#####  星形

 

星形的HTML结构同样使用一个带ID的空`div`。星形的实现方式比较复杂，主要是使用`transform`属性来旋转不同的边。仔细体会下面的代码。

```
`#star {``    ``width``: ``0``;``    ``height``: ``0``;``    ``margin``: ``50px` `0``;``    ``color``: ``#fc2e5a``;``    ``position``: ``relative``;``    ``display``: ``block``;``    ``border-right``: ``100px` `solid` `transparent``;``    ``border-bottom``: ``70px` `solid` `#fc2e5a``;``    ``border-left``: ``100px` `solid` `transparent``;``    ``-moz-``transform``: ``rotate``(``35``deg);``    ``-webkit-``transform``: ``rotate``(``35``deg);``    ``-ms-``transform``: ``rotate``(``35``deg);``    ``-o-``transform``: ``rotate``(``35``deg);``}`` ` `#star:before {``    ``height``: ``0``;``    ``width``: ``0``;``    ``position``: ``absolute``;``    ``display``: ``block``;``    ``top``: ``-45px``;``    ``left``: ``-65px``;``    ``border-bottom``: ``80px` `solid` `#fc2e5a``;``    ``border-left``: ``30px` `solid` `transparent``;``    ``border-right``: ``30px` `solid` `transparent``;``    ``content``: ``''``;``    ``-webkit-``transform``: ``rotate``(``-35``deg);``    ``-moz-``transform``: ``rotate``(``-35``deg);``    ``-ms-``transform``: ``rotate``(``-35``deg);``    ``-o-``transform``: ``rotate``(``-35``deg);``}`` ` `#star:after {``    ``content``: ``''``;``    ``width``: ``0``;``    ``height``: ``0``;``    ``position``: ``absolute``;``    ``display``: ``block``;``    ``top``: ``3px``;``    ``left``: ``-105px``;``    ``color``: ``#fc2e5a``;``    ``border-right``: ``100px` `solid` `transparent``;``    ``border-bottom``: ``70px` `solid` `#fc2e5a``;``    ``border-left``: ``100px` `solid` `transparent``;``    ``-webkit-``transform``: ``rotate``(``-70``deg);``    ``-moz-``transform``: ``rotate``(``-70``deg);``    ``-ms-``transform``: ``rotate``(``-70``deg);``    ``-o-``transform``: ``rotate``(``-70``deg);``}                              `
```

#####  六角星形

![CSS六角星形](http://img.htmleaf.com/1504/star_six_points.jpg)

和五角星的制作方法不同，六角星形状的制作方法是操纵`border`属性来制作两半图形，然后合并它们。

```
`#star_six_points {``    ``width``: ``0``;``    ``height``: ``0``;``    ``display``: ``block``;``    ``position``: ``absolute``;``    ``border-left``: ``50px` `solid` `transparent``;``    ``border-right``: ``50px` `solid` `transparent``;``    ``border-bottom``: ``100px` `solid` `#de34f7``;``    ``margin``: ``10px` `auto``;``}`` ` `#star_six_points:after {``    ``content``: ``""``;``    ``width``: ``0``;``    ``height``: ``0``;``    ``position``: ``absolute``;``    ``border-left``: ``50px` `solid` `transparent``;``    ``border-right``: ``50px` `solid` `transparent``;``    ``border-top``: ``100px` `solid` `#de34f7``;``    ``margin``: ``30px` `0` `0` `-50px``;``}                              `
```

#####  五边形

![CSS五边形](http://img.htmleaf.com/1504/pentagon.jpg)

创建CSS五边形需要结合两个图形：一个梯形，然后在它的上面放一个三角形，共同组成一个五边形。

```
`#pentagon {``    ``width``: ``54px``;``    ``position``: ``relative``;``    ``border-width``: ``50px` `18px` `0``;``    ``border-style``: ``solid``;``    ``border-color``: ``#277bab` `transparent``;``}`` ` `#pentagon:before {``    ``content``: ``""``;``    ``height``: ``0``;``    ``width``: ``0``;``    ``position``: ``absolute``;``    ``top``: ``-85px``;``    ``left``: ``-18px``;``    ``border-width``: ``0` `45px` `35px``;``    ``border-style``: ``solid``;``    ``border-color``: ``transparent` `transparent` `#277bab``;``}                              `
```

#####  六边形

 

六边形的制作方法可以有很多种，可以像五边形一样，先制作一个长方形，然后在它的上面和下面各放置一个三角形。

```
`#hexagon {``    ``width``: ``100px``;``    ``height``: ``55px``;``    ``background``: ``#fc5e5e``;``    ``position``: ``relative``;``    ``margin``: ``10px` `auto``;``}`` ` `#hexagon:before {``    ``content``: ``""``;``    ``width``: ``0``;``    ``height``: ``0``;``    ``position``: ``absolute``;``    ``top``: ``-25px``;``    ``left``: ``0``;``    ``border-left``: ``50px` `solid` `transparent``;``    ``border-right``: ``50px` `solid` `transparent``;``    ``border-bottom``: ``25px` `solid` `#fc5e5e``;``}`` ` `#hexagon:after {``    ``content``: ``""``;``    ``width``: ``0``;``    ``height``: ``0``;``    ``position``: ``absolute``;``    ``bottom``: ``-25px``;``    ``left``: ``0``;``    ``border-left``: ``50px` `solid` `transparent``;``    ``border-right``: ``50px` `solid` `transparent``;``    ``border-top``: ``25px` `solid` `#fc5e5e``;``}                              `
```

#####  八角形

![CSS八角形](http://img.htmleaf.com/1504/octagon.jpg)

八角形的制作方法也有多种方式，这里使用的是先制作两个相同的梯形，然后在两边分别放置一个三角形。

```
`#octagon {``    ``width``: ``100px``;``    ``height``: ``100px``;``    ``background``: ``#ac60ec``;``    ``position``: ``relative``;``}`` ` `#octagon:before {``    ``content``: ``""``;``    ``width``: ``42px``;``    ``height``: ``0``;``    ``position``: ``absolute``;``    ``top``: ``0``;``    ``left``: ``0``;``    ``border-bottom``: ``29px` `solid` `#ac60ec``;``    ``border-left``: ``29px` `solid` `#f4f4f4``;``    ``border-right``: ``29px` `solid` `#f4f4f4``;``}`` ` `#octagon:after {``    ``content``: ``""``;``    ``width``: ``42px``;``    ``height``: ``0``;``    ``position``: ``absolute``;``    ``bottom``: ``0``;``    ``left``: ``0``;``    ``border-top``: ``29px` `solid` `#ac60ec``;``    ``border-left``: ``29px` `solid` `#f4f4f4``;``    ``border-right``: ``29px` `solid` `#f4f4f4``;``}                              `
```

#####  心形

![CSS心形](http://img.htmleaf.com/1504/heart.jpg)

心形的制作是非常复杂的，可以使用伪元素来制作，分别将伪元素旋转不同的角度，并修改`transform-origin`属性来元素的旋转中心点。

```
`#heart {``    ``position``: ``relative``;``}`` ` `#heart:before,#heart:after {``    ``content``: ``""``;``    ``width``: ``70px``;``    ``height``: ``115px``;``    ``position``: ``absolute``;``    ``background``: ``red``;``    ``left``: ``70px``;``    ``top``: ``0``;``    ``-webkit-``border-radius``: ``50px` `50px` `0` `0``;``    ``-moz-``border-radius``: ``50px` `50px` `0` `0``;``    ``border-radius``: ``50px` `50px` `0` `0``;``    ``-webkit-``transform``: ``rotate``(``-45``deg);``    ``-moz-``transform``: ``rotate``(``-45``deg);``    ``-ms-``transform``: ``rotate``(``-45``deg);``    ``-o-``transform``: ``rotate``(``-45``deg);``    ``transform``: ``rotate``(``-45``deg);``    ``-webkit-``transform-origin``: ``0` `100%``;``    ``-moz-``transform-origin``: ``0` `100%``;``    ``-ms-``transform-origin``: ``0` `100%``;``    ``-o-``transform-origin``: ``0` `100%``;``    ``transform-origin``: ``0` `100%``;``}`` ` `#heart:after {``    ``left``: ``0``;``    ``-webkit-``transform``: ``rotate``(``45``deg);``    ``-moz-``transform``: ``rotate``(``45``deg);``    ``-ms-``transform``: ``rotate``(``45``deg);``    ``-o-``transform``: ``rotate``(``45``deg);``    ``transform``: ``rotate``(``45``deg);``    ``-webkit-``transform-origin``: ``100%` `100%``;``    ``-moz-``transform-origin``: ``100%` `100%``;``    ``-ms-``transform-origin``: ``100%` `100%``;``    ``-o-``transform-origin``: ``100%` `100%``;``    ``transform-origin``: ``100%` `100%``;``}                              `
```

#####  蛋形

 

蛋形时椭圆形的一个变体，它的高度要比宽度稍大，并且设置正确的`border-radius`属性即可以制作出一个蛋形。

```
`#egg {``    ``width``: ``136px``;``    ``height``: ``190px``;``    ``background``: ``#ffc000``;``    ``display``: ``block``;``    ``-webkit-``border-radius``: ``63px` `63px` `63px` `63px` `/ ``108px` `108px` `72px` `72px``;``    ``border-radius``: ``50%` `50%` `50%` `50%` `/ ``60%` `60%` `40%` `40%``;``}                              `
```

#####  无穷符号

![CSS无穷符号](http://img.htmleaf.com/1504/infinity.jpg)

无穷符号可以通过`border`属性和设置伪元素的角度来实现。

```
`#infinity {``    ``width``: ``220px``;``    ``height``: ``100px``;``    ``position``: ``relative``;``}`` ` `#infinity:before,#infinity:after {``    ``content``: ``""``;``    ``width``: ``60px``;``    ``height``: ``60px``;``    ``position``: ``absolute``;``    ``top``: ``0``;``    ``left``: ``0``;``    ``border``: ``20px` `solid` `#06c999``;``    ``-moz-``border-radius``: ``50px` `50px` `0``;``    ``border-radius``: ``50px` `50px` `0` `50px``;``    ``-webkit-``transform``: ``rotate``(``-45``deg);``    ``-moz-``transform``: ``rotate``(``-45``deg);``    ``-ms-``transform``: ``rotate``(``-45``deg);``    ``-o-``transform``: ``rotate``(``-45``deg);``    ``transform``: ``rotate``(``-45``deg);``}`` ` `#infinity:after {``    ``left``: ``auto``;``    ``right``: ``0``;``    ``-moz-``border-radius``: ``50px` `50px` `50px` `0``;``    ``border-radius``: ``50px` `50px` `50px` `0``;``    ``-webkit-``transform``: ``rotate``(``45``deg);``    ``-moz-``transform``: ``rotate``(``45``deg);``    ``-ms-``transform``: ``rotate``(``45``deg);``    ``-o-``transform``: ``rotate``(``45``deg);``    ``transform``: ``rotate``(``45``deg);``}                              `
```

#####  消息提示框

 

消息提示框可以先制作一个圆角矩形，然后在需要的地方放置一个三角形。

```
`#comment_bubble {``    ``width``: ``140px``;``    ``height``: ``100px``;``    ``background``: ``#088cb7``;``    ``position``: ``relative``;``    ``-moz-``border-radius``: ``12px``;``    ``-webkit-``border-radius``: ``12px``;``    ``border-radius``: ``12px``;``}`` ` `#comment_bubble:before {``    ``content``: ``""``;``    ``width``: ``0``;``    ``height``: ``0``;``    ``right``: ``100%``;``    ``top``: ``38px``;``    ``position``: ``absolute``;``    ``border-top``: ``13px` `solid` `transparent``;``    ``border-right``: ``26px` `solid` `#088cb7``;``    ``border-bottom``: ``13px` `solid` `transparent``;``}                              `
```

#####  吃豆人

 

吃豆人的制作方法是先在一个圆形里面制作一个透明的三角形。

```
`#pacman {``    ``width``: ``0``;``    ``height``: ``0``;``    ``border-right``: ``70px` `solid` `transparent``;``    ``border-top``: ``70px` `solid` `#ffde00``;``    ``border-left``: ``70px` `solid` `#ffde00``;``    ``border-bottom``: ``70px` `solid` `#ffde00``;``    ``border-top-left-radius``: ``70px``;``    ``border-top-right-radius: ``70px``;``    ``border-bottom-left-radius: ``70px``;``    ``border-bottom-right-radius``: ``70px``;``}                              `
```