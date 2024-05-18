## 盒子模型

在一个文档中，每个元素都被表示为一个矩形的盒子。
确定这些盒子的尺寸, 属性（像它的颜色，背景，边框方面）和位置是渲染引擎的目标。

在 CSS 中，使用标准盒模型描述这些矩形盒子中的每一个。
这个模型描述了元素所占空间的内容。
每个盒子有四个边：

- 外边距边（margin）,
- 边框边（border）,
- 内填充边（padding）
- 与内容边（content）。

### margin 的叠加

只有普通文档流中块框的垂直外边距才会发生外边距叠加。
行内框、 浮动框或绝对定位框之间的外边距不会叠加
外边距（margin）的高度等于两个发生叠加的外边距的高度中的较大者。

#### 例 1

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <div class="a">a</div>
    <div class="b">b</div>
  </head>
  <body>
    <style>
      .a {
        width: 100px;
        height: 100px;
        background-color: red;
        margin-bottom: 10px;
      }
      .b {
        width: 100px;
        height: 100px;
        background-color: blue;
        margin-top: 20px;
      }
    </style>
  </body>
</html>
```

![image-20240518112342934](https://gitee.com/hanosong/picgo_drawingbed/raw/master/image-20240518112342934.png)

### 盒模型计算

盒模型的值

1. content-box（默认）
2. padding-box （并不是标准 CSS 规范中的值，所以在实际应用中不会生效。）
3. border-box （项目中一般设置的）

#### 例 2

```html
<head>
    <div class="content-box">
        contentBox
    </div>
    <div class="padding-box">
        paddingBox
    </div>
    <div class="border-box">
        borderBox
    </div class="padding-box">
</head>

<body>
    <style>
        .content-box {
            width: 100px;
            height: 100px;
            background-color: red;
            box-sizing: content-box;
            border: 1px solid black;
            padding: 1px;
        }

        .border-box {
            width: 100px;
            height: 100px;
            background-color: blue;
            box-sizing: border-box;
            border: 2px solid pink;
            padding: 2px;
        }

        .padding-box {
            width: 100px;
            height: 100px;
            background-color: green;
            box-sizing: padding-box;
            border: 3px solid yellow;
            padding: 3px;
        }
    </style>

</body>

</html>
```

![image-20240518120151437](https://gitee.com/hanosong/picgo_drawingbed/raw/master/image-20240518120151437.png)

### 使得元素居中

1. 使用 inline-block

```md
在块状元素 parent 内添加了另外一个块状元素 child
将 child 设置 display: inline-block，同时配合 parent 设置 text-align: center，就可以设置 child 在 parent 内横向居中
将 parent 的 height 和 line-height 设置相等，就可以轻松实现 child 在 parent 内纵向居中啦
```

## position 和 z-index

[CSS 的 position 和 z-index 有关](https://godbasin.github.io/2016/06/25/about-position/)

### 文档流

1. 普通流（正常文档流）：在 HTML 里面的写法就是从上到下，从左到右的排版布局　=> (position: static)
   - 直接添加 left，top 等定位是无效的
2. position: relative: 保持原有文档流，但**相对本身的原始位置**发生位移，且占空间
   - 会溢出父元素，撑开整个页面:此时给父元素设置 overflow: hidden;则可以隐藏溢出部分 (超出并不会有滚动条)

![image-20240518144849277](https://gitee.com/hanosong/picgo_drawingbed/raw/master/image-20240518144849277.png)
3. position: absolute : 用于脱离文档流（不占位）
    * 定位是相对于static定位以外的第一个父元素进行定位
    * 当absolute的父元素position为static，则会继续往上查找，直到找到一个为relative/absolute/fixed的父元素作为定位参照物
    * 都是static定位，则相对于文档document进行定位
    * 未设置定位的absolute元素，其定位与其原本位置（position=static）相同

### z-index
* z-index只能在position属性值为relative/absolute/fixed的元素上有效
* 当向上追溯找不到含有z-index值的父元素的情况下，则可以视为自由的z-index元素
* 自由的z-index元素可以与其他自由的定位元素或者父元素的同级兄弟定位元素来比较z-index的值
* z-index值只决定同一父元素中的同级子元素的堆叠顺序
* 不同父元素中的子元素由元素在文档中的先后位置决定，后出现的会在上面。

![image-20240518152304708](https://gitee.com/hanosong/picgo_drawingbed/raw/master/image-20240518152304708.png)

