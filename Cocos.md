# Cocos 

## 项目结构

```
ProjectName（项目文件夹）
├──assets 
├──library
├──local
├──settings
├──temp
└──project.json

资源文件夹（assets）
assets 将会用来放置您游戏中所有本地资源、脚本和第三方库文件。只有在 assets 目录下的内容才能显示在 资源管理器 中。assets 中的每个文件在导入项目后都会生成一个相同名字的 .meta 文件，用于存储该文件作为资源导入后的信息和与其他资源的关联。一些第三方工具生成的工程或设计原文件，如 TexturePacker 的 .tps 文件，或 Photoshop 的 .psd 文件，可以选择放在 assets 外面来管理。

资源库（library）
library 是将 assets 中的资源导入后生成的，在这里文件的结构和资源的格式将被处理成最终游戏发布时需要的形式。如果您使用版本控制系统管理您的项目，这个文件夹是不需要进入版本控制的。
当 library 丢失或损坏的时候，只要删除整个 library 文件夹再打开项目，就会重新生成资源库。

本地设置（local）
local 文件夹中包含该项目的本地设置，包括编辑器面板布局，窗口大小，位置等信息。您不需要关心这里的内容，只要按照您的习惯设置编辑器布局，这些就会自动保存在这个文件夹。一般 local 也不需要进入版本控制。

项目设置（settings）
settings 里保存项目相关的设置，如 构建发布 菜单里的包名、场景和平台选择等。这些设置需要和项目一起进行版本控制。

project.json
project.json 文件和 assets 文件夹一起，作为验证 Cocos Creator 项目合法性的标志。只有包括了这两个内容的文件夹才能作为 Cocos Creator 项目打开。而 project.json 本身目前只用来规定当前使用的引擎类型和插件存储位置，不需要用户关心其内容。
这个文件也应该纳入版本控制。

构建目标（build）
在使用主菜单中的 项目->构建发布... 使用默认发布路径发布项目后，编辑器会在项目路径下创建 build 目录，并存放所有目标平台的构建工程。由于每次发布项目后资源 id 可能会变化，而且构建原生工程时体积很大，所以此目录建议不进入版本控制。
```



## 声明类型

```
常用参数
default: 设置属性的默认值，这个默认值仅在组件第一次添加到节点上时才会用到
type: 限定属性的数据类型，详见 CCClass 进阶参考：type 参数
visible: 设为 false 则不在 属性检查器 面板中显示该属性
serializable: 设为 false 则不序列化（保存）该属性
displayName: 在 属性检查器 面板中显示成指定名字
tooltip: 在 属性检查器 面板中添加属性的 Tooltip
```

## 属性参数

### 属性检查器相关参数

