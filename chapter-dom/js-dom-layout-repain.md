#重排和重绘

#### 1. 导致重排的行为

* Visible DOM elements are added or removed：添加或删除可见的DOM元素
* Elements change position ：元素位置改变
* Elements change size (because of a change in margin, padding, border thickness, width, height, etc.) ：元素尺寸改变（因为边距，填充，边框宽度，宽度，高度等属性改变）
* Content is changed, e.g., textchanges or an image is replaced with one of a different size ：内容改变，例如，文本改变或图片被另一个不同尺寸的所替代
* Page renders initially ：最初的页面渲染
* Browser window is resized ：浏览器窗口改变尺寸

#### 2. 导致队列刷新的操作

Because of the computation costs associated with each reflow, most browsers **optimize the reflow process by queuing changes** and performing them in batches. 

因为计算量与每次重排版有关，大多数浏览器通过队列化修改和批量显示优化重排版过程。

* offsetTop, offsetLeft, offsetWidth, offsetHeight 
* scrollTop, scrollLeft, scrollWidth, scrollHeight 
* clientTop, clientLeft, clientWidth, clientHeight
* getComputedStyle()(currentStylein IE)（在IE中此函数称为currentStyle）

修改样式中，尽可能避免使用上述属性。

#### 3. 最小化重绘和重排

尽可能批量修改DOM，可以通过下面的步骤减少重绘和重排的次数：

* 使元素脱离文档流
    * 隐藏元素，进行修改，然后再显示它
    * 使用一个文档片断(document fragment)在已存DOM之外创建一个子树，然后将它拷贝到文档中(**推荐！它所产生的DOM遍历和重排次数最少**)
    * 将原始元素拷贝到一个脱离文档的节点中，修改副本，然后覆盖原始元素
* 对其应用多重改变

#### 4. 其他性能优化建议

#####(1) 缓存布局信息
#####(2) 让元素脱离动画流
建议：
* 页面顶部可以“折叠/展开”的元素称作“动画元素”，用绝对坐标对它进行定位，当它的尺寸改变时，就不会推移页面中其他元素的位置，而只是覆盖其他元素。
* 展开动作只在“动画元素”上进行。这时其他元素的坐标并没有改变，换句话说，其他元素并没有因为“动画元素”的扩大而随之下移，而是任由动画元素覆盖。
* “动画元素”的动画结束时，将其他元素的位置下移到动画元素下方，界面“跳”了一下

#####(3) 使用事件委托
每绑定一个事件处理器都是有代价的：
* 加重了页面负担（更多的页面标记和JavaScript代码）
* 增加运行期的执行时间上

需要访问和修改更多的DOM节点，程序就会更慢。