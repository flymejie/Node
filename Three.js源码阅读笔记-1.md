# [Three.js源码阅读笔记-1](https://www.cnblogs.com/yiyezhai/archive/2012/11/29/2791319.html)

 Three.js是一个比较伟大的webgl开源库，它简化了浏览器3D编程，使得使用JavaScript在浏览器中创建复杂的场景变得容易很多。Github上众多webgl demo令我兴奋不已，跃跃欲试。由于这个库还处在开发阶段，因此资料非常匮乏，爱好者大部分时间不得不通过阅读该库的源码进行学习，我现在也准备这样做。

这是第一篇笔记，先从最基础的核心（Core）对象开始。

## Core::Vector2

该构造函数用来创建一个表示二维向量的对象

```
THREE.Vector2 = function ( x, y ) {
    this.x = x || 0;
    this.y = y || 0;
};
```

Vector2对象的功能函数采用定义构造函数的原型对象来实现，形如：

```
THREE.Vector2.prototype = {
    constructor: THREE.Vector2,
    set: function ( x, y ) {
        this.x = x;
        this.y = y;
        return this;
    },
    copy: function ( v ) {
        this.x = v.x;
        this.y = v.y;
        return this;
    },
        ...... // 更多的函数
};
```

- 函数set(x,y)用以指定向量的值，调用者本身的x，y值被影响了，而该方法本身又返回调用者本身，这种情况很常见，以下不再说明。通过文字能够表述清楚功能的函数不再引用源代码，这一点以下也不再说明。

- 函数copy(v)用来将向量v复制进调用者。

- 函数add(a,b)和函数sub(a,b)分别表示对向量a，b相加和相减。

- 函数addSelf(v)和subSelf(v)分别表示对调用者本身加上或减去向量v。

- 函数multiplyScale(s)和divideScale(s)分别表示对调用者本身乘以或除以s。

- 函数lerpSelf(v,alpha)将调用者向v所指的方向旋转alpha，当alpha为1时，调用者最终等于v，而当alpha=0时，调用者还等于原来。

  ```
  lerpSelf: function ( v, alpha ) {
          this.x += ( v.x - this.x ) * alpha;
          this.y += ( v.y - this.y ) * alpha;
          return this;
      },
  ```

- 函数negate()对调用者取反。

- 函数dot(v)返回float类型的调用者和向量v的点乘。

- 函数lengthSq()和函数length()返回float类型的调用者长度平方或长度。

- 函数normalize()将调用者本身归一化。

- 函数distanceToSquared(v)和distanceTo(v)将返回调用者和向量v的距离。这里的距离其实是两向量起点都在原点时，终点之间的距离，也就是向量this-v的长度。

- 函数setLength(s)将向量的长度缩放至为s，方向不变。

- 函数equals(v)判断调用者与向量v的值是否相同。

- 函数isZero()判断调用者是否是零向量。

- 函数clone()返回一个与调用者值一样的新向量，相当于将其复制出去，注意与copy(v)的区别。

## Core::Vector3

该构造函数创建一个表示三维向量的对象

```
THREE.Vector3 = function ( x, y, z ) {
    this.x = x || 0;
    this.y = y || 0;
    this.z = z || 0;
};
```

三维向量和二维向量有许多共通之处，比如set，add，dot，length，clone等，此处尽数略去，只记录三维向量比二维向量多出的部分函数。

- 函数setX(x)，setY(y)和setZ(z)用来单独设置某一分量的值。
- 函数cross(a,b)和crossSelf(v)分别使调用者变为a，b的叉乘或者调用者本身与v的叉乘。叉乘是一个向量，垂直于参与叉乘的两个向量并呈右手螺旋法则。
- 函数getPositionFromMatrix(m)，getRotationFromMatrix(m)，getScaleFromMatrix(m)从4×4的模型矩阵中提取位置分量，旋转分量和缩放分量。模型矩阵表示了一系列平移、旋转、缩放变换的叠加效果。（这里第二个函数出现在文档中，在源码中被另外两个函数代替了，也许还没来得及更新）。
- 函数angleTo(v)计算调用者和向量v的夹角。

## Core::Vector4

