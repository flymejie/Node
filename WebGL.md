# WebGL 

WebGL是在浏览器中实现三维效果的一套规范。 

## 1、三大组建

在Three.js中，要渲染物体到网页中，我们需要3个组建：场景（scene）、相机（camera）和渲染器（renderer）。有了这三样东西，才能将物体渲染到网页中去。 

```javascript
var scene = new THREE.Scene();  // 场景
var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);// 透视相机
var renderer = new THREE.WebGLRenderer();   // 渲染器
renderer.setSize(window.innerWidth, window.innerHeight);    // 设置渲染器的大小为窗口的内宽度，也就是内容区的宽度
document.body.appendChild(renderer.domElement);

```

**THREE是Three.js引擎的一个全局变量** 

场景是所有物体的容器，如果要显示一个苹果，就需要将苹果对象加入场景中。 

### 2、相机

另一个组建是相机，相机决定了场景中那个角度的景色会显示出来。相机就像人的眼睛一样，人站在不同位置，抬头或者低头都能够看到不同的景色。

场景只有一种，但是相机却又很多种。和现实中一样，不同的相机确定了呈相的各个方面。比如有的相机适合人像，有的相机适合风景，专业的摄影师根据实际用途不一样，选择不同的相机。对程序员来说，只要设置不同的相机参数，就能够让相机产生不一样的效果。

在Threejs中有多种相机，这里介绍两种，它们是：

透视相机（THREE.PerspectiveCamera）、这里我们使用一个透视相机，透视相机的参数很多，这里先不详细讲解。后面关于相机的那一章，我们会花大力气来讲。定义一个相机的代码如下所示：（已经迫不及待想看看相机的参数了，点这里）

