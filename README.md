# 前端开发面试题

## 一、HTML&CSS

#### 1. 清除浮动的方式

**clear**

在浮动元素后添加一个空div，利用css提高的clear:both清除浮动

**overflow**

在具有float子元素的父元素容器中设置“overflow”的属性为"hidden"或"auto"

```css
.container {
    background: #e8eae9;
    overflow: hidden;
}
```

**clearfix**

"clearfix"是基于在父元素上使用":before"和":after"这两个伪类，这两个伪类可以在float元素的父容器前后创建隐藏元素。

- ":before"和":after"伪类均使用"display:table",创建一个匿名的"table-cell"元素。分别用于防止子元素的顶部和底部的外边距坍塌。
- 同时":after"伪类还用来清除元素的浮动

```css
.clearfix:before,
.clearfix:after {
    content: "";
    display: table;
}

.clearfix:after {
    clear: both;
}

.clearfix {
    *zoom: 1; <!--IE6/7 上用于触发父元素的hasLayout机制-->
}
```

**注意：**每个元素只有一个":before"和":after"伪类，当尝试使用其他":before"和":after"技巧时，可能回合clearfix的清除浮动技巧发送冲突而不起作用。



#### 2. jpg&png

**体积大小**

png24>jpg(100%)>gif≈png8 

**图片质量**

png24属于一种无损压缩格式，支持约1600万色，因此基本能够完完全全的表现出原图的一切细节，但图片体积会非常的大。

jpg属于有损压缩格式，牺牲了一定的画质，但却非常好的控制住了图片的体积。在图片不是特别锐利的情况下，图片质量基本能够和png24看齐，体积却小了png24好多倍。

gif和png8仅支持256色，图片体积很小，但不是适合表现丰富的图片

**使用场景**

对于像logo、色彩种类单一的图片：一般使用png24/8格式，图片体积小，效果好，、使用png8的时候要注意，因为其只支持256色，因此有时会有色差。

复杂的图片，例如：人物，风景：一般采用jpg格式，这时若采用png24格式，图片大小往往会数倍于jpg，同时也未必能展现出更好的效果。

透明背景图片：只能选取png24/8、或者gif这种支持透明背景的图片格式。



####  3. Cookie，sessionStorage 和 localStorage 的区别？ 

Cookie是由网景公司创建的，目的就是将用户的数据储存在客户端上。伴随的HTML5的出现，现在又有另外一个解决数据离线储存的方案，就是HTML5中的Web storage，其中两个重要对象sessionStorage和localStorage可以解决浏览器sessions和长期储存数据的目的



1. Cookie

* 数据生命期：一般由服务器生成，可设置失效时间。如果在浏览器端生成Cookie，默认是关闭浏览器后失效

* 数据大小：4K左右

* 与服务器端通信：每次都会携带在HTTP头部中，如果使用Cookie保存过多数据会带来性能问题

* 易用性：需要自己封装，原生Cookie接口不友好

  

2. localStorage

- 数据生命期：除非被清除，否则永久保存 
- 数据大小：一般为5M
- 与服务器端通信：仅在客户端（即浏览器）中保存，不参与和服务器的通信 
- 易用性：源生接口可以接受，亦可再次封装来对Object和Array有更好的支持



3. sessionStorage

- 数据生命期：仅在当前会话下有效，关闭页面或浏览器后被清除 
-  其余同上



## 二、JavaScript

#### 1. 内存泄漏

**什么是内存泄漏**

程序的运行需要内存。只要程序提出要求，操作系统或者运行时（runtime）就必须供给内存。对于持续运行的服务进程（daemon），必须及时释放不再用到的内存。否则，内存占用越来越高，轻则影响系统性能，重则导致进程崩溃。不再用到的内存，没有及时释放，就叫做内存泄漏（memory leak）。

JavaScript提供了自动内存管理，减轻程序员的负担，这被称为"垃圾回收机制"（garbage collector）。



 **识别内存泄漏**

* 浏览器
  1. 打开开发者工具，选择 Timeline 面板
  2. 在顶部的`Capture`字段里面勾选 Memory
  3. 点击左上角的录制按钮。
  4. 在页面上进行各种操作，模拟用户的使用情况。
  5. 一段时间后，点击对话框的 stop 按钮，面板上就会显示这段时间的内存占用情况。
  6. 如果内存占用基本平稳，接近水平，就说明不存在内存泄漏 。



**常见 JavaScript 内存泄漏原因**

1. 意外的全局变量引起的内存泄露   
2. 闭包引起的内存泄露 
3. 没有清理的DOM元素引用 
4. 被遗忘的定时器或者回调 

## 三、 JQuery

#### 1. 事件委托

事件委托用于解决事件处理程序过多的问题。事件委托利用了事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件，利用父级去触发子级的事件。



e.g. 要求在表格(table)元素中的每个格子(td)都绑定一个点击(click)事件

```javascript
$("table").on("click", "td", function() {
    $(this).toggleClass("click");
});
```

也可以绑定在document对象上，但有时会影响性能，具体根据页面DOM结构决定

```javascript
$(document).on("click", "td", function() {
    $(this).toggleClass("click");
});
```

off()方法，取消事件绑定

```js
$("table").off("click", "td");
```

one()方法，绑定元素执行完毕后自动移除事件，可以方法仅触发一次的事件

```js
$("table").one("click", "td", function() {
    $(this).toggleClass("click");
});
```

 

#### 2. 动画





## 四、框架

#### 1. MVC和MVVM

**MVC**

![MVC](./img/MVC.png)

