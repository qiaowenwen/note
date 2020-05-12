问题：在 ios 中的 swiper 中当 loop 为 true 的时候，常常显示的是最后一张图的图片。
解决方案：

```js
//注意版本的升级，不一定是npm中的，也有可能在github中有更高的版本
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

参考文档（1）https://blog.csdn.net/book_1992/article/details/79744877
（ 2）https://github.com/leecade/react-native-swiper
