# document.write

加载文档时，用```document.write(text)```可以直接往文档里面写入内容，这部分内容会以HTML的形式被渲染。

    <script>
      document.write('*Hello, there!*');
    </script>

```document.write(text)```中的text没有严格的格式要求，可以包含非法标签或者不闭合标签。

注意：

* ```document.write(text)```应该往一个未加载完成的文档中写入内容，原文是：


> Both document.write and document.writeln method should output text into an unready (open) document.

当页面加载完成，文档流关闭。此时再调用```document.write()```，会先清楚文档内容，然后写入新的内容。原文为：
> When the page finishes loading, the document becomes closed. An attempt to document.write in it will cause the contents to be erased.

* 如果用```document.write()```来加载JS文件，那么会阻塞页面渲染。