- 视图（View）：用户界面，作为视图层，主要负责数据的展示 
- 控制器（Controller）：业务逻辑，控制器是模型和视图之间的纽带，MVC将响应机制封装在controller对象中，当用户和你的应用产生交互时，控制器中的事件触发器就开始工作了。 
- 模型（Model）：数据保存，用于封装和应用程序的业务逻辑相关的数据以及对数据的处理方法 

模型层(Model)最主要做业务数据封装操作。视图层(View)主要发布事件操作及监听模型层上的数据，如果模型层上有数据改变的时候，及时更新页面操作，最后显示给页面上来，控制层(Controller)主要监听视图层(View)的事件，调用模型层(Model)的方法来更新模型上的数据，模型层数据更新后，会发布一条消息出去，最后视图层(View)通过监听模型层(Model)的数据变化，来更新页面的显示; 如上是MVC的基本流程。 



**MVVM**

![MVVM](./img/MVVM.png)

- 视图（View）：用户界面，作为视图层，主要负责数据的展示 
- Viewmodel : 
- 模型（Model）：数据保存，用于封装和应用程序的业务逻辑相关的数据以及对数据的处理方法 

MVVM采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel，反之亦然,model数据的变动，也自动展示给页面显示，把Model和View关联起来的就是ViewModel。ViewModel负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model。

只要改变JavaScript对象的内容，就会导致DOM结构作出对应的变化，这让关注点从如何操作DOM变成了如何改变JavaScript对象的状态。

MVVM的核心思想：关注Model的变化，让MVVM框架利用自己的机制去自动更新DOM，从而把开发者从操作DOM的繁琐中解脱出来！ 

## 五、计算机网络

#### 1. 304状态码

对于304状态码，意思是告诉客户端使用缓存资源即可，因为服务器上的资源没有更新。所以304意味着在获取资源的时候，仍旧会发起一次请求到服务器，服务器确认 If-None-Match 和资源对比，没有发生变化，随即返回客户端一个304响应，告诉客户端使用缓存的资源即可。在这个过程中，并未从服务器携带资源返回，节约了带宽。



#### 2. 从输入URL到页面加载发生了什么？ 

> 1. DNS域名解析 : 获取域名的IP地址
> 2. 根据IP地址建立TCP连接（三次握手） 
> 3. 浏览器向服务器发送HTTP请求 
> 4. 服务器处理请求，浏览器接收HTTP响应
> 5. 渲染页面，构建DOM树
> 6. 关闭TCP连接（四次挥手）



#### 3. 前端性能优化方法

性能黄金法则：只有10%~20%的最终用户响应时间花在了下载HTML文档上。其余的80%~90%时间花在了下载页面中的所有组件上

       	1. 减少HTTP请求：CSS Sprites、合并JS脚本和CSS样式表、使用图片地图和内联图片
       	2. 使用内容发布网络（CDN）：CDN是一组分布在多个不同地理位置的Web服务器，用于更加有效地向用户发布内容
       	3. 添加Expires头
       	4. 压缩组件：gzip压缩
       	5. 使用Link标签将CSS放在顶部：使页面逐步呈现，避免白屏
       	6. 将Js脚本放在底部：因为脚本会阻塞其后页面内容的逐步呈现和其后面组件的并行下载
       	7. 避免CSS表达式：CSS表达式求值频繁，可使用一次性表达式和事件处理器
       	8. 使用外部Js和CSS：Js文件和CSS文件有机会被浏览器缓存起来，而HTML文档通常不会被配置为可以进行缓
       	9. 减少DNS查找
       	10. 精简JavaScript：减少不必要的字符以减小其大小，移除所有注释和不必要的空白字符、
       	11. 精简CSS：合并相同的类、移除不适用的类、使用缩写（"#606"代替"#6600066")、移除不必要字符串（“0”代替“0px“）
       	12. 避免重定向
       	13. 删除重复脚本
       	14. 配置ETag（实体标签）：Web服务器和浏览器用于确认缓存组件有效性的一种机制
       	15. 使Ajax可缓存



#### 4. CDN（Content Distribute Network，内容分发网络 ） 

CDN是将源站内容分发至最接近用户的节点，使用户可就近取得所需内容，提高用户访问的响应速度和成功率。解决因分布、带宽、服务器性能带来的访问延迟问题，适用于站点加速、点播、直播等场景。



CND工作流程：

1.用户向浏览器输入域名，浏览器发现本地没有DNS缓存，则向网站的DNS服务器请求；
2.网站的DNS域名解析器设置了CNAME，请求指向了CDN网络中的智能DNS负载均衡系统；
3.智能DNS负载均衡系统解析域名，根据用户IP地理位置、接入网类型，把对用户响应速度最快的IP节点返回给用户；
4.用户向该IP节点（CDN服务器）发出请求；
5.当缓存中没有目标资源时访问，CDN服务器会向原web站点请求，并缓存内容；当缓存中存在目标资源时，内容将从CDN服务器中返回
6.请求结果发给用户。

## 六、其他

#### 1. git合并冲突解决方法

```git
$ git merge test1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```

发生冲突的时候，需要手动解决冲突后在提交，`git status` 可以告诉我们发生冲突的文件

```git
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

此时查看文件，git会通过`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容 

```git
$ cat readme.txt
Hello World!
Git is a distributed control system.
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> test1
```

`git log --graph`可以图形化展示分支的合并过程

```git
$ git log --graph --oneline
*   dec1e2d (HEAD -> master) conflict fixed
|\
| * 19d9c88 (test1) AND simple
* | 5eb8d49 & simple
|/
* d7a271d add distributed
* c0d1a2a wrote a readme file
```

最后删除`test1`分支

```git
$ git branch -d test1
Deleted branch test1 (was 19d9c88).
```







