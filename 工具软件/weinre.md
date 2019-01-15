##简介
weinre 是一款可以在 pc 端调试手机端网页的工具 ##安装
weinre 基于 nodejs，因此首先要安装 nodejs，然后使用 npm 进行安装：</br>
npm -g install weinre 
##运行
weinre --boundHost 10.32.69.133(代表本机服务器的地址) --httpPort 8888(占用的端口号) 
##调试
在网页端打开如上的连接，然后将如下的代码复制到需要调试的页面中

```js
<script src="http://172.16.188.107:8081/target/target-script-min.js#anonymous" />
```

如果有其他的可以进行其他的操作

在手机端运行即可
