问题：在 ios 中的 swiper 中当 loop 为 true 的时候，常常显示的是最后一张图的图片。
解决方案：

```js
<Swiper
  ref="scrollView"
  loop={true}
  horizontal={true}
  showsHorizontalScrollIndicator={false}
  pagingEnabled={true}
>
  <Text>1212</Text>
</Swiper>
 componentDidUpdate() {

                     var ScrollView = this.refs.scrollView;
                    ScrollView.scrollBy(0, false)
           }

```
