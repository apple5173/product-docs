# 空锚点

**阅读本文预计 5 分钟**

使用【空锚点】来解决场景搭建和对象挂载中由于对象的锚点固定导致根据锚点进行的旋转，缩放无法满足需求的情况。

## 空锚点对象

通常情况下资源库中的对象锚点都是固定的，而以锚点为基础执行对象变换经常不满足需求。【空锚点】提供用户去自定义对象锚点位置的功能，利用【空锚点】对象本身作为对象的锚点来使用。而且通过**自动居中，顶点吸附和手动偏移**3 种偏移方式，提升【空锚点】作为父对象时在编辑状态下的操作便捷性。【空锚点】在工程内作为父对象存在时，【场景】内显示所有子对象所产生的的包围盒。你可以在【本地资源库】中的【游戏功能对象】栏中找到【空锚点】。

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcn48mTUDmOIKT5WW7ZB1wpgg.png)

## 创建空锚点

### 通过放置资源创建：

【空锚点】对象本身作为一个游戏对象可以存在于游戏场景中。你可以从【本地资源库】中将【空锚点】拖入【场景】或者【对象管理器】来自动生成一个【空锚点】对象。

1. 在【本地资源库】中找到【空锚点】

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcn2fAXn0y7xK0SlEaAgpTZJd.png)

1. 将对象拖入到【场景】中或者【对象管理器】下

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnP6Skc3UPbkT1Tfsjsiy6hg.png)

1. 在右侧【对象管理器】中【对象】栏找到对应的【初生点对象】并自定义锚点变换和锚点偏移。

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcni3LZHnvclYcg5IrbJwZXUh.png)

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnlL9anQjc19eOygoNeka8gA.png)

### 通过脚本创建：

通过脚本你也可以在游戏运行时通过【资源库】中的资源 ID 使用 `asyncSpawn` 接口动态生成一个【空锚点】对象来使用。【空锚点】的资源 ID 为“Anchor”。在【工程内容】下的脚本目录中新建一个脚本文件，将脚本拖入【对象管理器】中【对象】栏。选中脚本进行编辑，将下列示例代码替换脚本中的 `onStart` 方法：异步生成一个【空锚点】对象，打开双端同步，位置为默认（0，0，0），旋转为默认（0，0，0），缩放倍数为默认（1，1，1）。打印生成【初生点】对象的 guid。

```ts
protected async onStart(): Promise<void> {
    if(SystemUtil.isServer()) {
        let anchor = await Core.GameObject.asyncSpawn({guid: "Anchor", replicates: true}) as Gameplay.PlayerStart;
        console.log("anchor guid " + anchor.guid);
    }
}
```

此处我们也可以通过 `spawn` 接口生成，但是需要将【空锚点】拖入【优先加载栏】或者将【空锚点】进行【预加载】来保证生成后我们不需要等待资源下载而导致后续代码失效。

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnhjRiPOleEHS9tRriYHuWab.png)

```ts
// 预加载资源，将下列代码粘贴到脚本中的onStart方法之前
@Core.Property()
preloadAssets: string = "Anchor"；
```

设定锚点偏移并不会改变【空锚点】对象实际的 Transform 值。但是锚点偏移会影响执行变换时【空锚点】对象的枢轴点。

## 自定义空锚点偏移

【空锚点】对象的偏移将决定执行变换时【空锚点】对象的枢轴点。

**居中**：执行变换时以子对象包围盒的中心作为枢轴点进行移动，旋转，缩放。

**顶点**：执行变换时以子对象包围盒的顶点作为枢轴点进行移动，旋转，缩放。

**自定义偏移**：执行变换时以【空锚点】偏移后位置作为枢轴点进行移动，旋转，缩放。

## 使用空锚点

锚点偏移只作用于编辑态，运行态【空锚点】执行变换时仍然以自身实际值为准。在代码中空锚点只有普通父对象的作用。

### 获取空锚点对象

#### 【对象管理器】中【对象】栏下的【初生点对象】：

**使用****asyncFind****接口通过【初生点对象】的 GUID 去获取：**

1. 选中【空锚点】对象后右键点击【复制对象 ID】获取它的 GUID。注意区分对象 ID 与资源 ID 的区别。

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnEJB10niCEqQ5KHUtrtjw0c.png)

1. 将【属性面板】中【基础属性】类中的【静态状态】取消勾选，静态对象不执行脚本逻辑。

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnsjxYBbzeCmqEoYqy9kiFRf.png)

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnP4ohpf4AuMXgsx0NKXiPsg.png)

1. 在脚本的 onStart 方法中添加下列代码：代码将异步查找 ID 对应的对象并以【空锚点】对象进行接收。

```ts
if(SystemUtil.isServer()) {
    let anchor = await Core.GameObject.asyncFind("3819014E") as Gameplay.Anchor;
    console.log("anchor guid " + anchor .guid);
}
```

**使用脚本挂载的方式进行获取：**

1. 选中【空锚点】对象，在属性面板中将静态状态取消

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnXXtQ6WHL9ojiLOxa5kzlyc.png)

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnnkAu7tpGE82al946ls561e.png)

1. 将脚本挂载到【空锚点】对象下方

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnd3vwPiWtnHQ8OHfcs5fILh.png)

1. 在脚本的 onStart 方法中添加下列代码：代码获取脚本挂载的对象并以【空锚点】对象进行接收

```ts
let anchor = this.gameObject as Gameplay.Anchor ;
```

#### 动态生成的【初生点对象】：

下列示例代码替换脚本中的 `onStart` 方法：示例代码在客户端往 `asyncSpawn` 接口（中传入【空锚点】的资源 ID“Anchor”异步生成了一个对应的【空锚点】对象。

```ts
protected async onStart(): Promise<void> {
    if(SystemUtil.isServer()) {
        let anchor = await Core.GameObject.asyncSpawn({guid: "Anchor", replicates: true}) as Gameplay.PlayerStart;
        console.log("anchor guid " + anchor.guid);
    }
}
```
