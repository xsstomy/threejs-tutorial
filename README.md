# threejs-tutorial

从今天 2020年11月27日 开始学习和探索 Three.js 。  


<br>
<div style="display: flex; justify-content: center; align-items: center;">
    <img width="400" src="https://raw.githubusercontent.com/puxiao/notes/master/imgs/wechat.jpg" alt="wechat.jpg" />
    <img width="280" src="https://github.com/puxiao/notes/blob/master/imgs/zsxq.jpg?raw=true alt=" 加入知识星球二维码.jpg" />
</div>


<br>

> 以下内容更新于 2021.04.16

**特别提醒：**

本教程最开始使用的是 r123 版本，但是后来 Three.js  更新到 r125 版后，r125 中做了一些修改，将 Geometry 从核心类( core ) 中移除，转移到了 examples/jsm/deprecated/。

> Geometry 类已被废弃，不建议继续使用

然后使用 BufferGeometry 代替之前的 Geometry。此外还有其他很多地方修改，这就造成本教程一些文章中的示例代码在最新的版本中已经不可用了。

但是文章中讲解的代码思路、原理、用法是不会有太大的差异。

目前最新版本为 r127版本，所以...随着 Three.js 版本不断更新，本教程中的示例代码终会有过时的时候。

对于某个具体的类，Three.js 官方文档都有详细的使用示例，可去官网文档查看最新的用法。

<br>

说一声抱歉：我在写第 25 节文章的时候才彻底理解 左手坐标系统和右手坐标系统，而我在前面章节中有可能讲解坐标体系对应的 上下左右前后 时把方向搞错了，但是我记不清是哪个章节了。

<br>

> 以上内容更新于 2021.04.16



<br>

> 以下内容更新于 2021.05.22



<br>

> 因为本系列暂停了本系列教程的更新，所以就暂时在这里补充上关于 3D 坐标系的相关知识吧。

直角坐标系与球极坐标系：

1. 左右手坐标系统他们都是 直角坐标系，使用 (x,y,z) 来表示空间某个点的坐标，webgl/three.js 采用右手坐标系。

2. 除 右手坐标系 用来确定 xyz 轴朝向外，还有一个 “右手螺旋法则” 用来判定旋转方向。

3. 球极坐标系，又称 空间极坐标，使用 (r,φ,θ) 来表示空间某个点的坐标。

   > Three.js 的球极坐标 对应的类是：Spherical
   >
   > https://threejs.org/docs/index.html#api/zh/math/Spherical

> 只有真正了解 Three.js 的这 2 套坐标系，同时理解 Vector2(二维向量)、Vector3(三维向量)、Raycaster(光线投射)，才有可能晋级为 Three.js 空间高手。



<br>

我在学习的过程中也向 Three.js 官方提交了自己的 PR，贡献出自己一点点力量。

