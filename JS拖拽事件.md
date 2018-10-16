# JS拖拽事件

## 一. 实现拖放的步骤：

### 1.1 步骤1：创建一个可拖拽对象：

#### 1.1.1如果想要拖动某个元素，需要设置元素的 draggable 属性为 true。

```
<img id="dragImg" draggable="true" />
```

#### 1.1.2给 dragstart 设置一个事件监听器存储拖拽数据。

```
document.getElementById("dragImg").addEventListener("dragstart", function(event) {
    // 存储拖拽数据和拖拽效果...
    event.dataTransfer.setData("Text",ev.target.id);
}, false);
```

### 1.2 步骤2：放置对象：

假设放置对象的DOM为：

```
<div id="dragTarget"></div>
```

### 1.2.1 dragenter事件，用来确定放置目标是否接受放置。

如果放置被接受，那么这个事件必须取消。

```
document.getElementById("dragTarget").addEventListener("dragenter", function(event) {
    // 阻止浏览器默认事件
    event.preventDefault();
}, false);
```

### 1.2.2 dragover事件，用来确定给用户显示怎样的反馈信息。

如果这个事件被取消，反馈信息（通常就是光标）就会基于 dropEffect 属性的值更新。

```
document.getElementById("dragTarget").addEventListener("dragover", function(event) {
    // 阻止浏览器默认事件
    event.preventDefault();
}, false);
```

### 1.2.3 最后是drop事件，允许放置对象。

```
document.getElementById("dragTarget").addEventListener("drop", function(event) {
    event.preventDefault();
    var data=event.dataTransfer.getData("Text");
    event.target.appendChild(document.getElementById(data));
}, false);
```

## 二. 拖放的相关事件：

| 事件      | 产生事件的元素           | 描述                             |
| --------- | ------------------------ | -------------------------------- |
| dragstart | 被拖放的元素             | 开始拖放操作                     |
| drag      | 被拖放的元素             | 拖放过程中                       |
| dragenter | 拖放过程中鼠标经过的元素 | 被拖放元素开始进入本元素的范围内 |
| dragover  | 拖放过程中鼠标经过的元素 | 被拖放元素正在本元素范围内移动   |
| dragleave | 拖放过程中鼠标经过的元素 | 被拖放元素离开本元素的范围       |
| drop      | 拖放的目标元素           | 有其他元素被拖放到本元素中       |
| dragend   | 拖放的对象元素           | 拖放操作结束                     |

## 三. DataTransfer对象的属性与方法

### 3.1 DataTransfer对象的属性：

| 属性          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| dropEffect    | 表示拖放操作的视觉效果，允许对其进行值的设定。该效果必须在用effectAllowed属性指定的允许的视觉效果范围内，允许指定的值有：none、copy、link、move。 |
| effectAllowed | 用来指定当元素被拖放时所允许的视觉效果。可以指定的值有：none、copy、copyLink、copyMove、link、linkMove、all、uninitialize。 |
| files         | 返回表示被拖拽文件的 FileList。                              |
| types         | 存入数据的MIME类型。如果任意文件被拖拽，那么其中一个类型将会是字符串”Files”。 |

| 方法                                             | 描述                                                         |
| ------------------------------------------------ | ------------------------------------------------------------ |
| void setData(DOMString format, DOMString data)   | 向DataTransfer对象存入数据。                                 |
| DOMString getData(DOMString data)                | 读取DataTransfer对象中的数据。                               |
| void clearData(DOMString format)                 | 清除DataTransfer对象中的数据。如果省略参数format，则清除全部数据。 |
| void setDragImage(Element image, long x, long y) | 用img元素来设置拖放图标。                                    |

## 四. draggable属性兼容性：

![image_1aq4irg51vpoq1j1mnaa9m1dbd9.png-56.1kB](http://static.zybuluo.com/dengzhirong/cxbopjk8ctuajycpdu6urmhm/image_1aq4irg51vpoq1j1mnaa9m1dbd9.png)



# JS拖拽文件上传 实例



```javascript
function dragFiles(Btn){
      //利用html5 FormData() API,创建一个接收文件的对象，因为可以多次拖拽，这里采用单例模式创建对象Dragfiles
    var Dragfiles = (function () {
        var instance;
        return function () {
            if (!instance) {
                instance = new FormData();
            }
            return instance;
        }
    }());
      Btn.ondragover = function (ev) {
        //阻止浏览器默认打开文件的操作
        ev.preventDefault();
        //拖入文件后边框颜色变红
        this.style.borderColor = 'red';
    }

    Btn.ondragleave = function (ev) {
         ev.preventDefault();
        //恢复边框颜色
        this.style.borderColor = 'gray';
    }
    let arr = [];
    Btn.ondrop = function (ev) {
        //恢复边框颜色
        this.style.borderColor = 'gray';
        //阻止浏览器默认打开文件的操作
        ev.preventDefault();
        var files = ev.dataTransfer.files;

        var len = files.length,
            i = 0;
        var frag = document.createDocumentFragment(); //为了减少js修改dom树的频度，先创建一个fragment，然后在fragment里操作
        var tr, time, size;
        var newForm = Dragfiles(); //获取单例
        var it = newForm.entries(); //创建一个迭代器，测试用
        while (i < len) {
            tr = document.createElement('tr');
            let urls = files[i];
            let net = new FileReader();
            net.readAsDataURL(urls);
            net.onload=function(){
                arr.push(this.result);
                // console.log(this.result);
            }
            //获取文件大小
            size = Math.round(files[i].size * 100 / 1024) / 100 + 'KB';
            //获取格式化的修改时间
            time = files[i].lastModifiedDate.toLocaleDateString() + ' ' + files[i].lastModifiedDate.toTimeString().split(' ')[0];
            // 页面显示 结构 
            tr.innerHTML = '<td>' + files[i].name + '</td><td>' + time + '</td><td>' + size + '</td><td>删除</td>';
            console.log(size + ' ' + time);
            frag.appendChild(tr);
            //添加文件到newForm
            newForm.append(files[i].name, files[i]);
            //console.log(it.next());
            i++;
        }
        // 插入到页面
        this.childNodes[1].childNodes[1].appendChild(frag);
        //为什么是‘1'？文档里几乎每一样东西都是一个节点，甚至连空格和换行符都会被解释成节点。而且都包含在childNodes属性所返回的数组中.不同于jade模板
    }
}
```

