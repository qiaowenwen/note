#pdf 的相关问题 ###在交易流程的开发过程中，遇到签章无法显示的问题。在手机端的打开 pdf 的方式用的是连接跳转，但是打开的过程中发现只有改的章并没有显示在上面。 ##解决方案：安卓是进行更改配置。但 ios 利用一些处理，ios12 却不能兼容，最终采用的办法是，h5 采用 pdf.js 进行处理  
[pdf.js 地址]（https://mozilla.github.io/pdf.js/getting_started/）

##在本次过程中遇到的一些问题
（1）同样，前端也遇到不能签章无法显示的问题

```js
```

（2）在每次加载之后，当再次打开，希望从头开始,在阅读了源码后发现在文章中会将位置每次都进行了存储。于是将每次的存

```js
// 更改前
databaseStr = JSON.stringify(this.database)
localStorage.setItem('pdfjs.history', databaseStr)
// 更改后
this.database = ''
databaseStr = JSON.stringify(this.database)
localStorage.setItem('pdfjs.history', databaseStr)
```

(3)pdf.js 文件太大，解决方案是将一些不必要的功能进行隐藏，将一些不必要的图片删除例如 image 文件
