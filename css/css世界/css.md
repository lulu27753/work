* 在css世界中，HTML是魔法石，选择器就是选择法器，CSS属性就是魔法师，CSS各种属性值就是魔法师的魔法技能，浏览器就是他们所在的“王国”，“王国”会不断更新法律法规(版本升级)，决定是否允许使用新的魔法石(HTML5新标签新属性)，是否允许新的魔法师入“国籍”（CSS3新属性)，或者允许魔法师使用某些新技能(CSS新的属性值)，以及是否舍弃某些魔法技能(display：run-in)；操作系统就是他们所在的世界，不同的操作系统代表不同的平行世界。所以，CSS世界有这么几个比较大的平行世界，即window世界，OSX世界以及移动端的ios世界和Andriod世界。不同世界的浏览器王国的命运不一样。例如，在OSX世界中，IE王国是不存在的，而safri王国却异常强大，但在windows世界中，Safari王国却异常落寞。

* @规则
    * @media
    * @font-face
    * @page
    * @support

* `<a>、<button>`这样的元素，当我们使用键盘进行tab健切换的时候，是可以focus的，表现为虚框或者外发光，这类元素称为“焦点元素”，非焦点元素指没有设置tabindex属性的`<div><span>`等普通元素。在IE6|IE7浏览器下，非焦点元素对:active置若罔闻
* 规范的“未定义行为”导致了浏览器对属性的表现实现不一致，从而导致了浏览器的兼容性问题
* Firefox认为:active发生在mousedown事件之后
* “块级元素”和“display; block“不是一个概念，`<li>`默认display：list-item;`<tabel>`默认display：table;但它们均是块级元素，因为它们都符合块级元素的基本特征，也就是一个水平流上只能单独显示一个元素，多个块级元素则换行显示。正是由于“块级元素”具有换行特性，因此理论上它可以配合clear属性来清除浮动

```css
.clear:after {
    content: '';
    display: table; // block | list-item
    clear: both;
}
```

* width:auto
    * 充分利用可用空间(外部尺寸)：块级元素的width默认是父级容器的100%
    * 收缩与包裹：fit-content，收缩到合适，典型浮动、绝对定位、inline-block、table
    * 收缩到最小（min-content)：table-layout，每列空间都不够时，文字能断就断，但是中文是随便断的，英文单词不能断
    * 超出容器限制(max-content)：一般尺寸不会主动超过父级容器宽度，除非有明确的width 或者 white-space：nowrap
* 1、外部尺寸和流体特性
    * 正常流宽度：
        * 块级元素不设置宽度，其尺寸表现为铺满容器
            * 流动性：并不是看上去的宽度100%显示这么简单，而是一种margin|border|padding和content内容区域自动分配水平空间的机制，表现为“外部尺寸”的块级元素一旦设置了宽度，流动性就丢失了。
     * 格式化宽度：
        * “绝对定位模型”：表现为“包裹性”，宽度由内部尺寸决定
        * 例外：宽度由外部尺寸决定：对于非替换元素，当left|top或top|bottom对立方位的属性值同时存在的时候，元素的宽度大小相对于最近的具有定位特性(position属性值不是static)的祖先元素计算
* 2、内部尺寸和流体特性
    * 包裹性（自适应性）：
        * 元素尺寸由内部元素决定，但永远小于“包含块”容器的尺寸（除非容器尺寸小于元素的“首选最小宽度”）
        * inline-block | 浮动元素 | 绝对定位元素
    * 首选最小宽度：
        * 东亚文字（如中文）最小宽度为每个汉字的宽度
        * 西方文字最小宽度由特定的连续的英文字符单元决定。并不是所有的英文字符都会组成连续单元，一般会终止于空格（普通空格）、短横线、问号以及其他非英文字符等。
* 三无准则：无宽度、无图片、无浮动
* 按钮：
    * inline-block
    * 按钮文字越多宽度越宽(内部尺寸特性)，但如果文字足够多，则会在容器的宽度处自动换行（自适应特性）
* 让英文字符和中文一样，每个字符都用最小宽度单元：word-break:break-all
* 






























