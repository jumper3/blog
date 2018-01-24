---
title: CSS 动画 | MDN照搬委员会
date: 2018-1-18 16:07:59
tags: CSS
---

从Animated.css的源码里能学到什么呢？

```css
.animated {
  -webkit-animation-duration: .8s;
  animation-duration: .8s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
```

`animation-duration`： 动画时长

[animation-fill-mode](http://www.w3school.com.cn/cssref/pr_animation-fill-mode.asp)：属性规定动画在播放之前或之后，其动画效果是否可见



#### 关键帧

> `@keyframes` 让开发者通过指定动画中特定时间点必须展现的关键帧样式（或者说停留点）来控制CSS动画的中间环节。
>
> 
>
> 要使用关键帧, 先创建一个带名称的`@keyframes`规则，以便后续使用 [`animation-name`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-name) 这个属性来调用指定的`@keyframes`。 每个`@keyframes` 规则包含多个关键帧，每个关键帧有一个百分比值作为名称，代表在动画进行中，在哪个阶段触发这个帧所包含的样式。
>
> 
>
> 关键帧的编写顺序没有要求，最后只会根据百分比按由小到大的顺序触发。



```css
@-webkit-keyframes fadeInLeft {
  from {
    opacity: 0.5;
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}

@keyframes fadeInLeft {
  from {
    opacity: 0.5;
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}

.fadeInLeft {
  -webkit-animation-name: fadeInLeft;
  animation-name: fadeInLeft;
}
```

其中，from、to 又可以更换为关键帧百分比，如0% 50% 100%

那动画之中主要又操作的是什么呢？



#### transform

> transform 属性向元素应用 2D 或 3D 转换。该属性允许我们对元素进行旋转、缩放、移动或倾斜。



| 值                                        | 描述                     |
| ---------------------------------------- | ---------------------- |
| none                                     | 定义不进行转换。               |
| matrix(*n*,*n*,*n*,*n*,*n*,*n*)          | 定义 2D 转换，使用六个值的矩阵。     |
| matrix3d(*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*） |                        |
| translate(*x*,*y*)                       | 定义 2D 转换。              |
| translate3d(*x*,*y*,*z*)                 | 定义 3D 转换。              |
| translateX(*x*)                          | 定义转换，只是用 X 轴的值。        |
| translateY(*y*)                          | 定义转换，只是用 Y 轴的值。        |
| translateZ(*z*)                          | 定义 3D 转换，只是用 Z 轴的值。    |
| scale(*x*,*y*)                           | 定义 2D 缩放转换。            |
| scale3d(*x*,*y*,*z*)                     | 定义 3D 缩放转换。            |
| scaleX(*x*)                              | 通过设置 X 轴的值来定义缩放转换。     |
| scaleY(*y*)                              | 通过设置 Y 轴的值来定义缩放转换。     |
| scaleZ(*z*)                              | 通过设置 Z 轴的值来定义 3D 缩放转换。 |
| rotate(*angle*)                          | 定义 2D 旋转，在参数中规定角度。     |
| rotate3d(*x*,*y*,*z*,*angle*)            | 定义 3D 旋转。              |
| rotateX(*angle*)                         | 定义沿着 X 轴的 3D 旋转。       |
| rotateY(*angle*)                         | 定义沿着 Y 轴的 3D 旋转。       |
| rotateZ(*angle*)                         | 定义沿着 Z 轴的 3D 旋转。       |
| skew(*x-angle*,*y-angle*)                | 定义沿着 X 和 Y 轴的 2D 倾斜转换。 |
| skewX(*angle*)                           | 定义沿着 X 轴的 2D 倾斜转换。     |
| skewY(*angle*)                           | 定义沿着 Y 轴的 2D 倾斜转换。     |
| perspective(*n*)                         | 为 3D 转换元素定义透视视图。       |

可以查看w3c中的例子：[transform](http://www.w3school.com.cn/cssref/pr_transform.asp)



#### 动画效果叠加

更让人激动的是什么呢？

我们可以吧多个transform的值应用在一个transform上，就像这样

```css
@keyframes triangleRotate {
  100% {
    -webkit-transform: rotate(90deg) translateX(.3rem); 
    transform: rotate(90deg) translateX(.3rem); 
  }
}
```