[View Raw Code](http://www.hewebgl.com/article/getarticle/50#)[?](http://www.oriontransfer.co.nz/software/jquery-syntax)

```javascript
 var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);

1、跟随位置，摄像机跟随的目标物体的位置
2、跟随的方向，摄像机沿哪个方向移动来跟随物体
3、跟随速度
4、跟随距离，摄像机与物体的距离
```

### 3、渲染器

最后一步就是设置渲染器，渲染器决定了渲染的结果应该画在页面的什么元素上面，并且以怎样的方式来绘制。这里我们定义了一个WebRenderer渲染器，代码如下所示：

```javascript
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

```

注意，渲染器renderer的domElement元素，表示渲染器中的画布，所有的渲染都是画在domElement上的，所以这里的appendChild表示将这个domElement挂接在body下面，这样渲染的结果就能够在页面中显示了。 

有两种渲染器 ：

var  renderer=new THREE.CanvasRenderer();     几何级别的渲染，兼容性更好

var renderer=new THREE.WebGLRenderer();       像素级的渲染，渲染效果更好

默认的渲染背景色为黑色

可以通过以下方式改变背景色：

```
	renderer.setClearColor('rgb(135,206,250)',1.0);
	renderer.setClearColor(0xffffff,1.0);
	renderer.setClearColor('#428bca',1.0);
	renderer.setClearColor('rgba(135,206,250,0.5)',1.0);
```



### 4、添加物体到场景中

那现在，我们将一个物体添加到场景中：

```javascript
var geometry = new THREE.CubeGeometry(1,1,1); //物体形状
var material = new THREE.MeshBasicMaterial({color: 0x00ff00});
var cube = new THREE.Mesh(geometry, material); 
scene.add(cube);
```

代码中出现了THREE.CubeGeometry，THREE.CubeGeometry是什么东东，他是一个几何体，几何体由什么组成，已经不是本课的主要内容了，后面的课程我们会详细的学到。不过这里你只需要知道CubeGeometry是一个正方体或者长方体，究竟是什么，由它的3个参数所决定，cubeGeometry的原型如下代码所示：

```javascript
CubeGeometry(width, height, depth, segmentsWidth, segmentsHeight, segmentsDepth, materials, sides)

```



width：立方体x轴的长度

height：立方体y轴的长度

depth：立方体z轴的深度，也就是长度

想一想大家就明白，以上3个参数就能够确定一个立方体。

剩下的几个参数就要费解和复杂一些了，不过后面我们会自己来写一个立方体，到时候，你会更明白这些参数的意义，这里你可以将这些参数省略

### 5、渲染

终于到了最后一步，这一步做完后，就可以该干嘛干嘛去了。

渲染应该使用渲染器，结合相机和场景来得到结果画面。实现这个功能的函数是

renderer.render(scene, camera);

渲染函数的原型如下：

render( scene, camera, renderTarget, forceClear )

各个参数的意义是：

scene：前面定义的场景

camera：前面定义的相机

renderTarget：渲染的目标，默认是渲染到前面定义的render变量中

forceClear：每次绘制之前都将画布的内容给清除，即使自动清除标志autoClear为false，也会清除。

### 6、渲染循环

渲染有两种方式：实时渲染和离线渲染 。

先看看离线渲染，想想《西游降魔篇》中最后的佛主，他肯定不是真的，是电脑渲染出来的，其画面质量是很高的，它是事先渲染好一帧一帧的图片，然后再把图片拼接成电影的。这就是离线渲染。如果不事先处理好一帧一帧的图片，那么电影播放得会很卡。CPU和GPU根本没有能力在播放的时候渲染出这种高质量的图片。

实时渲染：就是需要不停的对画面进行渲染，即使画面中什么也没有改变，也需要重新渲染。下面就是一个渲染循环：

```javascript
function render() {
    cube.rotation.x += 0.1;
    cube.rotation.y += 0.1;
    renderer.render(scene, camera);
    requestAnimationFrame(render);
}
```

其中一个重要的函数是requestAnimationFrame，这个函数就是让浏览器去执行一次参数中的函数，这样通过上面render中调用requestAnimationFrame()函数，requestAnimationFrame()函数又让rander()再执行一次，就形成了我们通常所说的游戏循环了。 

## 1、场景，相机，渲染器之间的关系

Three.js中的场景是一个物体的容器，开发者可以将需要的角色放入场景中，例如苹果，葡萄。同时，角色自身也管理着其在场景中的位置。

相机的作用就是面对场景，在场景中取一个合适的景，把它拍下来。

渲染器的作用就是将相机拍摄下来的图片，放到浏览器中去显示。他们三者的关系如下图所示：

![img](http://www.hewebgl.com/attached/image/20130810/20130810150021_257.jpg)

## 2 . 第二个框架（重构）

第一个框架是将所有代码在一段脚本中完成，当逻辑复杂一点后，就比较难读懂。所以，我们将其按照功能分解成函数，代码如下

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Three框架</title>
        <script src="js/Three.js" data-ke-src="js/Three.js"></script>
        <style type="text/css">
            div#canvas-frame {
                border: none;
                cursor: pointer;
                width: 100%;
                height: 600px;
                background-color: #EEEEEE;
            }

        </style>
        <script>
            var renderer;
            function initThree() {
                width = document.getElementById('canvas-frame').clientWidth;
                height = document.getElementById('canvas-frame').clientHeight;
                renderer = new THREE.WebGLRenderer({
                    antialias : true
                });
                renderer.setSize(width, height);
                document.getElementById('canvas-frame').appendChild(renderer.domElement);
                renderer.setClearColor(0xFFFFFF, 1.0);
            }

            var camera;
            function initCamera() {
                camera = new THREE.PerspectiveCamera(45, width / height, 1, 10000);
                camera.position.x = 0;
                camera.position.y = 1000;
                camera.position.z = 0;
                camera.up.x = 0;
                camera.up.y = 0;
                camera.up.z = 1;
                camera.lookAt({
                    x : 0,
                    y : 0,
                    z : 0
                });
            }

            var scene;
            function initScene() {
                scene = new THREE.Scene();
            }

            var light;
            function initLight() {
                light = new THREE.DirectionalLight(0xFF0000, 1.0, 0);
                light.position.set(100, 100, 200);
                scene.add(light);
            }

            var cube;
            function initObject() {

                var geometry = new THREE.Geometry();
                var material = new THREE.LineBasicMaterial( { vertexColors: THREE.VertexColors} );
                var color1 = new THREE.Color( 0x444444 ), color2 = new THREE.Color( 0xFF0000 );

                // 线的材质可以由2点的颜色决定
                var p1 = new THREE.Vector3( -100, 0, 100 );
                var p2 = new THREE.Vector3(  100, 0, -100 );
                geometry.vertices.push(p1);
                geometry.vertices.push(p2);
                geometry.colors.push( color1, color2 );

                var line = new THREE.Line( geometry, material, THREE.LinePieces );
                scene.add(line);
            }
            function render()
            {
                renderer.clear();
                renderer.render(scene, camera);
                requestAnimationFrame(render);
            }
            function threeStart() {
                initThree();
                initCamera();
                initScene();
                initLight();
                initObject();
                render();
            }

        </script>
    </head>

    <body onload="threeStart();">
        <div id="canvas-frame"></div>
    </body>
</html>
```

### 2、在Threejs中定义一个点

在三维空间中的某一个点可以用一个坐标点来表示。一个坐标点由x,y,z三个分量构成。在three.js中，点可以在右手坐标系中表示：

空间几何中，点可以用一个向量来表示，在Three.js中也是用一个向量来表示的，代码如下所示：

```javascript
THREE.Vector3 = function ( x, y, z ) {

this.x = x || 0;
this.y = y || 0;
this.z = z || 0;
};
```

**THREE.Vector3  表示Vector3是定义在THREE下面的一个类** 

THREE.Vector3被赋值为一个函数。这个函数有3个参数，分别代表x坐标，y坐标和z坐标的分量。函数体内的代码将他们分别赋值给成员变量x，y，z。看看上面的代码，中间使用了一个“||”（或）运算符，就是当x=null或者undefine时，this.x的值应该取0。 

### 点的操作

在3D世界中点可以用THREE.Vector3D来表示。对应源码为/src/math/Vector3.js（注意：源码所在的位置，可能不同版本不一样，请自己搜索Vector3关键词来确定）。在您继续学习之前，你可以打开该文件浏览一下，推荐使用WebStorm，如果没有，你也可以用NotePad++。

现在来看看怎么定义个点，假设有一个点x=4，y=8，z=9。你可以这样定义它：

var point1 = new THREE.Vecotr3(4,8,9);

另外你也可以使用set方法，代码如下：

var point1 = new THREE.Vector3();

point1.set(4,8,9);

## 实例：画一条彩色线

初中数学中有一个定理：两个不重合的点能够决定一条直线。在three.js中，也可以通过定义两个点，来画一条直线。我们先看看，这一节，我们要完成实例的效果图：![img](http://www.hewebgl.com/attached/image/20130515/20130515133907_86.png)

这个例子的代码如下所示 

```htm;
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Three框架</title>
        <script src="js/Three.js"></script>
        <style type="text/css">
            div#canvas-frame {
                border: none;
                cursor: pointer;
                width: 100%;
                height: 600px;
                background-color: #EEEEEE;
            }

        </style>
        <script>
            var renderer;
            function initThree() {
                width = document.getElementById('canvas-frame').clientWidth;
                height = document.getElementById('canvas-frame').clientHeight;
                renderer = new THREE.WebGLRenderer({
                    antialias : true
                });
                renderer.setSize(width, height);
                document.getElementById('canvas-frame').appendChild(renderer.domElement);
                renderer.setClearColor(0xFFFFFF, 1.0);
            }

            var camera;
            function initCamera() {
                camera = new THREE.PerspectiveCamera(45, width / height, 1, 10000);
                camera.position.x = 0;
                camera.position.y = 1000;
                camera.position.z = 0;
                camera.up.x = 0;
                camera.up.y = 0;
                camera.up.z = 1;
                camera.lookAt({
                    x : 0,
                    y : 0,
                    z : 0
                });
            }

            var scene;
            function initScene() {
                scene = new THREE.Scene();
            }

            var light;
            function initLight() {
                light = new THREE.DirectionalLight(0xFF0000, 1.0, 0);
                light.position.set(100, 100, 200);
                scene.add(light);
            }

            var cube;
            function initObject() {

                var geometry = new THREE.Geometry();
                var material = new THREE.LineBasicMaterial( { vertexColors: true } );
                var color1 = new THREE.Color( 0x444444 ), color2 = new THREE.Color( 0xFF0000 );

                // 线的材质可以由2点的颜色决定
                var p1 = new THREE.Vector3( -100, 0, 100 );
                var p2 = new THREE.Vector3(  100, 0, -100 );
                geometry.vertices.push(p1);
                geometry.vertices.push(p2);
                geometry.colors.push( color1, color2 );

                var line = new THREE.Line( geometry, material, THREE.LinePieces );
                scene.add(line);
            }

            function threeStart() {
                initThree();
                initCamera();
                initScene();
                initLight();
                initObject();
                renderer.clear();
                renderer.render(scene, camera);
            }

        </script>
    </head>

    <body onload="threeStart();">
        <div id="canvas-frame"></div>
    </body>
