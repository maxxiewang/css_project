# CSS-Project

### CSS盒模型注意点

1. padding不能为负值，而margin可以为负值
2. 背景色会平铺到非margin的区域
3. margin-top传的现象及解决方案
4. margin上下叠加的现象及解决方案

### 块级盒子与内联盒子

- 块级盒子（block-box）和 内联盒子（inline box）
- 块级盒子：div、p、h1 ...  内联盒子：span、a、strong ...

##### 块级盒子特性

1. 独占一行
2. 支持所有样式
3. 不写宽度的时候，跟父容器的宽度相同
4. 所占区域是一个矩形

##### 内联盒子特性

1. 盒子不会产生换行
2. 有些样式不支持，例如：width，height 等
3. 不写宽的时候，宽度由内容决定
4. 据占区域不一定是矩形（内容换行的情况）
5. 内联标签之间是有空隙的（font-size=0可以解决）

<u>内联盒子的问题特别多，布局尽量不要选内联盒子。仅在文本修饰时使用</u>

### 自适应盒模型的特性

自适应盒模型指的是，当盒子不设置宽度时，盒模型相关组成部分的处理方式是如何的：即子元素不写宽度的时候，当加填充时，会自动往里收缩，不必再进行一些计算去处理。

### 标准盒模型与怪异盒模型

- 在标准盒模型中，如果你给盒设置width和height，实际设置的是content-box。padding和border再加上设置的宽高一起决定了整个盒子的大小。
- 在怪异盒模型中，所有宽度都是可见宽度，所以内容宽度是该宽度减去边框和填度部分，即：width = border + padding + content
- content-box：width、height -> content
- border-box ：width、height -> conent + padding + border

### 浮动

- 当元素被浮动时，会脱离文档流，根据float 的值向左或向右移动，直到它的外边界碰到父元素的内边界或另一个浮动元素的外边界为止，是CSS布局中实现左右布局的一种方式。

- 文档流：文档流是元素在web页面上的一种呈现方式，按照出现的先后顺序进行排列。

  ##### 清浮动的方案

  - clear属性 （清除上下的）
  - BFC 
  - 空标签
  - .clearfix:: after {}
  
  ##### 浮动的注意点
  
  - 只会影响后面的元素（并不会影响之前元素的布局）
  - 文本不会被浮动元素覆盖。（因为当时设计浮动这个API，就是为了图文混排用的。）
  - 具备内联盒子特性：宽度由内容决定
  - 具备块级盒子特性：支持所有样式
  - 浮动放不下，会自动换行
  
  ### 定位
  
  CSS position属性用于指定一个元素在文档中的定位方式，其中top， right， bottom 和 left 属性则决定了该元素的最终位置。

```css
position:
	static,
	relative,
	absolute,
	sticky,
	fixed
```

##### 相对定位 relative

1. 相对定位的元素是在文档中的正常位置偏移给定的值
2. 在文档流内，不影响其他元素布局
3. 相对于自身进行偏移

##### 绝对定位 absolute

1. 绝对定位的元素脱离了文档流，绝对定位元素不占据空间
2. 具备内联盒子特性：宽度由内容决定
3. 具备块级盒子特性：支持所有样式
4. ==绝对定位元素相对于最近的非static祖先元素定位，当这样的祖先元素不存在时，则相对于可视区定位。==，定位规则是：以离定位元素最近的非static元素

##### 固定定位 fixed

1. 固定在可视区中 （固钉，滚动条拖拽后还在）
2. 固定定位元素不受祖先元素影响

##### 粘性定位 sticky

1. 相对定位与固定定位的混合，超过阈值后，触发变为固定定位。（例：表格的表头冻结）

##### z-index

改变定位元素的层级关系，如果父容器也有z-index的话，优先级以父容器为主，高于里面的子元素。

### BFC

BFC即Block Formatting Contexts(块级格式化上下文)，它是W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。
  具有BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的一些特性。
  通俗一点来讲，可以把BFC理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

- float的值不是none
- position的值不是static或者relative
- display的值是inline-block、table-cell、flex、table-caption或者inline-flex
- overflow的值不是visible.  overflow:hidden

在现代布局flex和grid中，是默认自带BFC规范的，所以可以解决非BFC盒子的一些问题，这就是为什么flex和grid能成为更好的布局方式原因之一。

### Flex布局

##### 主轴与交叉轴

<img src="C:\Users\Maxxie\AppData\Roaming\Typora\typora-user-images\image-20220830092310626.png" alt="image-20220830092310626" style="zoom:67%;" />

![image-20220830094031187](C:\Users\Maxxie\AppData\Roaming\Typora\typora-user-images\image-20220830094031187.png)

### Flex容器相关设置

```javascript
// 换行与缩写
flex-wrap {
    nowrap; // 默认，不换行
    wrap;
    wrap-reverse;
}
// flex 并不适合多行多列布局，虽然有flex-wrap 等折行处理

// 一种简写方式 ，direction与wrap 合体版
flex-flow: column wrap;

// 主轴对齐方式
jutisfy-conent: {
    flex-start(默认);
    flex-end;
    center; 
    space-around;
    space-between;
    space-evenly;
}

/* 交叉轴的对齐方式 */
// 每一行的对齐方式
align-items 

// 针对整体的对齐方式
align-content // 只有一行不折行的情况下，这个是不生效的。所以一定要加 flex-wrap

/*
子项分组布局：
margin-right:auto，不用嵌套一堆父容器了，auto让右边的外边距自适应。这种分组办法还可以分多个组，比较实用。
*/

```

### flex子项相关设置

**flex-grow 扩展比例**：默认为0，1为占满。多个子项都设置了flex-grow的话，有一个计算的分配比例。









------

**==transform：translate( -50%, -50%) 属性==**

**==display属性详解，inline-block==**