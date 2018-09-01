# FlexBox 布局

## flex布局是什么？

> **[info]** 提示
>
> Flex 是 FlexBox 的缩写，意为“_弹性布局_”。用来为`盒装模型`提供最大的灵活性。

- 示例

```css
.flex-container {
  display: flex;
  /* webkit内核 */
  display: -webkit-flex;
  /* 行内元素flex布局 */
  /* display:inline-flex; */
}
```

## 基本概念

> **[info]** 提示
>
> 项目默认沿主轴排列

{% includeCsv %}
名词,说明
main axis,水平的主轴
cross axis,垂直的主轴
main start,主轴的开始位置（与边框的交叉点）
main end,主轴的结束位置
cross start,交叉轴的开始位置
cross end,交叉轴的结束位置
main size,单个项目占据主轴的空间
cross size,单个项目占据交叉轴的空间
{% endincludeCsv %}

## 容器的属性

{% includeCsv %}
属性,说明
flex-direction,决定主轴的方向
flex-wrap,决定一行轴线排不下时，如何换行
flex-flow,是flex-direction属性和flex-wrap属性的简写形式，默认为 row nowrap
justify-content,定义了在主轴上的对齐方式
align-items,定义了项目在交叉轴上如何对齐
align-content,定义了多根轴线的对齐方式，如果只有一根轴线，该属性不起作用。
{% endincludeCsv %}

### flex-direction

> **[info]** 提示
>
> *flex-direction*属性决定主轴的方向。(即项目的排列方向)

```css
.flex-container{
  flex-direction:row | row-reverse | column | column-reverse;
  /* webkit内核 */
  -webkit-flex-direction:row | row-reverse | column | column-reverse
}
```

{% includeCsv %}
属性值,说明
row,(默认值)主轴为水平方向，起点在左端
row-reverse,主轴为水平方向，起点在右端
column,主轴为垂直方向，起点在上沿
column-reverse,主轴为垂直方向，起点在下沿
{% endincludeCsv %}

### flex-wrap

> **[info]** 提示
>
> flexbox中的默认都排在一条线（轴线）上。*flex-wrap*属性定义了，如果一条轴线排不下，如何换行。

``` css
.flex-container{
  flex-wrap:nowrap | wrap | wrap-reverse;
}
```

{% includeCsv %}
属性值,说明
nowrap,(默认)不换行
wrap,换行，第一行在上方
wrap-reverse,换行，第一行在下方
{% endincludeCsv %}

### flex-flow

> **[info]** 提示
>
> *flex-flow*属性是*flex-direction*属性和*flex-wrap*属性的简写形式，默认为 row nowrap

``` css
.flex-container{
  flex-flow:<flex-direction> || flex-wrap;
}
```

### justify-content

> **[info]** 提示
>
> *justify-content*属性定义了在主轴上的而对齐方式。

``` css
.flex-conatainer{
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

{% includeCsv %}
属性值,说明
flex-start,(默认值)，左对齐
flex-end,左对齐
center,居中
space-between,两端对齐，之间的间隔都相等
space-around,每个项目两端的间隔相等。所以项目之间的间隔比项目与边框的间隔大一倍。
{% endincludeCsv %}

### align-items

> **[info]** 提示
>
> 定义了项目在交叉轴上如何对齐。

``` css
.flex-container{
  align-items:flex-start | flex-end | center | baseline | stretch;
}
```

{% includeCsv %}
属性值,说明
flex-start,交叉轴的起点对齐
flex-end,交叉轴的终点对齐
center,交叉轴的中点对齐
baseline,项目第一行文字的基线对齐
stretch,（默认值）：如果项目未设置高度或者设为auto，将占满整个屏幕的高度。
{% endincludeCsv %}

### align-content

> **[info]** 提示
>
> *align-content*属性定义了多根轴线的对齐方式，如果只有一根轴线，该属性不起作用。

``` css
.flex-container{
  align-content:flex-start | flex-end | center | space-between | space-around | stretch;
}
```

{% includeCsv %}
属性值,说明
flex-start,与交叉轴的起点对齐
flex-end,与交叉轴的终点对齐
center,与交叉轴的中点对齐
space-between,与交叉轴的两端对齐，轴线之间的间隔平均分布
space-around,每根轴线两端的举例都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch,(默认值)：轴线占满整个交叉轴。
{% endincludeCsv %}

## 项目的属性

{% includeCsv %}
属性名,说明
order,定义了项目的排列顺序。
flex-grow,定义了项目的放大比例。
flex-shrink,定义了项目的缩小比例。
flex-basis,
flex,
align-self,
{% endincludeCsv %}

### order

> **[info]** 提示
>
>定义了项目的排列顺序，值为数值。（从小到大排序）

``` css
.flex-item{
  order: <integer>；/* default 0 */
}
```

### flex-grow

> **[info]** 提示
>
> 定义了项目的放大比例。默认为0，即如果存在剩余空间，也不放大。
>
> 如果所有项目的*flex-grow*都是1，则他们将等分剩余空间；如果一个项目的*flex-grow*属性值为2，剩余的项目都是1，则前者占据剩余空间的将比其他项目多一倍。

``` css
flex-item{
  flex-grow: <integer>; /* default 0 */
}
```

### flex-shrink

> **[info]** 提示
>
> 定义了项目的缩小比例。默认为1，即如果空间不足，该项目将缩小。
>
> 如果所有项目的 *flex-shrink* 属性值为1，当空间不足时，都将等比例缩放。
>
> 如果一个项目的*flex-shrink*属性值为0，其他的项目都为1，则空间不足时，前者不缩放。
>
> 负值对该属性无效。

``` css
flex-item{
  flex-shrink: <integer>; /* default 1 */
}
```