该构造函数创建一个表示四维向量的对象

```
THREE.Vector4 = function ( x, y, z, w ) {
    this.x = x || 0;
    this.y = y || 0;
    this.z = z || 0;
    this.w = ( w !== undefined ) ? w : 1;
};
```

四维向量用来表示齐次坐标，其函数和Vector2，Vector3中的函数功能重合，仅仅是多一个分量而已，这里不再记录。

## Core::Matrix3

该构造函数创建一个表示3×3矩阵的对象

```
THREE.Matrix3 = function () {
    this.elements = new Float32Array(9);
};
```

 3×3矩阵有9个元素，存储在矩阵对象的属性elements中，elements是一个数组。

- 函数getInverse(m)返回矩阵m的逆矩阵，同时改变调用者本身。
- 函数transpose()转置调用者。
- 函数transposeToArray(r)将调用者转置进数组r而不改变自身。（这个地方似乎源码错了，var m=this.m应该为var m=this.elements。）

## Core::Matrix4

该构造函数创建一个表示4×4矩阵的对象，4×4矩阵在三维图形学中非常重要，模型矩阵、视图矩阵和投影矩阵都是这样的矩阵。

```
THREE.Matrix4 = function ( n11, n12, n13, n14, n21, n22, n23, n24, n31, n32, n33, n34, n41, n42, n43, n44 ) {
    this.elements = new Float32Array( 16 );
    this.set(
        ( n11 !== undefined ) ? n11 : 1, n12 || 0, n13 || 0, n14 || 0,
        n21 || 0, ( n22 !== undefined ) ? n22 : 1, n23 || 0, n24 || 0,
        n31 || 0, n32 || 0, ( n33 !== undefined ) ? n33 : 1, n34 || 0,
        n41 || 0, n42 || 0, n43 || 0, ( n44 !== undefined ) ? n44 : 1
    );
};
```

在Matrix3对象中出现的几个函数在Matrix4中有相同的作用，这里也略去。

-  函数identity()将对象重置为单位阵。

-  函数lookAt(eye,center,up)将对象设定为一个视图矩阵，参数都是Vector3对象，该矩阵只会用到eye和center的相对位置。该视图矩阵表示，摄像机在eye位置看向center位置，且向上的向量（这一点稍后解释）为up时的视图矩阵。视图矩阵又可以看做摄像机的模型矩阵，所以该函数产生的矩阵又可以表示以下变换：将物体从原点平移至位置center-eye，再将其旋转至向上的向量为up。向上的向量up用来固定相机，可以想象当相机固定在一点，镜头朝向固定方向的时候，还是可以在一个维度里自由旋转的，up向量固定相机的这个维度。

  ```
  lookAt: function ( eye, target, up ) {
          var te = this.elements;
          var x = THREE.Matrix4.__v1; // 空Vector3对象，下同
          var y = THREE.Matrix4.__v2;
          var z = THREE.Matrix4.__v3;
          z.sub( eye, target ).normalize();
          if ( z.length() === 0 ) {
              z.z = 1;
          }
          x.cross( up, z ).normalize();
          if ( x.length() === 0 ) {
              z.x += 0.0001;
              x.cross( up, z ).normalize();
          }
          y.cross( z, x );
          te[0] = x.x; te[4] = y.x; te[8] = z.x;
          te[1] = x.y; te[5] = y.y; te[9] = z.y;
          te[2] = x.z; te[6] = y.z; te[10] = z.z;
          return this;
      },
  ```

-  函数multiply(a,b)，multiplySelf(v)和multiplyToArray(a,b,r)将两个矩阵相乘。

-  函数multiplyScale(s)将对象所有16个元素都乘以s。

- 函数multiplyVector3(v)和multiplyVector4(v)将对象矩阵左乘四维行向量，返回vector3和vector4类型的行向量。如果对象矩阵是模型视图矩阵，输入的向量是点位置信息，则输出的向量则是经过模型变换和相机变换后，该点相对于相机的位置。输入vector3类型向量时，自动补足为齐次坐标，返回时再砍掉第四个分量成为普通坐标。