1. PR [21409](https://github.com/mrdoob/three.js/pull/21409) 已获准在 r127 中合并
2. PR  [21642](https://github.com/mrdoob/three.js/pull/21642) 已获准在 r128 中合并
3. PR  [21687](https://github.com/mrdoob/three.js/pull/21687) 已获准在 r128中合并
4. PR  [21729](https://github.com/mrdoob/three.js/pull/21729) 已获准在 r129中合并

Three.js 官方维护人员非常热心和严谨。

几乎每天都有新的 PR 被提交，感觉 Three.js 社区活力满满。



> 以上内容更新于 2021.05.22



<br>


## 我的学习资料

我刚开始学习 three.js，目前主要看 Three.js 官方出的 教程 和文档：

* [threejsfundamentals.org：官方教程](https://threejsfundamentals.org/threejs/lessons/zh_cn/) (该教程只有前几篇是有中文翻译的)
* [threejs.org：官方中文文档](https://threejs.org/docs/index.html#manual/zh/introduction/Creating-a-scene)

除此之外，还有其他几个值得推荐的、国内博主写的 Three.js 系列教程：

* [wjceo.com：暮志未晚写的three.js教程](https://www.wjceo.com/blog/threejs/)

* [hewebgl.com：Three.js基础教程](http://www.hewebgl.com/article/articledir/1)

* [webgl3d.cn：Three.js教程](http://www.webgl3d.cn/Three.js/)

* 强烈推荐看一下 [图解WebGL&Three.js工作原理](https://www.cnblogs.com/wanbo/p/6754066.html)

  > 可惜该作者近几年都没再更新 Three.js 相关文章。

特别说明 hewebgl.com 和 webgl3d.cn 的教程存在问题就是：

1. 教程内容版本有些老化，使用的并不是最新版 three.js
2. 教程基于网页，而不是基于 React，更不是基于 React + TypeScript

但是这两个网站教程作者编写的时候，非常用心，里面讲述的大量关于 Three.js 理论知识是值得反复学习阅读的。

**综上所述**

1. 我会以官方教程(https://threejsfundamentals.org/threejs/lessons/zh_cn/) 为主线。
2. 我会在以上教程、文档，以及我搜集到的其他相关教程基础上，来编写本系列 Three.js 教程。
3. 我会以一个新手的视角，心路历程，来编写本系列 Three.js 教程。



<br>

## Three.js官方文档的补充说明

当 Three.js 每次版本迭代更新时，官方只负责维护 英文版 文档，中文版文档完全是靠网友业余时间友情翻译与维护的。

**这就会造成 中文版文档 落后于 英文版文档。**

比如 r130 版本中 `AxesHelper` 新增加了 `.setColors()` 方法，而此时的中文文档中，还未有人相应增加这个方法。

因此当你想要查找某个 类 的用法时，你应该最优先选择去看 **英文** 的官方文档。

> https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene



<br>

我曾经也翻译过好几处地方，提交 PR 也被并入，但是随着时间的推移，逐渐没有翻译的热情了。

因为实在是太多，更新太频繁，没有那么多精力去搞文档。



<br>

## 关于国内有些Three.js示例中代码过时的补充说明

我加了一些 Three.js 交流QQ群，经常有人在里面发一些问题，处在学习阶段的我，经常会去帮忙看一下。

> 看别人遇到的问题，也特别能够提高自己的一些所见所闻，知识面。

经常发生一些这样的情景：**对方说是照着某个示例敲的代码，可就是运行不起来。**

首先我会去官网文档中，查一下他们代码中用到的 类、属性、方法，但是很多时候根本查不到。

这说明他们用的类，属性，方法已发生变更、修改、废弃等。



<br>

此时，我都会到 Three.js github 官方仓库中，在 `Pull requests` 中搜索该属性或方法。

> https://github.com/mrdoob/three.js/pulls

> 搜索时请注意要把 is:open 删除掉，因为既然都被废弃了，那肯定 PR 已经是被并入过的了，状态肯定是 close，不可能是 open。

通常情况下，都可以检索出和废弃的 类、属性、方法相关 PR 信息，点击查看 PR 详情，就能够找到为什么要废弃，建议以后改用 xxx 之类的信息。

至此，原因和结果都知道了，就很容易修复代码了。



<br>

总结一下，想把 Three.js 搞明白，一定要经常做以下 4 件事：

1. 看 英文/中文 文档
2. 去 Github 仓库看源码
3. 去 `Pull requests` 中看最新或之前的 PR 改动
4. 使用、查看源码过程中，发现可以改进的地方，勇敢、大胆得去提交 PR



<br>

## 相关书籍推荐

事实上，目前我个人并没有购买过任何 Three.js 相关的书籍。

因为我认为最好的 Three.js 书籍就是 最新源码、官方文档、官方示例。

<br>

我购买了很多和 WebGL、3D 图形学相关的书籍。

如果没有 3D 图形学相关知识，那么后期提升 Three.js 会比较困难。



<br>

**推荐的第1本书籍：《3D数学基础：图形和游戏开发(第2版)》**

购买地址：http://product.dangdang.com/28552828.html

这本书系统全面得介绍了 3D 图形学中各个数学概念。

> 笛卡尔坐标系、极坐标系、向量、点乘、叉乘、欧拉角、四元数、矩阵转换... 等等这些概念，你都需要了解，否则你后期根本无法理解和写出 复杂点的 Three.js 交互代码。

> 简直就该人手 1 本

不要被书名中的 数学 二字吓到，书中的数据公式，根本不需要你去记忆。



> 尽量在 当当或京东 做活动时候购买，比如 `5折` 或 `满100减50` 时购买，比较划算。



<br>

**推荐的第2本书籍：《基于WebGL的自顶向下方法(第七版)》**

购买地址：http://product.dangdang.com/23933108.html

这本书系统全面介绍了 基于 webgl 的 3D图形学知识体系。

可以让你在大脑中快速构建出 3D 图形学的渲染概念。

> 注意，是基于 webgl，而不是基于 three.js



<br>

**推荐的第3本书籍：虎书(第4版)**

第四版英文下载地址：

http://index-of.es/z0ro-Repository-2/Cyber/01%20-%20Computer%20Science/Fundamentals%20Of%20Computer%20Graphics%20-%20Peter%20Shirley,%20Steve%20Marschner.pdf

这本书系统全面得介绍了 3D 图形学，这本书是计算机图形学最权威的书籍，没有之一。

> 需要有梯子才可以访问。

> 由于这本书的封面是一只老虎，所以这本书才被称为 “虎书”
>
> 这本书只有第2版有简体中文，不过第2版已经过时，第三版和第四版差别不是太大。



<br>

**其他书籍**

除此之外，我还购买了其他书籍，但是，这些书籍并不属于 强烈推荐 的那种。

> 这些书我个人认为看一下可以，不看也无所谓。
>
> 假设满星为 5 颗星

1. 本人推荐指数 2 颗星：《深入理解OpenGL、WebGL 和 OpenGL ES》
2. 本人推荐指数 1 颗星：《计算机图形学——几何体数据结构》
3. 本人推荐指数 0 颗星：《3D图形系统设计与实现》



<br>

## WebGL相关教程

首先说明一下，如果学想对 Three.js 有更深层次的修炼，那么你一定要去学习一下 WebGL。

> WebGL又分为：WebGL1、WebGL2

Three.js 本身就是针对 WebGL 的封装。

WebGL 教程：https://webglfundamentals.org/webgl/lessons/zh_cn/

WebGL2 教程：https://webgl2fundamentals.org/webgl/lessons/zh_cn/

**假设你不想学习 WebGL 也没有关系，直接学习 Three.js 也是完全没有问题的。**



<br>

## 你还需要掌握的技术栈

* **JS、ES6**
* **CSS、SCSS**
* **React、hooks**
* **TypeScript**
* **包管理工具Yarn 或 NPM**

以上是本系列文章使用的技术栈。

若将来要将开发的项目发布到线上，你可能还需要掌握：

* **Git 代码管理**
* **Koa 创建简单web服务器**
* **Nginx 配置静态服务器**
* **Docker 创建容器服务**



<br>

## 关于3D建模

Three.js 内置了很多基础模型，也支持内部自定义图形。

但是，**建模并不是 Three.js 最核心和擅长的，Three.js 最核心功能是进行 浏览器 3D 场景渲染和交互**。

**因此学习 Three.js 的核心应该放在 渲染和交互 上，而不是建模。**

> 以上纯粹目前个人观点，仅供参考

<br>

#### 传统 3D 软件

多数场景下 3D 建模这个工作还应该在传统的 3D 软件中完成，例如 3D Max、C4D、Blender 等。

虽然 3D 软件各有不同，但是他们导出文件格式标准相同，所以 Three.js 是支持他们所导出的模型的。

因此，若想学好、用好 Three.js，你还需要掌握一门 3D 软件，我个人强烈推荐以下 2 个软件：

**第1推荐(强烈推荐)：C4D**

优点：轻量级 3D 建模软件、支持简体中文、国内中文教程、资源非常多

缺点：软件收费，当然你可以自己网上搜到 ** 版

**第2推荐：Blender**

优点：开源免费、也属于轻量级

缺点：国内使用人群数量较少，教程和资源较少

**对于完全不懂3D软件的人来说，Windows 10 自带的 “画图 3D” 这个软件也是可以的。**

<br>

#### 补充说明

即使在你的项目团队中，有专门的人负责 3D 建模并导出 Three.js 支持的 文件给你使用，我也非常建议你要学习一下 3D 软件。

如果你不曾使用过 3D 软件，那么你会对 Three.js 中的很多概念感到陌生，甚至是无法想象为什么会是这样。

> 例如：场景、网格、材质、灯光 等等。



<br>

## 本教程的缺点

#### 1、是Three.js教程，但不是Three.js文档

我们只是从一个初学者的角度来讲解 Three.js，但是不会讲解每一个讲解对象、每一个类的全部属性或方法，如果想了解某个类的全部属性和方法，建议你直接去看 Three.js 的官方文档。

本教程可以带你入门，但你依然需要不断地查阅官方文档，来弥补本教程中没有提及的属性或方法。

<br>

#### 2、没有配图

无论是相关知识点，纹理、示例运行效果，都没有配图。

没有别的原因，就是因为我懒，打字已经够占用时间了，真的没更多精力去配图。

不过我的每个示例都有详细完整的代码，你只需要复制到本地，实际调试一下就能看到效果。

<br>

#### 3、所有的示例基本上都是独立的，没有抽离出公共的类或组件

在实际的项目中一定会把某些创建过程、处理函数、逻辑进行抽离，单独成为一个类、函数或组件。

但是本系列教程中，为了避免比较绕，每个示例基本上都是完全独立的，包括样式 scss 文件。

这既是优点，也是缺点。

优点是你在查看某个示例时，代码独立而完整。

缺点是由于没有代码抽离，所以代码量会比较多，阅读起来略显麻烦。

> 我只在刚开始的几个示例中添加了代码注释，后面的示例中就因为懒，所以没有添加代码注释。

<br>

#### 4、本文没有讲解图形学相关知识

因为我在写本系列教程时，我自己都未曾学习过图形学，所以肯定无法站在 `图形学或 webgl` 的维度来讲解 three.js。

**即使学完本系列教程，你也只是 Three.js 简单入门。**

因为如果没有图形学知识作为基础，你很难完成复杂点的 Three.js 开发。



<br>

我现在正在学习图形学，只有掌握图形学后，才会更加容易理解 three.js 。

> 尽管我目前也只是学习了图形学一点点基础的东西，但是此刻再回头去看 three.js 中的很多属性和方法，相对容易很多。



<br>

除了本文上面推荐的基本书籍之外，强烈推荐大家观看这个视频。

**闫令琪：现代计算机图形学入门**

https://www.bilibili.com/video/BV1X7411F744



<br>

**大家都是 Three.js 小白新手，一起加油！**