| 参数名      | 说明                                       | 类型             | 默认值    | 备注                                                         |
| ----------- | ------------------------------------------ | ---------------- | --------- | ------------------------------------------------------------ |
| type        | 限定属性的数据类型                         | (Any)            | undefined | 详见 [type 参数](http://docs.cocos.com/creator/manual/zh/scripting/reference/class.html#type) |
| visible     | 在 **属性检视器** 面板中显示或隐藏         | boolean          | (注1)     | 详见 [visible 参数](http://docs.cocos.com/creator/manual/zh/scripting/reference/class.html#visible) |
| displayName | 在 **属性检视器** 面板中显示为另一个名字   | string           | undefined |                                                              |
| tooltip     | 在 **属性检视器** 面板中添加属性的 Tooltip | string           | undefined |                                                              |
| multiline   | 在 **属性检视器** 面板中使用多行文本框     | boolean          | false     |                                                              |
| readonly    | 在 **属性检视器** 面板中只读               | boolean          | false     |                                                              |
| min         | 限定数值在编辑器中输入的最小值             | number           | undefined |                                                              |
| max         | 限定数值在编辑器中输入的最大值             | number           | undefined |                                                              |
| step        | 指定数值在编辑器中调节的步长               | number           | undefined |                                                              |
| range       | 一次性设置 min, max, step                  | [min, max, step] | undefined | step 值可选                                                  |
| slide       | 在 **属性检视器** 面板中显示为滑动条       | boolean          | false     |                                                              |

### 序列化相关参数

这些参数不能用于 get 方法

| 参数名               | 说明                       | 类型    | 默认值    | 备注                                                         |
| -------------------- | -------------------------- | ------- | --------- | ------------------------------------------------------------ |
| serializable         | 序列化该属性               | boolean | true      | 详见 [serializable 参数](http://docs.cocos.com/creator/manual/zh/scripting/reference/class.html#serializable) |
| formerlySerializedAs | 指定之前序列化所用的字段名 | string  | undefined | 重命名属性时，声明这个参数来兼容之前序列化的数据             |
| editorOnly           | 在导出项目前剔除该属性     | boolean | false     |                                                              |

### 其它参数

| 参数名     | 说明                                  | 类型                                        | 默认值    | 备注                                                         |
| ---------- | ------------------------------------- | ------------------------------------------- | --------- | ------------------------------------------------------------ |
| default    | 定义属性的默认值                      | (Any)                                       | undefined | 详见 [default 参数](http://docs.cocos.com/creator/manual/zh/scripting/reference/class.html#default) |
| url        | 该属性为指定资源的 url                | `function`  (继承自 cc.RawAsset 的构造函数) | undefined | 详见 [获取和加载资源: Raw Asset](http://docs.cocos.com/creator/manual/zh/scripting/load-assets.html#raw-asset) |
| notify     | 当属性被赋值时触发指定方法            | `function (oldValue) {}`                    | undefined | 需要定义 default 属性并且不能用于数组 不支持 ES6 定义方式    |
| override   | 当重写父类属性时需要定义该参数为 true | boolean                                     | false     | 详见 [override 参数](http://docs.cocos.com/creator/manual/zh/scripting/reference/class.html#override) |
| animatable | 该属性是否能被动画修改                | boolean                                     | true      |                                                              |

 ## 访问节点和组件

你可以在 **属性检查器** 里修改节点和组件，也能在脚本中动态修改。动态修改的好处是能够在一段时间内连续地修改属性、过渡属性，实现渐变效果。脚本还能够响应玩家输入，能够修改、创建和销毁节点或组件，实现各种各样的游戏逻辑。要实现这些效果，你需要先在脚本中获得你要修改的节点或组件。 

## 获得组件所在的节点

获得组件所在的节点很简单，只要在组件方法里访问 `this.node` 变量：

```
    start: function () {
        var node = this.node;
        node.x = 100;
    }
```

## 基本图像渲染

### Sprite 组件参考

Sprite（精灵）是 2D 游戏中最常见的显示图像的方式，在节点上添加 Sprite 组件，就可以在场景中显示项目资源中的图片。 ![add sprite](http://docs.cocos.com/creator/manual/zh/components/sprite/sprite_component.png)

### Sprite 属性

| 属性             | 功能说明                                                     |
| ---------------- | ------------------------------------------------------------ |
| Atlas            | Sprite 显示图片资源所属的 [Atlas 图集资源](http://docs.cocos.com/creator/manual/zh/asset-workflow/atlas.html) |
| Sprite Frame     | 渲染 Sprite 使用的 [SpriteFrame 图片资源](http://docs.cocos.com/creator/manual/zh/asset-workflow/sprite.html) |
| Type             | 渲染模式，包括普通（Simple）、九宫格（Sliced）、平铺（Tiled）和填充（Filled）渲染四种模式 |
| Size Mode        | 指定 Sprite 的尺寸，`Trimmed` 会使用原始图片资源裁剪透明像素后的尺寸；`Raw` 会使用原始图片未经裁剪的尺寸；当用户手动修改过 `size` 属性后，`Size Mode` 会被自动设置为 `Custom`，除非再次指定为前两种尺寸。 |
| Trimmed Mode     | 是否渲染原始图像周围的透明像素区域，详情请参考[图像资源的自动剪裁](http://docs.cocos.com/creator/manual/zh/asset-workflow/trim.html)。 |
| Src Blend Factor | 当前图像混合模式                                             |
| Dst Blend Factor | 背景图像混合模式，和上面的属性共同作用，可以将前景和背景 Sprite 用不同的方式混合渲染，效果预览可以参考 [glBlendFunc Tool](http://www.andersriggelsen.dk/glblendfunc.php) |

添加 Sprite 组件之后，通过从 **资源管理器** 中拖拽 Texture 或 SpriteFrame 类型的资源到`Sprite Frame`属性引用中，就可以通过 Sprite 组件显示资源图像。