- 函数rotateAxis(v)使用对象矩阵左上角的3×3子矩阵左乘行向量v，得到一个新的行向量并归一化，返回这个新行向量。该函数同时更新了向量v的值。模型视图矩阵左上角3×3的子矩阵包含了模型矩阵中的旋转信息，将该子矩阵左乘一个向量，得到的新向量实际上就是原向量经过旋转（该旋转效果来自于模型矩阵）得到的。因此该函数名为rotateAxis。

  ```
  rotateAxis: function ( v ) {
          var te = this.elements;
          var vx = v.x, vy = v.y, vz = v.z;
          v.x = vx * te[0] + vy * te[4] + vz * te[8];
          v.y = vx * te[1] + vy * te[5] + vz * te[9];
          v.z = vx * te[2] + vy * te[6] + vz * te[10];
          v.normalize();
          return v;
      },
  ```

- 函数crossVector(v)计算矩阵对象（调用者）和v的叉乘，实际上就是对象矩阵左乘四维行向量v，返回向量。这个具体是做什么的，我还没弄明白。

  ```
  crossVector: function ( a ) {
          var te = this.elements;
          var v = new THREE.Vector4();
          v.x = te[0] * a.x + te[4] * a.y + te[8] * a.z + te[12] * a.w;
          v.y = te[1] * a.x + te[5] * a.y + te[9] * a.z + te[13] * a.w;
          v.z = te[2] * a.x + te[6] * a.y + te[10] * a.z + te[14] * a.w;
          v.w = ( a.w ) ? te[3] * a.x + te[7] * a.y + te[11] * a.z + te[15] * a.w : 1;
          return v;
      },
  ```

- 函数determinant()计算矩阵的行列式值。

- 函数flattenToArray(flat)和函数flattenToArrayOfset(flat,offset)将矩阵转存到一维数组中，前一个函数从flat[0]存储到flat[15]，后一个函数允许指定开始存储的位置，从flat[offset]存储到flat[offset+15]。

- 函数getPosition()和函数setPosition()用来获取或设置矩阵对象的位置分量。正如旋转分量存储在左上角3×3的子矩阵中，位置分量存储在第四行前三个分量上，即element[12]， element[13]， element[14]中。

- 函数getColumeX()，getColumeY()，getColumeZ()分别提取左上角3×3子矩阵的三列。

- 函数compose(translate,rotation,scale)将对象矩阵设置为由vector3类型translate对象表示的平移、由matrix3类型rotation对象表示的旋转、由vector3类型scale对象表示的缩放这三个变换组合到一起的变换矩阵。实际上就是讲其直接填充到模型矩阵的相应子空间。

- 函数decompose(translate,rotation,scale)将矩阵对象拆开到三个对象中，和上一个函数正好相反。

- 函数extractPosition(m)和extractRotation(m)将矩阵对象m中表示位置或旋转的分量抽取到调用者对象中，比如两个物体经过多次各不相同的变换，只需要一个物体的模型视图矩阵extractRotation另一个物体的模型视图矩阵，则调用者就和另外一个物体保持着变换之处相同的旋转方位。

- 函数translate(v)是模型矩阵最基本的变换之一：平移变换，将模型矩阵从属的物体平移向量v。

- 函数rotateX(angle)，rotateY(angle)，rotateZ(angle)分别将模型矩阵从属的物体绕X，Y，Z轴旋转角度angle。

- 函数rotateByAxis(axis, angle)将模型矩阵从属的物体绕一个任意轴axis旋转角度angle，这是上面两条所涉及的变换的多次叠加（叠加参数由当前位置和axis参数决定），我在《模型视图矩阵和投影矩阵：webgl笔记(1)》中曾讨论到绕任意轴旋转的问题。

- 这里不应该有一个scale(s)函数吗？可是我在源码中没找到。

- 函数makeTranslate(x,y,z)，makeRotationX(theta)，makeRotationY(theta)，makeRotationZ(theta)，makeRotationAxis(axis,angle)，makeScale(s)函数将对象矩阵直接重置为单位阵经过一次平移、或绕某轴旋转、或单纯某次缩放后的矩阵。该函数更新对象本身的值，而且更新的结果与对象之前的值毫无关联（这也是make前缀函数的特点）。

