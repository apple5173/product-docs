# 资源

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnKOHfF61LEUAcfBGDB0mi1g.png)

## 资源简介

### 资源是什么

```ts
- 编辑器提供给开发者使用的模型、材质、贴图、特效、动作、声音等美术相关素材
```

### 资源的应用场景

```ts
- 主编辑器运行时从本地资源库拖拽至视口或者对象管理器内
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnUKeT5bGPMzo8tsjv4rPPRb.png)

```ts
- 脚本、动态加载调用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnVBcIzW21ImimJerhEO2Yyg.png)

## 资源库使用指南

### 资源库展示

```ts
- 资源库常驻在编辑器主界面左侧
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcntxWyYCUMS8Z4j7uGZ0Kuzc.png)

### 资源库功能说明

```ts
  - 默认状态下，所有美术资源都是未下载状态，需要左键点击下载资源

  - 资源下载需要时间，如果网络状态正常，一个资源需要几秒时间下载

  - 所有资源根据资源类型顺序排列在本地资源库中

  - 资源有主题、风格、分类、标签等信息，方便开发者寻找资源

  - 每种资源使用方式不一样
```

## 资源类型

### 静态模型

```ts
- 没有骨骼信息，不具备播放动画功能的模型资源，例如房屋、砖石、自然景观等
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnsPubTIHILoUMnKvH4gUjWh.png)

### 骨骼模型

```ts
- 带有骨骼信息，开发者可通过脚本等程序方式控制播放动画的模型资源，例如载具、动物、怪物等
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnt69NNic0QowhMhyisfpqrc.png)

### 预制体

```ts
- 预制体是开发者根据设计目的，在编辑器中使用模型、特效、UI、脚本等资源进行组合制作的高级资源，本身可能带有功能，也可能是静态模型组合而成
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnOvVGmTQKdIvJJcOiKVExph.png)

### 材质

```ts
- 材质定义场景中资源的表面属性， 从广义上来讲，可以将材质视为涂在网格体上用来控制其视觉外观的"涂料"。从更偏技术性的角度来讲，材质确切告知渲染引擎一个表面应该如何与场景中的光线交互， 材质定义了表面的每个方面，包括颜色、反射性、崎岖度、透明度等

- 材质不可以单独存在，必须依赖模型，具体表现由搭配的贴图决定
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnvX8s0xug8zYU8SQU3po3ac.png)

### 场景贴图

```ts
- 专门应用于场景物件的贴图资源，具备四方连续的特性，不可用于其他用途

- 场景贴图不可以单独存在，必须依赖材质，贴图和材质合并决定模型表现

- 场景贴图只可拖拽至场景物件中的材质的贴图插槽上使用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnu8odDwuOl1kzIcmZrMXrPh.png)

### UI 贴图

```ts
- 专门应用于UI编辑器的贴图资源，不可用于其他用途

- UI贴图不可以单独存在，必须依赖UI编辑器生产的UI，表现由UI控件决定

- UI贴图只可拖拽至UI编辑器中使用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnQro9586enyIgnwoTrd7RQf.png)

### 天空球贴图

```ts
- 专门应用于世界对象-天空盒的贴图资源，不可用于其他用途

- 天空球贴图不可以单独存在，只可拖拽至天空盒对象中使用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnzXLRHfGQAJNskhseVgPHZd.png)

### 动画姿态

```ts
- 适配编辑器配套骨骼的循环动作资源，比如呼吸站立、攻击待机、射击待机等，依赖角色相关资源

- 当前版本中动画姿态只可通过脚本调用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnZ8GqDe1usK7c5t0w8Oqv7c.png)

### 动画

```ts
- 适配编辑器配套骨骼的单次动作资源，比如劈砍、跳跃、施法等，依赖角色相关资源

- 动画不可以单独存在，只可拖拽至角色编辑器中使用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcn9BfIhJnU7HFWrETjFZCjKh.png)

### 粒子特效

```ts
- 带有粒子系统的特效资源，可以拖拽至场景里使用，也可以通过脚本、预制体等工具与其他资源或者逻辑一起使用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnTZzxSYxbWtZIMyGsfF13Fu.png)

### 音效

```ts
- 声音资源，可以拖拽至场景里使用，也可以通过脚本、预制体等工具与其他资源或者逻辑一起使用
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnBF9ZVVN2KRyYHJGf8zBttc.png)

### 角色换装资源

```ts
- 角色部位资源，可以拖拽至场景里使用，也可以通过脚本、预制体等工具与其他资源或者逻辑一起使用，主要应用在角色编辑器中
```

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcneqXFfLavNnRsdg1mXruhzc.png)
