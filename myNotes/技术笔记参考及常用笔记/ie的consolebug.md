对于ie9以下不打开控制台页面的console.log（）的报错解决办法：
我们可以在页面中加入如下 js 代码，其作用是：
如果浏览器支持 console，则输出内容。
不支持的（如：IE8、IE9）则不会输出，从而不会导致错误。
```javaScript
<script type="text/javascript">
  //解决 IE8、IE9 不支持 console 问题
  window.console = window.console || (function () {
    var c = {}; c.log = c.warn = c.debug = c.info = c.error = c.time = c.dir = c.profile
    = c.clear = c.exception = c.trace = c.assert = function () { };
    return c;
  })();
</script>
```