- 函数makeFrustum(...)，makePerspective(...)，makeOrthographic(...)也是用来初始化新矩阵，具体含义到相机类里面再讨论，我想相机类的构造函数里一定会调用这些函数的。

- 函数clone()将矩阵对象复制出来并返回。

## Core::Face3

该函数创建一个三角形平面对象

```
THREE.Face3 = function ( a, b, c, normal, color, materialIndex ) {
    this.a = a;
    this.b = b;
    this.c = c;
    this.normal = normal instanceof THREE.Vector3 ? normal : new THREE.Vector3();
    this.vertexNormals = normal instanceof Array ? normal : [ ];
    this.color = color instanceof THREE.Color ? color : new THREE.Color();
    this.vertexColors = color instanceof Array ? color : [];
    this.vertexTangents = [];
    this.materialIndex = materialIndex;
    this.centroid = new THREE.Vector3();
};
```

对象的a，b，c值是三个顶点的索引（后面会说到，Mesh对象中将所有点存储为一个数组）；顾名思义normal是法线；color是颜色；materialIndex是顶点材质索引：这几个参数即可以传入vector3类型又可以传入数组类型。

- clone(x)方法返回一个新的，具有相同值的对象。

## Core::Face4

该函数创建一个四个顶点的面，和Face3几乎一样，略去。

## Core::Math

THREE.Math是一个“静态类”，没有构造函数因此也不需要通过new关键字初始化。该类提供一些必要的数学工具。

- 函数clamp(x,a,b)将x夹在区间[a,b]中。clampBottom(x,a)的作用类似，只不过只夹一边。

- 函数mapLinear(x,a1,a2,b1,b2)计算出一个值y，使得点(x,y)落在(a1,a2)和(b1,b2)连成的直线上。

  ```
  mapLinear: function ( x, a1, a2, b1, b2 ) {
          return b1 + ( x - a1 ) * ( b2 - b1 ) / ( a2 - a1 );
      },
  ```

- 函数random16()，randInt(low,high)，randFloat(low,high)，randFloatSpread(range)分别产生[0,1]区间的16位随机浮点数，[low,high]区间随机整数，[low,high]区间随机浮点数，[-range/2,range/2]区间随机浮点数。

- 函数sigh(x)根据x的符号返回+1或-1。

## Core::Clock

该构造函数创建时钟（确切的说是秒表）对象

```
THREE.Clock = function ( autoStart ) {
    this.autoStart = ( autoStart !== undefined ) ? autoStart : true;
    this.startTime = 0;
    this.oldTime = 0;
    this.elapsedTime = 0;
    this.running = false;
};
```

 函数start()和stop()用来开始计时或停止计时。

- 函数getDelta()返回调用该函数时距离上一次调用该函数时的时间长度，如果是第一次调用该函数，则返回此时距离开始计时时的时间长度。如果autoStart值为真，若在调用getDelta()函数时尚未调用start()函数或者已经调用过stop()函数，则自动开始计时并返回0。如果autoStart()值为假，则在调用start()之前或stop()之后，调用getDelta()返回0。
- 函数getElapsedTime()返回调用该函数时距离开始计时时的时间。

## Core::Color

该构造函数构造一个表示颜色的对象

```
THREE.Color = function ( hex ) {
    if ( hex !== undefined ) this.setHex( hex );
    return this;
};
```

函数setHex(hex)以十六进制序列设置对象的r，g，b属性。实际上在对象中，最终是以这三个属性存储颜色的。

```
setHex: function ( hex ) {
        hex = Math.floor( hex );
        this.r = ( hex >> 16 & 255 ) / 255;
        this.g = ( hex >> 8 & 255 ) / 255;
        this.b = ( hex & 255 ) / 255;
        return this;
    },
```

- 函数setRGB(r,g,b)和setHSV(h,s,v)以RGB值或HSV值设置对象。
- 函数getHex()返回16进制颜色值。
- 函数copyGammaToLinear(color)，copyLinearToGamma(color)将color的rgb值分别平方或开方，赋给调用者对象。
- 函数convertGammaToLinear()和convertLinearToGamma()分别对调用者自身的rgb值平方或开放。