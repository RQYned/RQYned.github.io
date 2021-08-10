# CSS基础之定位问题

------

## 1.position的属性有哪些，区别是什么？

属性值：

|  属性值  | 概述                                                         |
| :------: | ------------------------------------------------------------ |
| absolute | 绝对定位，相对于static定位以外的一个父元素进行定位，元素的位置通过left、right、top、bottom属性进行规定。 |
| relative | 相对定位。相对于元素原来位置进行定位，元素的位置通过left、right、top、bottom属性进行规定。 |
|  fixed   | 生成绝对定位的元素，指定元素相对于屏幕视口(viewport)的位置进行元素位置，元素的位置不会随屏幕的滚动进行变动，常用作顶部导航栏的元素定位方式。 |
|  static  | 默认值，没有定位，元素会出现在正常的文档流中，会忽略top、bottom、left、right或者z-index声明，块级元素从上向下排列，行级元素从左向右排列。 |
| inherit  | 规定从父元素继承position属性元素的值。                       |

### absolute:元素定位只相对于元素自身位置，和其他元素无关，也不会影响其他元素。

起始位置：当设置了top、left，浏览器会遍历该元素的所有父元素，如果找到了其中一个父元素设置了position属性，就以该父元素为基准；如果父元素未指定时，会以浏览器边界定位。

代码：

```html
 <div class="parent">
    <div class="child1">
    </div>
  </div>
```

```css
 body{
        margin: 0;
        width: 700px;
        min-width: 500px;
      }
      .parent{
        width: 100px;
        height: 30px;
        background-color: aqua;
        position: absolute;
      }
      .child1{
        position: absolute;
        width: 10px;
        height: 4px;
        margin-top: 1px;
        margin-left: 3px;
        background-color: black;
      }
```

起始位置：

![](https://raw.githubusercontent.com/RQYned/blogImages/master/img/20210810204235.png)

设置absolute：

![image-20210810204338927](https://raw.githubusercontent.com/RQYned/blogImages/master/img/20210810204338.png)

### relative：元素的定位永远是相对于自身位置的，和其他元素无关，也不会影响其他元素

代码：

```html
<div class="parent">
    <div class="child1">
    </div>
    <div class="child2"></div>
  </div>
```



```css
  .parent {
     width: 100px;
     height: 30px;
     background-color: aqua;
     position: absolute;
   }

   .child1 {
     width: 10px;
     height: 4px;
     background-color: black;
   }
    .child2 {
      position: relative;
      width: 10px;
      height: 4px;
      margin-top: 1px;
      margin-left: 3px;
      background-color: darkgreen;
    }
```

黑色div为起始位置，绿色为自身移动的相对定位

![image-20210810204719806](https://raw.githubusercontent.com/RQYned/blogImages/master/img/20210810204719.png)