</html>
```

看看A begin 和A end之间的代码，就是画线的代码。 

### 1、首先，我们声明了一个几何体geometry，如下：

var geometry = new THREE.Geometry();

几何体里面有一个vertices变量，可以用来存放点。

### 2、定义一种线条的材质，使用THREE.LineBasicMaterial类型来定义，它接受一个集合作为参数，其原型如下：

LineBasicMaterial( parameters )

Parameters是一个定义材质外观的对象，它包含多个属性来定义材质，这些属性是：

Color：线条的颜色，用16进制来表示，默认的颜色是白色。

Linewidth：线条的宽度，默认时候1个单位宽度。

Linecap：线条两端的外观，默认是圆角端点，当线条较粗的时候才看得出效果，如果线条很细，那么你几乎看不出效果了。

Linejoin：两个线条的连接点处的外观，默认是“round”，表示圆角。

VertexColors：定义线条材质是否使用顶点颜色，这是一个boolean值。意思是，线条各部分的颜色会根据顶点的颜色来进行插值。（如果关于插值不是很明白，可以QQ问我，QQ在前言中你一定能够找到，嘿嘿，虽然没有明确写出）。

Fog：定义材质的颜色是否受全局雾效的影响。

好了，介绍完这些参数，你可以试一试了，在课后，我们会展示不同同学的杰出作品。下面，接着上面的讲，我们这里使用了顶点颜色vertexColors: THREE.VertexColors，就是线条的颜色会根据顶点来计算。

var material = new THREE.LineBasicMaterial( { vertexColors: THREE.VertexColors } );

### 3、接下来，定义两种颜色，分别表示线条两个端点的颜色，如下所示：

var color1 = new THREE.Color( 0x444444 ),

color2 = new THREE.Color( 0xFF0000 );

### 4、定义2个顶点的位置，并放到geometry中，代码如下：

var p1 = new THREE.Vector3( -100, 0, 100 );

var p2 = new THREE.Vector3( 100, 0, -100 );

geometry.vertices.push(p1);

geometry.vertices.push(p2);

### 5、为4中定义的2个顶点，设置不同的颜色，代码如下所示：

geometry.colors.push( color1, color2 );

geometry中colors表示顶点的颜色，必须材质中vertexColors等于THREE.VertexColors 时，颜色才有效，如果vertexColors等于THREE.NoColors时，颜色就没有效果了。那么就会去取材质中color的值，这个很重要，大家一定记住。

### 6、定义一条线

定义线条，使用THREE.Line类，代码如下所示：

var line = new THREE.Line( geometry, material, THREE.LinePieces );

第一个参数是几何体geometry，里面包含了2个顶点和顶点的颜色。第二个参数是线条的材质，或者是线条的属性，表示线条以哪种方式取色。第三个参数是一组点的连接方式，我们会在后面详细讲解。

然后，将这条线加入到场景中，代码如下：

scene.add(line);

这样，场景中就会出现刚才的那条线段了

**在Threejs中，坐标和右边的坐标完全一样。x轴正方向向右，y轴正方向向上，z轴由屏幕从里向外。 **

## 线条的深入理解

**在Threejs中，一条线由点，材质和颜色组成。**

点由THREE.Vector3表示，Threejs中没有提供单独画点的函数，它必须被放到一个THREE.Geometry形状中，这个结构中包含一个数组vertices，这个vertices就是存放无数的点（THREE.Vector3）的数组。这个表示可以如下图所示：![three.js向量](http://www.hewebgl.com/attached/image/20130515/20130515135032_174.png)

为了绘制一条直线，首先我们需要定义两个点，如下代码所示：

var p1 = new THREE.Vector3( -100, 0, 100 );

var p2 = new THREE.Vector3( 100, 0, -100 );

请大家思考一下，这两个点在坐标系的什么位置，然后我们声明一个THREE.Geometry，并把点加进入，代码如下所示：

var geometry = new THREE.Geometry();

geometry.vertices.push(p1);

geometry.vertices.push(p2);

geometry.vertices的能够使用push方法，是因为geometry.vertices是一个数组。这样geometry 中就有了2个点了。

然后我们需要给线加一种材质，可以使用专为线准备的材质，THREE.LineBasicMaterial。

最终我们通过THREE.Line绘制了一条线，如下代码所示:

var line = new THREE.Line( geometry, material, THREE.LinePieces );

ok，line就是我们要的线条了。