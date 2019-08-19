#背景图片的自适应的问题 
###最近开发中遇到一个问题就是在背景图片设置的过程中由于需要撑开内容。

####问题 1 背景的周围有阴影
####解决方案： 可以设置背景色，在背景色之上设置背景图片

####问题 2 类似于 title 的，形状不规则的的 
####解决方案：通常会将分为三个部分，两边的和中间的部分，中间可以进行部分的截取。在中间的部分的设置 repeat-x

![markdown](/img/title.png)

```html
<div class="knowledge-card-title-img">
  <div class="knowledge-card-title-left"></div>
  <div class="knowledge-card-title-middle">哈哈哈哈哈</div>
  <div class="knowledge-card-title-right"></div>
</div>
```

```css
.knowledge-card-title-left {
  float: left;
  background-image: url('./img/left.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  width: 12px;
  height: 32px;
}

.knowledge-card-title-right {
  float: left;
  background-image: url('./img/right.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  width: 12px;
  height: 32px;
}

.knowledge-card-title-middle {
  padding: 0 8px;
  float: left;
  background-image: url('./img/middle.png');
  background-size: 100% 100%;
  background-repeat: repeat-x;
}
```

####总结：<span style="color:red">（1）一旦内容可变的，背景图是会跟着变。尽量使图片设置背景色。（2） 遇到形状较为负责的情况，根据观察，去设置不同的情况。</span>
