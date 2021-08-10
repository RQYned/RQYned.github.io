# CSS之float布局

------

PC端常见的float布局基本以双飞翼布局和圣杯布局为经典；

即两边宽度写死，中间的宽度自适应。

下面介绍这两种布局的同时也介绍flex布局和通过定位实现的布局的简单展示：

页面结构如下：

```html
<body>
  <div class="container">
    <div class="main" >
    </div>
    <div class="left">
    </div>
    <div class="right"></div>
  </div>
  <script src="index.js">
  </script>
</body>
```

#### 圣杯布局：

```css
   body {
     margin: 0;
     width: 202px;
     min-width: 55px;
   }

   /* 加上padding，撑开位置 */
   .container {
     width: 100%;
     height: 30vh;
     padding-left: 10px;
     padding-right: 20px;
   }

   .container>div {
     height: 100%;
     float: left;
   }

   .main {
     width: 100%;
     background-color: darkgreen;
   }
/* 设置margin-left：-100%的原因是：
                                margin的百分比是相对于父元素的，所以需要整行的宽度才能补偿这个margin值，所以left就能到main的位置
                                然后通过相对定位right自身的宽度就移到了左侧 */
   .left {
      position: relative;
      margin-left: -100%;
      right: 10px;
      width: 10px;
     background-color: darkorange;
    
   }
/* 这里的margin-right：-20px，是可以使main重叠right的宽度，
因为设置了float所以right就会到main的右边， */
   .right {
      margin-right: -20px;
     width: 20px;
     background-color: darkturquoise;
   }
```

------

效果图如下：

![image-20210810214834044](https://raw.githubusercontent.com/RQYned/blogImages/master/img/20210810214834.png)

#### 双飞翼布局

双飞翼因为要在main上设置margin，而我们之前已经设置了width：100%，所以我们在main里做一个新的div，将显示的内容放进去，给wrap设置margin就可以了

```html
<body>
  <div class="container">
    <div class="main" >
      <div class="wrap"></div>
    </div>
    <div class="left"></div>
    <div class="right"></div>
  </div>
  <script src="index.js">
  </script>
</body>
```

```css
   body {
     margin: 0;
     width: 202px;
     min-width: 55px;
   }

   .container {
     width: 100%;
     height: 30vh;
     padding-left: 10px;
     padding-right: 20px;
   }

   .container>div {
     height: 100%;
     float: left;
   }

   .wrap {
     height: 100%;
     margin: 0 20px 0 10px;
     background-color: yellow;
   }

   .main {
     width: 100%;
   }

   .left {
     margin-left: -100%;
     width: 10px;
     background-color: darkorange;

   }

   .right {
     margin-left: -20px;
     width: 20px;
     background-color: darkturquoise;
   }
```

效果如下：

![image-20210810220847431](https://raw.githubusercontent.com/RQYned/blogImages/master/img/20210810220847.png)

**这里记录一下margin负值的概念**

| Margin-left,margin-top | 元素向左、向上移动                                           |
| ---------------------- | ------------------------------------------------------------ |
| **Margin-right**       | **右侧元素左移（“后续元素”会被拉向指定方向），元素自身不变** |
| **Margin-bottom**      | **右侧元素上移（“后续元素”会被拉向指定方向），元素自身不变** |

#### flex布局实现自适应

页面结构：

```html
<body>
  <div class="box">
    <div class="left" ></div>
    <div class="center"></div>
    <div class="right"></div>
  </div>
  <script src="index.js">
  </script>
</body>
```

```css
   body {
     margin: 0;
     width: 202px;
     min-width: 55px;
   }

  .box{
    display: flex;
    /* 左中右排列顺序 */
    justify-content: space-between;
    height: 100px;
  }
  .center{
    /* 自动填充剩下的区域 */
    flex: 1;
    height: 10px;
    background-color: yellow;
  }
  .left,
  .right{
    /* flex属性 ：flex-grow（元素放大比例，默认为0，即有剩余空间也不放大，设置为1，则元素等分剩余空间）
                 flex-shrink（元素缩小比例，默认为1，即空间不足时缩小该元素，设置为0，即不缩小），
                 flex-basis（定义了元素占据的主轴空间，浏览器会根据这个属性计算主轴是否有多余空间，
    	                      默认值为auto。
                            即元素本身的大小，不过也可以设置像素值（px）规定大小）
                 flex为以上三属性的简写，默认值为0 1 auto三种 */
    flex:0 0 20px;
    height: 10px;
    background-color: turquoise;
  }
```

效果如下：

![image-20210810222306265](https://raw.githubusercontent.com/RQYned/blogImages/master/img/20210810222306.png)

#### 通过定位实现

页面布局同上；

```css
   body {
     margin: 0;
     width: 202px;
     min-width: 55px;
   }

   .box {
     height: 100px;
   }

   .center {
     margin: 0 20px;
     height: 10px;
     background-color: yellow;
   }

   .left,
   .right {
     position: absolute;
     top: 0;
     width: 20px;
     height: 10px;
     background-color: turquoise;
   }

   .left {
     left: 0;
   }

   .right {
     right: 0;
   }
```

效果如下：

![image-20210810223743545](https://raw.githubusercontent.com/RQYned/blogImages/master/img/20210810223743.png)

## 参考文章：

> 掘金文章：https://juejin.cn/post/6983934602196811789#heading-25

> 阮一峰flex布局教程：http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html

