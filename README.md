# CSS3绘制腾讯QQ企鹅

## 绘制我们的企鹅

> 前提，你已经看过[CSS3绘制图形基本原理](https://www.jianshu.com/p/56256db2df2f)一文，已对一些基本图形绘制了解。

开始着手于QQ 企鹅的绘制, 第一步基本框架的绘制。

![result.png](https://upload-images.jianshu.io/upload_images/735083-59d755e606945df4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过对Logo图像的观察，按照层次划分来组合最终的效果。选择使用绝对位置position:absolute;来布局各个元素。主要划分为头部，身体，围脖，双手，双脚。

```html
    <!-- QQ Logo box -->
    <div id="qq">
        <!-- 头 -->
        <div class="head"></div>
        <!-- 身体 -->
        <div class="body"></div>
        <!-- 手 -->
        <div class="handWrapper"></div>
        <!-- 脚 -->
        <div class="footWrapper"></div>
    </div>
```
基本框架结构就是这样的，QQ 对于容器是通过绝对定位来对每个元素布局进行设置的。

QQ Logo容器（画板）：
```css
/**
 * QQ Logo 绘制
 */
#qq {
    position: relative;
    margin: 0 auto;
    width: 420px;
    height: 400px;
    outline: gold solid 2px;
}
```

骨架出来了，那我们就开始一步步的进行绘制了，先从头开始：

绘制 head 前，还是跟步骤1一样，先对 head 的层次结构划分清楚，依次为：左眼、右眼、上嘴唇、下嘴唇、嘴唇的层次感体现

```html
 <!-- 头 -->
<div class="head">
     <!-- 左眼 -->
     <div class="left eye"></div>
     <!-- 右眼 -->
     <div class="right eye"></div>
     <!-- 上嘴唇 -->
     <div class="mouthTopContainer"></div>
     <!-- 下嘴唇 -->
     <div class="mouthBottomContainer"></div>
     <!-- 嘴唇上下层次感 -->
     <div class="lispContainer"></div>
 </div>
```

绘制 head 的轮廓：

```css
 /* QQ head */
.head {
    position: absolute;
    top: 18px;
    left: 96px;
    width: 234px;
    height: 185px;
    border: 1px solid #000;
    /* 通过对border-radius 圆弧的层度来进行钩画 */
    border-top-left-radius: 117px 117px;
    border-top-right-radius: 117px 117px;
    border-bottom-left-radius: 117px 68px;
    border-bottom-right-radius: 117px 68px;
}
```
![image.png](https://upload-images.jianshu.io/upload_images/735083-0f9d886a55cc075c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

图中为什么圆弧是设置成 ` border-bottom-left-radius: 117px 68px;` 一般根据设计图出来后导出转成带有标尺图后，会自动计算出值；如果没有的话，那就要通过计算了。

然后依次绘制 head 其他结构：

**眼睛**

```css

/* 眼睛 */
.eye {
    position: absolute;
    width: 44px;
    height: 66px;
    border:1px solid #000;
    border-radius: 50% 50%;
}

.left.eye {
    left: 62px;
    top: 50px;
}

.right.eye {
    left: 132px;
    top: 50px;
}
```
![image.png](https://upload-images.jianshu.io/upload_images/735083-26a037d3989c49d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**嘴**

```css
/* QQ head -> mouth */
.mouthTopContainer {
    position: absolute;
    top: 120px;
	left: 39px;
    width: 158px;
    height: 29px;
    border: 1px solid #000;
}

.mouthBottomContainer {
    position: absolute;
    top: 146px;
	left: 39px;
    width: 158px;
    height: 15px;
    border: 1px solid #000;
}
```
![image.png](https://upload-images.jianshu.io/upload_images/735083-e934db4d135d3aa1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到这里基本头的骨架就出来，然后就是对头的骨架结构的线条进行修饰，现在太丑了，对吧！

**眼睛**

```html
<!-- 左眼 -->
<div class="left eye">
        <!-- 眼球 -->
        <div class="innerLeftEye"></div>
    </div>
    <!-- 右眼 -->
    <div class="right eye">
        <!-- 眼球 -->
        <div class="innerRightEye">
              <!-- 月牙眼球两端圆弧修饰 -->
              <div class="fix"></div>
         </div>
</div>
```

```css
/* QQ head -> eye */
.eye {
    position: absolute;
    width: 44px;
    height: 66px;
    border:1px solid #000;
    border-radius: 50% 50%;
}

.left.eye {
    left: 62px;
    top: 50px;
}

.right.eye {
    left: 132px;
    top: 50px;
}

.innerLeftEye {
    position: absolute;
    top: 20px;
    left: 20px;
    width: 18px;
    height: 24px;
    border-radius: 50%;
    border: 1px solid #000;
}

.innerLeftEye::after {
    content: "";
    position: absolute;
    top: 6px;
    left: 9px;
    width: 6px;
    height: 8px;
    border: 1px solid #000;
    border-radius: 50%;
}

.innerRightEye {
    position: absolute;
    top: 20px;
    left: 8px;
    /* 月牙眼球外轮廓 */
    width: 18px;
    height: 24px;
    border: 1px solid #000;
    border-top-left-radius: 50% 90%;
    border-top-right-radius: 50% 90%;
    border-bottom-left-radius: 50% 10%;
    border-bottom-right-radius: 50% 10%;
}

.innerRightEye::after {
    content: "";
    position: absolute;
    bottom: -1px;
	left: 4px;
    /* 月牙眼球内部轮廓 */
    width: 10px;
    height: 13px;
    border: 1px solid #000;
    border-top-left-radius: 50% 100%;
	border-top-right-radius: 35% 80%;
}

.fix {
    position: absolute;
    top: 17px;
    width: 4px;
    height: 4px;
    border: 1px solid #000;
    border-radius: 50%;
}

.fix:after{
	content: "";
    position: absolute;
    top: 0;
	left: 14px;
	width: 4px;
    height: 4px;
    border: 1px solid #000;
	border-radius: 50%;
}

```

![image.png](https://upload-images.jianshu.io/upload_images/735083-3baf6a2c78f40932.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**嘴**

```html
<!-- 上嘴唇 -->
<div class="mouthTopContainer">
    <div class="mouthTop"></div>
</div>
<!-- 下嘴唇-->
<div class="mouthBottomContainer">
    <div class="mouthBottom"></div>
</div>
<!-- 嘴唇上下层次感-咬合部位  -->
<div class="lispContainer">
    <div class="lips">
            <div class="lipShadow left">
            </div>
            <div class="lipShadow right">
            </div>
    </div>
</div>
```

```css
/* QQ head -> mouth */
.mouthTopContainer {
    /* 定位 */
    position: absolute;
    top: 120px;
	left: 39px;
    width: 158px;
    height: 29px;
    overflow: hidden; /* 隐藏超出部分 */
}

.mouthTop {
    /* 上嘴唇轮廓 */
    position: absolute;
    top: 0;
	left: 0;
    width: 158px;
    height: 34px;
    border: 1px solid #000;
    border-top-left-radius: 45% 34px;
	border-top-right-radius: 45% 34px;
}

.mouthBottomContainer {
    position: absolute;
    top: 146px;
	left: 39px;
    width: 158px;
    height: 15px;
    overflow: hidden;   /* 隐藏超出部分 */
}

.mouthBottom {
    position: absolute;
    top: -4px;
	left: 0;
    width: 158px;
    height: 24px;
    border: 1px solid #000;
    border-top:none;
    border-bottom-left-radius: 45% 24px;
	border-bottom-right-radius: 45% 24px;
}

/* 嘴唇上下层次感-咬合部位 */
.lispContainer {
    /* 定位 */
    position: absolute;
	top: 146px;
	left: 60px;
    width: 116px;
    height: 24px;
}

.lips {
    position: absolute;
	top: 0;
	left: 0;
    width: 116px;
    height: 24px;
    border: 1px solid #FFA600;
    border-bottom-left-radius: 50% 100%;
	border-bottom-right-radius: 50% 100%;
}
```

![image.png](https://upload-images.jianshu.io/upload_images/735083-d3cb3a972a0784c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/735083-3af2faf83990531a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/735083-bc8e527ad3a9efd7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

基本 head 轮廓就是这样了，最后在把右眼眼球部分上个色，来进行层叠覆盖隐藏

```css
.innerRightEye {
    position: absolute;
    top: 20px;
    left: 8px;
    /* 月牙眼球外轮廓 */
    width: 18px;
    height: 24px;
    /* border: 1px solid #000; */
    border-top-left-radius: 50% 90%;
    border-top-right-radius: 50% 90%;
    border-bottom-left-radius: 50% 10%;
    border-bottom-right-radius: 50% 10%;
    background: black;
	box-shadow: 0 -1px 2px black;
}

.innerRightEye::after {
    content: "";
    position: absolute;
    bottom: -1px;
	left: 4px;
    /* 月牙眼球内部轮廓 */
    width: 10px;
    height: 13px;
    /* border: 1px solid #000; */
    border-top-left-radius: 50% 100%;
    border-top-right-radius: 35% 80%;
    background: white;
}

.fix {
    position: absolute;
    top: 19px;
    width: 4px;
    height: 4px;
    /* border: 1px solid #000; */
    border-radius: 50%;
    background: black;
}

.fix:after{
	content: "";
    position: absolute;
    top: 0;
	left: 14px;
	width: 4px;
    height: 4px;
    /* border: 1px solid #000; */
    border-radius: 50%;
    background: black;
}
```

![image.png](https://upload-images.jianshu.io/upload_images/735083-48fd5a4d0428425c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


接下来 开始绘制 QQ 的 body 部分，老样子对 body 进行层次结构划分：围巾、围巾尾、内轮廓、外轮廓

```html
<!-- 身体 -->
<div class="body">
    <!-- 内轮廓 -->
    <div class="innerWrapper">
         <div class="inner"></div>
    </div>
    <!-- 外轮廓 -->
    <div class="outerWrapper">
          <div class="outer"></div>
    </div>
    <!-- 围巾 -->
    <div class="scarf"></div>
    <!-- 围巾尾 -->
    <div class="scarfEnd"></div>
</div>
```

先各个容器位置布局好

```css
/* QQ body */
.body {
    /* body 容器定位 */
    position: absolute;
    top: 135px;
    left: 48px;
    width: 326px;
    height: 300px;
    /* border: 1px solid #000; */
}

/* QQ body -> scarf */
.scarf {
    position: absolute;
    top: -2px;
    left: 34px;
    width: 258px;
    height: 110px;
    border: 1px solid #000;
    border-top: none;
}

/* QQ body -> scarfEnd */
.scarfEnd {
    position: absolute;
    left: 74px;
    top: 90px;
	width: 52px;
    height: 64px;
    border: 3px solid black;
}

/* QQ body -> innerWrapper */
.innerWrapper {
    /* innerWrapper 容器定位 */
    position: absolute;
    left: 30px;
	top: 76px;
    width: 280px;
    height: 200px;
    border: 1px solid #000;
}

/* QQ body -> outerWrapper */
.outerWrapper{
    /* outerWrapper 容器定位 */
    position: absolute;
	top: 54px;
	overflow: hidden;
    width: 262px;
	left: 32px;
    height: 250px;
    border: 1px solid #000;
}

```
![](https://upload-images.jianshu.io/upload_images/735083-5a2f42ca2f280160.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

轮廓线条修正

```css
/* QQ body */
.body {
    /* body 容器定位 */
    position: absolute;
    top: 135px;
    left: 48px;
    width: 326px;
    height: 300px;
    /* border: 1px solid #000; */
}

/* QQ body -> scarf */
.scarf {
    position: absolute;
    top: -2px;
    left: 34px;
    width: 258px;
    height: 110px;
    border: 1px solid #000;
    border-top-left-radius: 30px 34px;
	border-top-right-radius: 38px 34px;
	border-bottom-left-radius: 50% 76px;
    border-bottom-right-radius: 50% 76px;
    border-top: none;
}

/* QQ body -> scarfEnd */
.scarfEnd {
    position: absolute;
    left: 74px;
    top: 90px;
	width: 52px;
    height: 64px;
    border: 3px solid black;
    border-bottom-left-radius: 50% 43%;
	border-bottom-right-radius: 15px;
	border-top-left-radius: 20% 57%;
}

/* QQ body -> innerWrapper */
.innerWrapper {
    /* innerWrapper 容器定位 */
    position: absolute;
    left: 30px;
	top: 76px;
    width: 280px;
    height: 200px;
    overflow: hidden;
}

.inner {
    position: absolute;
    left: 25px;
	top: -71px;
	width: 218px;
	height: 210px;
    border: 1px solid #000;
    border-radius: 50%;
}

/* QQ body -> outerWrapper */
.outerWrapper{
    /* outerWrapper 容器定位 */
    position: absolute;
	top: 54px;
	overflow: hidden;
    width: 262px;
	left: 32px;
    height: 250px;
}

.outer{
    position: absolute;
	top: -84px;
	width: 260px;
    height: 250px;
    border: 1px solid #000;
	border-radius: 125px;
}

```
![](https://upload-images.jianshu.io/upload_images/735083-8b13bbc5a39072f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

大致轮廓基本已经出来了，还有一些内部线条，等后面在来慢慢绘制。

接下来我们来绘制 hand 部分，安装老路子层次结构划分：左手、右手； 手的样子需要通过两个 div 进行整合才能绘制出来，所以再次划分： 左手上、左手下、右手上、右手下

```html
<!-- 手 -->
<div class="handWrapper">
    <div class="leftHandTopContainer">
        <div class="leftHandTop"></div>
    </div>
    <div class="leftHandBottomContainer">
        <div class="leftHandBottom"></div>
    </div>
    <div class="rightHandTopContainer">
        <div class="rightHandTop"></div>
    </div>
    <div class="rightHandBottomContainer">
        <div class="rightHandBottom"></div>
    </div>
</div>
```

```css
/* QQ handWrapper */
.handWrapper{
    /* 定位手的起始点 */
	position: absolute;
	top: 219px;
	left: 7px;
}

/* QQ handWrapper -left */
.leftHandTopContainer {
    /* 定位 */
	position: absolute;
	top: 55px;
	left: 50px;
    width: 118px;
    height: 26px;
    border: 1px solid #000;
	transform-origin: bottom left;
	transform: rotate(-70deg);
}

.leftHandBottomContainer {
    /* 定位 */
    position: absolute;
	top: 78px;
	left: 50px;
	width: 100px;
    height: 30px;
    border: 1px solid #000;
	transform-origin: top left;
	transform: rotate(-70deg);
}

/* QQ handWrapper -right */
.rightHandTopContainer {
    /* 定位 */
    position: absolute;
	top: 47px;
	left: 240px;
    width: 118px;
    height: 34px;
    border: 1px solid #000;
	transform-origin: bottom right;
    transform: rotate(65deg);
}

.rightHandBottomContainer{
    /* 定位 */
    position: absolute;
	top: 81px;
    left: 248px;
	width: 110px;
	height: 58px;
    border: 1px solid #000;
	transform-origin: top right;
	transform: rotate(90deg);
}

```

![image.png](https://upload-images.jianshu.io/upload_images/735083-0881a38bf2460989.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

线条轮廓修改

```css
/* QQ handWrapper */
.handWrapper{
    /* 定位手的起始点 */
	position: absolute;
	top: 219px;
	left: 7px;
}

/* QQ handWrapper -left */
.leftHandTopContainer {
    /* 定位 */
	position: absolute;
	top: 55px;
	left: 50px;
    width: 118px;
    height: 26px;
    /* border: 1px solid #000; */
	transform-origin: bottom left;
    transform: rotate(-70deg);
    overflow: hidden;
}

.leftHandTop {
     /* 上半部分 */
	width: 128px;
	height: 54px;
    border: 1px solid #050346;
    border-top-left-radius: 44% 38px;
    border-top-right-radius: 56% 33px;
}

.leftHandBottomContainer {
    /* 定位 */
    position: absolute;
	top: 78px;
	left: 50px;
	width: 100px;
    height: 30px;
    /* border: 1px solid #000; */
	transform-origin: top left;
    transform: rotate(-70deg);
    overflow: hidden;
}

.leftHandBottom {
    position: absolute;
    top: -26px;
    width: 128px;
	height: 44px;
    border: 1px solid #050346;
    border-bottom-left-radius: 48% 20px;
	border-bottom-right-radius: 52% 23px;
}

/* QQ handWrapper -right */
.rightHandTopContainer {
    /* 定位 */
    position: absolute;
	top: 47px;
	left: 240px;
    width: 118px;
    height: 34px;
    /* border: 1px solid #000; */
	transform-origin: bottom right;
    transform: rotate(65deg);
    overflow: hidden;
}

.rightHandTop {
    position: absolute;
    left: -30px;
    width: 148px;
	height: 54px;
    border: 1px solid #050346;
    border-top-right-radius: 41% 54px;
    border-top-left-radius: 59% 48px;
}

.rightHandBottomContainer{
    /* 定位 */
    position: absolute;
	top: 81px;
    left: 248px;
	width: 110px;
	height: 58px;
    /* border: 1px solid #000; */
	transform-origin: top right;
    transform: rotate(90deg);
    overflow: hidden;
}

.rightHandBottom {
    position: absolute;
	top: 1px;
	left: 38px;
    width: 68px;
	height: 28px;
    border: 1px solid #000;
    border-bottom-right-radius: 100% 40px;
}

```

![image.png](https://upload-images.jianshu.io/upload_images/735083-a01988e53a12014b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

是不是漂亮很多了， 那快点把脚的部分也完成吧,和手的结构基本类似。

```html
<!-- 脚 -->
<div class="footWrapper">
    <div class="leftFootTopWrapper">
        <div class="leftFootTop"></div>
    </div>
    <div class="leftFootBottomWrapper">
        <div class="leftFootBottom"></div>
    </div>
    <div class="rightFootTopWrapper">
        <div class="rightFootTop"></div>
    </div>
    <div class="rightFootBottomWrapper">
        <div class="rightFootBottom"></div>
    </div>
</div>
```

基础位置布局

```css
/* QQ footerWrapper */
.footWrapper{
    /* 定位起始点 */
	position: absolute;
	top: 292px;
    left: 80px;
    width: 300px;
    height: 80px;
    border: 1px solid #000;
}

/* QQ footerWrapper -> left */
.leftFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 16px;
	left: -1px;
    width: 130px;
    height: 37px;
    border: 1px solid #000;
}

.leftFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: -1px;
	width: 130px;
	height: 38px;
    border: 1px solid #000;
}

/* QQ footerWrapper -> right */
.rightFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 22px;
	left: 134px;
    width: 130px;
    height: 38px;
    border: 1px solid #000;
}

.rightFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: 134px;
	width: 134px;
    height: 38px;
    border: 1px solid #000;
}

```

![](https://upload-images.jianshu.io/upload_images/735083-6da4644949bd9d59.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

轮廓调整

```css

/* QQ footerWrapper */
.footWrapper{
    /* 定位起始点 */
	position: absolute;
	top: 292px;
    left: 80px;
    width: 300px;
    height: 80px;
    /* border: 1px solid #000; */
}

/* QQ footerWrapper -> left */
.leftFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 16px;
	left: -1px;
    width: 130px;
    height: 37px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.leftFootTop {
    position: absolute;
	top: -10px;
    left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid black;
    border-top-left-radius: 80% 70%;
}

.leftFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: -1px;
	width: 130px;
	height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.leftFootBottom {
    position: absolute;
    top: -30px;
	left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid #000;
    border-top-left-radius: 50% 44%;
	border-top-right-radius: 50% 44%;
	border-bottom-left-radius: 50% 56%;
	border-bottom-right-radius: 50% 56%;
}

/* QQ footerWrapper -> right */
.rightFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 22px;
	left: 134px;
    width: 130px;
    height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.rightFootTop {
    position: absolute;
    top: 0px;
	left: 4px;
    width: 120px;
	height: 60px;
    border: 4px solid black;
    border-top-right-radius: 32% 65%;
}

.rightFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: 134px;
	width: 134px;
    height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.rightFootBottom {
    position: absolute;
    top: -30px;
	left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid #000;
    border-top-left-radius: 50% 56%;
	border-top-right-radius: 50% 56%;
	border-bottom-left-radius: 50% 44%;
	border-bottom-right-radius: 50% 44%;
}

```

![image.png](https://upload-images.jianshu.io/upload_images/735083-e87099428af2318f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

基本整体框架结构就出来了，开始上色吧。上色的过程可以帮助我们调整z-index，也就是各个模块的重叠层次，遮盖了一些无用的线条和框角。

1. head 开始

```css
 /* QQ head */
.head {
    position: absolute;
    top: 18px;
    left: 96px;
    width: 234px;
    height: 185px;
    border: 1px solid #000;
    border-top-left-radius: 117px 117px;
    border-top-right-radius: 117px 117px;
    border-bottom-left-radius: 117px 68px;
    border-bottom-right-radius: 117px 68px;
    background: #000;
}

/* QQ head -> eye */
.eye {
    position: absolute;
    width: 44px;
    height: 66px;
    border:1px solid #000;
    border-radius: 50% 50%;
    background: #fff;
}

.left.eye {
    left: 62px;
    top: 50px;
}

.right.eye {
    left: 132px;
    top: 50px;
}

.innerLeftEye {
    position: absolute;
    top: 20px;
    left: 20px;
    width: 18px;
    height: 24px;
    border-radius: 50%;
    border: 1px solid #000;
    background: #000;
}

.innerLeftEye::after {
    content: "";
    position: absolute;
    top: 6px;
    left: 9px;
    width: 6px;
    z-index: 11;
    height: 8px;
    /* border: 1px solid #000; */
    border-radius: 50%;
    background: #fff;
}

.innerRightEye {
    position: absolute;
    top: 20px;
    left: 8px;
    /* 月牙眼球外轮廓 */
    width: 18px;
    height: 24px;
    /* border: 1px solid #000; */
    border-top-left-radius: 50% 90%;
    border-top-right-radius: 50% 90%;
    border-bottom-left-radius: 50% 10%;
    border-bottom-right-radius: 50% 10%;
    background: black;
    box-shadow: 0 -1px 2px black;
}

.innerRightEye::after {
    content: "";
    position: absolute;
    bottom: -1px;
	left: 4px;
    /* 月牙眼球内部轮廓 */
    width: 10px;
    height: 13px;
    /* border: 1px solid #000; */
    border-top-left-radius: 50% 100%;
    border-top-right-radius: 35% 80%;
    background: #FFF;
}

.fix {
    position: absolute;
    top: 19px;
    width: 4px;
    height: 4px;
    /* border: 1px solid #000; */
    border-radius: 50%;
    background: #000;
}

.fix:after{
	content: "";
    position: absolute;
    top: 0;
	left: 14px;
	width: 4px;
    height: 4px;
    /* border: 1px solid #000; */
    border-radius: 50%;
    background: black;
}

/* QQ head -> mouth */
.mouthTopContainer {
    /* 定位 */
    position: absolute;
    top: 120px;
    left: 39px;
    z-index: 1;
    width: 158px;
    height: 29px;
    overflow: hidden; /* 隐藏超出部分 */
}

.mouthTop {
    /* 上嘴唇轮廓 */
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    width: 158px;
    height: 34px;
    border: 1px solid #FFA600;
    border-top-left-radius: 45% 34px;
    border-top-right-radius: 45% 34px;
    background: #FFA600;
}

.mouthBottomContainer {
    position: absolute;
    top: 146px;
    left: 39px;
    z-index: 1;
    width: 158px;
    height: 15px;
    overflow: hidden;   /* 隐藏超出部分 */
}

.mouthBottom {
    position: absolute;
    top: -4px;
    left: 0;
    z-index: 1;
    width: 158px;
    height: 24px;
    border: 1px solid #FFA600;
    border-top:none;
    border-bottom-left-radius: 45% 24px;
    border-bottom-right-radius: 45% 24px;
    background: #FFA600;
}

/* 嘴唇上下层次感-咬合部位 */
.lispContainer {
    /* 定位 */
    position: absolute;
	top: 146px;
	left: 60px;
    width: 116px;
    height: 24px;
}

.lips {
    position: absolute;
	top: 0;
	left: 0;
    width: 116px;
    height: 24px;
    border: 1px solid #FFA600;
    border-bottom-left-radius: 50% 100%;
    border-bottom-right-radius: 50% 100%;
    background: #FFA600;
}

```

![](https://upload-images.jianshu.io/upload_images/735083-3279852d229a27cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2. body

```css
/* QQ body */
.body {
    /* body 容器定位 */
    position: absolute;
    top: 135px;
    left: 48px;
    width: 326px;
    height: 300px;
    /* border: 1px solid #000; */
}

/* QQ body -> scarf */
.scarf {
    position: absolute;
    top: -2px;
    left: 34px;
    z-index: 5;
    width: 258px;
    height: 110px;
    border: 1px solid #000;
    border-top-left-radius: 30px 34px;
	border-top-right-radius: 38px 34px;
	border-bottom-left-radius: 50% 76px;
    border-bottom-right-radius: 50% 76px;
    border-top: none;
    background: #FB0009;
}

/* QQ body -> scarfEnd */
.scarfEnd {
    position: absolute;
    left: 74px;
    top: 90px;
	width: 52px;
    height: 64px;
    border: 3px solid black;
    border-bottom-left-radius: 50% 43%;
	border-bottom-right-radius: 15px;
    border-top-left-radius: 20% 57%;
    background: #FB0009;
}

/* QQ body -> innerWrapper */
.innerWrapper {
    /* innerWrapper 容器定位 */
    position: absolute;
    left: 30px;
	top: 76px;
    width: 280px;
    height: 200px;
    overflow: hidden;
}

.inner {
    position: absolute;
    left: 25px;
	top: -71px;
	width: 218px;
	height: 210px;
    border: 1px solid #000;
    border-radius: 50%;
    background: #fff;
}

/* QQ body -> outerWrapper */
.outerWrapper{
    /* outerWrapper 容器定位 */
    position: absolute;
	top: 54px;
	overflow: hidden;
    width: 262px;
	left: 32px;
    height: 250px;
}

.outer{
    position: absolute;
	top: -84px;
	width: 260px;
    height: 250px;
    border: 1px solid #000;
    border-radius: 125px;
    background: #000;
}
```
![](https://upload-images.jianshu.io/upload_images/735083-3ff41fd4ce75871f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上色后你会发现，有的图层显示先后顺序不对，需要调整下先后顺序。
  * head > body
  * body里（scafEnd > inner > outer）

![image.png](https://upload-images.jianshu.io/upload_images/735083-5ba38d5b1a347adc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


3. hand

```css
/* QQ handWrapper -left */
.leftHandTopContainer {
    /* 定位 */
	position: absolute;
	top: 55px;
	left: 50px;
    width: 118px;
    height: 26px;
    /* border: 1px solid #000; */
	transform-origin: bottom left;
    transform: rotate(-70deg);
    overflow: hidden;
}

.leftHandTop {
     /* 上半部分 */
	width: 128px;
	height: 54px;
    border: 1px solid #050346;
    border-top-left-radius: 44% 38px;
    border-top-right-radius: 56% 33px;
    background: #000;
}

.leftHandBottomContainer {
    /* 定位 */
    position: absolute;
	top: 78px;
	left: 50px;
	width: 100px;
    height: 30px;
    /* border: 1px solid #000; */
	transform-origin: top left;
    transform: rotate(-70deg);
    overflow: hidden;
}

.leftHandBottom {
    position: absolute;
    top: -26px;
    width: 128px;
	height: 44px;
    border: 1px solid #050346;
    border-bottom-left-radius: 48% 20px;
    border-bottom-right-radius: 52% 23px;
    background: #000;
}

/* QQ handWrapper -right */
.rightHandTopContainer {
    /* 定位 */
    position: absolute;
	top: 47px;
	left: 240px;
    width: 118px;
    height: 34px;
    /* border: 1px solid #000; */
	transform-origin: bottom right;
    transform: rotate(65deg);
    overflow: hidden;
}

.rightHandTop {
    position: absolute;
    left: -30px;
    width: 148px;
	height: 54px;
    border: 1px solid #050346;
    border-top-right-radius: 41% 54px;
    border-top-left-radius: 59% 48px;
    background: #000;
}

.rightHandBottomContainer{
    /* 定位 */
    position: absolute;
	top: 81px;
    left: 248px;
	width: 110px;
	height: 58px;
    /* border: 1px solid #000; */
	transform-origin: top right;
    transform: rotate(90deg);
    overflow: hidden;
}

.rightHandBottom {
    position: absolute;
	top: 1px;
	left: 38px;
    width: 68px;
	height: 28px;
    border: 1px solid #000;
    border-bottom-right-radius: 100% 40px;
    background: #000;
}

```

4. footer

```css
/* QQ footerWrapper */
.footWrapper{
    /* 定位起始点 */
	position: absolute;
	top: 292px;
    left: 80px;
    width: 300px;
    height: 80px;
    /* border: 1px solid #000; */
}

/* QQ footerWrapper -> left */
.leftFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 16px;
	left: -1px;
    width: 130px;
    height: 37px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.leftFootTop {
    position: absolute;
	top: -10px;
    left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid black;
    border-top-left-radius: 80% 70%;
    background: #FF9C00;
}

.leftFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: -1px;
	width: 130px;
	height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.leftFootBottom {
    position: absolute;
    top: -30px;
	left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid #000;
    border-top-left-radius: 50% 44%;
	border-top-right-radius: 50% 44%;
	border-bottom-left-radius: 50% 56%;
    border-bottom-right-radius: 50% 56%;
    background: #FF9C00;
}

/* QQ footerWrapper -> right */
.rightFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 22px;
	left: 134px;
    width: 130px;
    height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.rightFootTop {
    position: absolute;
    top: 0px;
	left: 4px;
    width: 120px;
	height: 60px;
    border: 4px solid black;
    border-top-right-radius: 32% 65%;
    background: #FF9C00;
}

.rightFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: 134px;
	width: 134px;
    height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.rightFootBottom {
    position: absolute;
    top: -30px;
	left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid #000;
    border-top-left-radius: 50% 56%;
	border-top-right-radius: 50% 56%;
	border-bottom-left-radius: 50% 44%;
    border-bottom-right-radius: 50% 44%;
    background: #FF9C00;
}

```
![image.png](https://upload-images.jianshu.io/upload_images/735083-99c72e3873c6d815.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到了这里基本完成了 90% 了， 剩下的就是线条优化，使 QQ 看起来更有层次感、立体感。

**嘴唇**

嘴巴的形状不够性感、立体；绘制一个斜边三角形，修复嘴唇的层次感。

![斜边三角形](https://upload-images.jianshu.io/upload_images/735083-023166cf198da7d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

绘制这样一个斜边三角形，步骤分解如图所示：

![步骤分解](https://upload-images.jianshu.io/upload_images/735083-be6e95b7c5f9eb65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

先是绘制一个普通三角形，通过逆时针旋转得到一个修复三角形，那么相对称的修复三角形可以通过使用rotateY，绕着Y轴旋转180度，来得到。

```html
<!-- 嘴唇上下层次感 -->
<div class="lispContainer">
    <div class="lips">
        <!-- 左右上下嘴唇咬合阴影  -->
        <div class="lipShadow left"></div>
        <div class="lipShadow right"></div>
    </div>
</div>
```

```css
/* 嘴唇上下层次感-咬合部位 */
.lispContainer {
    /* 定位 */
    position: absolute;
	top: 146px;
	left: 60px;
    width: 116px;
    height: 24px;
}

.lips {
    position: absolute;
	top: 0;
	left: 0;
    width: 116px;
    height: 24px;
    border: 1px solid #FFA600;
    border-bottom-left-radius: 50% 100%;
    border-bottom-right-radius: 50% 100%;
    background: #FFA600;
}

.lipShadow {
    position: absolute;
    width: 0px;
    height: 0px;
    border-top: 20px solid transparent;
	border-bottom: 20px solid transparent;
	border-right: 8px solid black;
	transform-origin: top right;
    transform: rotate(-60deg);
    z-index: 2;
}

.lipShadow.left {
    top: 4px;
    left: -12px;
    transform: rotate(-60deg);
}

.lipShadow.right {
    top: 4px;
    left: 111px;
    transform: rotate(60deg) rotateY(180deg);
}

```

![image.png](https://upload-images.jianshu.io/upload_images/735083-abec1dc060e0f831.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**围巾**

围脖竟然没折痕，不立体； 通过绘制一个“小尾巴”来进行美化

![小尾巴](https://upload-images.jianshu.io/upload_images/735083-7b31b363591cc7f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```css
border-right: 6px solid black;
width: 100px;
height: 70px;
border-bottom-right-radius: 70px 70px;
```
当对一个角应用圆角样式，如果这个角相邻的两个border一个有定义而一个无定义，那么绘制的结果就是由粗到细的“小尾巴了”。[在整个绘制过程中，同一个图形它的绘制方法有很多种，例如一个矩形可以用 width x height构成，也可以由border x height(width)构成，甚至可以由border组合(width = height = 0)构成，根据情况选择吧。]

```html
<!-- 围巾 -->
<div class="scarf">
    <div class="scarfShadow"></div>
    <div class="scarfShadowRight"></div>
</div>
<!-- 围巾尾 -->
<div class="scarfEnd">
    <div class="scarfEndShadow"></div>
</div>
</div>
```

```css
/* QQ body -> scarf */
.scarf {
    position: absolute;
    top: -2px;
    left: 34px;
    z-index: 5;
    width: 258px;
    height: 110px;
    border: 4px solid #000;
    border-top-left-radius: 30px 34px;
	border-top-right-radius: 38px 34px;
	border-bottom-left-radius: 50% 76px;
    border-bottom-right-radius: 50% 76px;
    border-top: none;
    background: #FB0009;
}

.scarfShadowLeft {
    position: absolute;
    top: 0px;
	left: 6px;
	width: 60px;
    height: 70px;
    /* border: 4px solid #000; */
    border-top: 6px solid #000;
	border-top-left-radius: 90px 120px;
    border-top-right-radius: 30px 30px;
	transform: rotate(-79deg);
}

.scarfShadowRight {
    position: absolute;
    top: 8px;
	left: 143px;
	width: 100px;
    height: 70px;
    /* border: 4px solid #000; */
    border-right: 6px solid black;
	width: 100px;
    border-bottom-right-radius: 70px 70px;
    border-right: 6px solid black;
}

/* QQ body -> scarfEnd */
.scarfEnd {
    position: absolute;
    left: 74px;
    top: 90px;
	width: 52px;
    height: 64px;
    border: 3px solid black;
    border-bottom-left-radius: 50% 43%;
	border-bottom-right-radius: 15px;
    border-top-left-radius: 20% 57%;
    background: #FB0009;
    z-index: 4;
}

.scarfEndShadow {
    position: absolute;
    top: 6px;
	left: 12px;
	width: 20px;
    height: 20px;
    /* border: 4px solid #000; */
    border-top: 6px solid #000;
    border-top-left-radius: 30px 30px;
    transform-origin: top right;
    transform: skewX(4deg) scaleY(1.5) rotate(-60deg);
}
```

![image.png](https://upload-images.jianshu.io/upload_images/735083-ed8a80d97ac978cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**脚**

也是通过绘制`小尾巴`来进行美化

```html
<!-- 脚 -->
<div class="footWrapper">
    <div class="leftFootTopWrapper">
        <div class="leftFootTop"></div>
    </div>
    <div class="leftFootBottomWrapper">
        <div class="leftFootBottom"></div>
    </div>
    <!-- 脚趾间隔线条 -->
    <div class="toe left"></div>
    <div class="rightFootTopWrapper">
        <div class="rightFootTop"></div>
    </div>
    <div class="rightFootBottomWrapper">
        <div class="rightFootBottom"></div>
    </div>
    <!-- 脚趾间隔线条 -->
    <div class="toe right"></div>
</div>
```

```css
/* QQ footerWrapper */
.footWrapper{
    /* 定位起始点 */
	position: absolute;
	top: 292px;
    left: 80px;
    width: 300px;
    height: 80px;
    /* border: 1px solid #000; */
}

.toe {
    position: absolute;
	width: 25px;
	height: 20px;
    /* border: 4px solid #000; */
    border-top: 4px solid black;
    border-top: 4px solid black;
    border-top-right-radius: 30px 30px;
    border-top-left-radius: 10px 10px;
    transform-origin: top left;
    z-index: 10;
}

/* QQ footerWrapper -> left */
.leftFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 16px;
	left: -1px;
    width: 130px;
    height: 37px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.leftFootTop {
    position: absolute;
	top: -10px;
    left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid black;
    border-top-left-radius: 80% 70%;
    background: #FF9C00;
}

.toe.left {
    top: 50px;
    left: 2px;
    transform: rotate(-45deg);
}

.leftFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: -1px;
	width: 130px;
	height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.leftFootBottom {
    position: absolute;
    top: -30px;
	left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid #000;
    border-top-left-radius: 50% 44%;
	border-top-right-radius: 50% 44%;
	border-bottom-left-radius: 50% 56%;
    border-bottom-right-radius: 50% 56%;
    background: #FF9C00;
}

/* QQ footerWrapper -> right */
.rightFootTopWrapper {
    /* 定位左脚上容器 */
    position: absolute;
	top: 22px;
	left: 134px;
    width: 130px;
    height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.rightFootTop {
    position: absolute;
    top: 0px;
	left: 4px;
    width: 120px;
	height: 60px;
    border: 4px solid black;
    border-top-right-radius: 32% 65%;
    background: #FF9C00;
}

.toe.right {
    top: 50px;
    left: 264px;
    transform: rotate(45deg) rotateY(180deg);
}

.rightFootBottomWrapper {
    position: absolute;
    top: 52px;
	left: 134px;
	width: 134px;
    height: 38px;
    /* border: 1px solid #000; */
    overflow: hidden;
}

.rightFootBottom {
    position: absolute;
    top: -30px;
	left: 3px;
    width: 120px;
	height: 60px;
    border: 4px solid #000;
    border-top-left-radius: 50% 56%;
	border-top-right-radius: 50% 56%;
	border-bottom-left-radius: 50% 44%;
    border-bottom-right-radius: 50% 44%;
    background: #FF9C00;
}
```

![](https://upload-images.jianshu.io/upload_images/735083-83d108138f73a931.png?imageMogr2/auto-orient/striCimageView2/2/w/1240)

大功告成，一个生动的 QQ 企鹅就绘制完了～

介绍下这个过程中几个比较典型的图形绘制方法：

1、企鹅的眼睛：椭圆，直接设置border-radius:50% 50%; 即可[因为宽高分别为44px和66px，所以也可以这样设定：border-radius: 22px / 33px]

2、围脖的尾部：一个圆角各异的矩形，所以这里需要对几个角分别设定border-radius，微调的结果为

```css
border-bottom-left-radius: 50% 43%;
border-bottom-right-radius: 15px;
border-top-left-radius: 20% 57%;
```
3、企鹅的胳膊：手的绘制较为麻烦一点，可以分为上下两个部分，将绘制的结果拼接到一起。那么对于不需要的部分怎么办呢？我们可以将上(下)部分放到一个div(container)中，利用overflow:hidden的属性来截取所要的部分。绘制复杂图形的时候常用的方法就是切割和拼接，将图形切割成一个个简单的小块，通过层叠和旋转变化进行组合。

使用transform:rotate(deg)的时候，优先设定transform-origin属性，会比较方便。设定的点作为中心点，整个图形绕着这个点进行角度变化。例如：transform-origin:bottom left， 使用左下角作为原点。也可以使用具体的像素值和百分比。

在基本的框架线条中比非常多的使用了border-radius用于构造各种曲线条，小企鹅是圆圆胖胖的，:)

[本文参考](http://www.alloyteam.com/2012/10/css3-draw-qq-logo/#prettyPhoto)
