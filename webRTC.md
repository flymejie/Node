# webRTC

## 简介



## 视频约束

``` 
width 宽
height  高  4：3  16：9 
aspect Radio 比例 高 / 宽
frameRate 帧率 高平滑
facingMode 摄像头选择  user   :前置摄像头
					environment  ： 后置摄像头
					left   :    前置左侧摄像头
					right   ：  前置右侧摄像头
resizeMode : 画面裁剪					
```



## 音频约束

```
volume 0-1.0 音量相关
sampleRate 音频采样率  11025Hz、22050Hz、24000Hz、44100Hz、48000Hz五个等级
sampleSize 大小 
echoCancellation 回音消除 true false
autoGainControl  自动增音 true false
noiseSupperession 降噪 
latency 延迟大小 200ms 以内最好  
channelCount 声道
deviceID  多个音频设备 设备的切换
groupID  同一个物理设备

```

## 视频特效

```
CSS filter , -webkit-filter/filter  
如何将video 和filter 关联
OpenGL/Metal

```

```
支持的特效种类
特效		  |		说明		|	特效		|	说明
grayscale	| 	灰度		  |   opacity	 | 透明度
sepia		|	褐色		  |	brightness	|	亮度
hue-rotate	|	色相旋转	 | blur       	|  模糊
invert   	| 	反色		  | drop-shadow	  |  阴影
```

## MediaStream

```
轨
MediaStream.addTrack()  向媒体流中加入不同的轨
MediaStream.removeTrack()  移除轨
MediaStream.getVideoTracks() 所有的视频轨
MediaStream.getAudiaTracks() 所有音频轨

```

```
MediaStream 事件
MediaStream.onaddtrack  添加触发的事件
MediaStream.onremovetrack 移除触发的事件
MediaStream.onended  流结束时触发的事件
```



## MediaRecoder 录制媒体流

```
基本格式
var mediaRecorder = new MediaRecorder(stream[,option]);

参数				|		说明
stream				|	媒体流，可从getUserMedia,<video>,<audio>或<canvas>获取
option				|  限制选项
  
限制选项
选项				|	说明
mimeType		  |	video/webm MP4 codecs=vp8  h264 audio/webm mp3 codecs=opus
audioBitsPerSecond | 音频码率
videoBitsPerSecond | 视频码率
bitsPerSecond	   | 整体码率
```



## getDisplayMedia 录制桌面

```
var promise = navigator.mediaDevices.getDisplayMedia(constraints)
constraints 可选 与getUserMedia 函数中一致

设置地址：
chrome://flags/#enable-experimental-web-platform-features
```

## MediaRecorder API

```
MediaRecorder.start(timeslice) 开始录制媒体，timeslice是可选的，如果设置了会按时间切片储存数据
MediaRecorder.stop() 停止录制，此时会触发包括最终Blob数据的dataavailable事件
MediaRecorder.pause  暂停录制
MediaRecorder.resume()  恢复录制
MediaRecorder.isTypeSupported()  检查录制的文件格式是否支持
```

## MediaRecorder 事件

```
MediaRecorder.ondataavailable  当数据有效时触发 每次记录一定时间的数据时（如果没有指定时间片，则记录整个数据时）会定期触发
MediaRecorder.onerror  当发生错误时触发
```

## JavaScript 储存数据的方式

```
string
Blob 
ArrayBuffer 
ArrayBufferView  各种buffer
```

## Socket.Io

```
socket.emit()  给本次链接发消息 
io.in(room).emit()  给某个房间内所有人发消息 io 代表所有节点 in代表某个房间
socket.to(room).emit()  除本连接外，给某个房间内所有人发消息  room内所有人
socket.broadcast.emit()  除本连接外给所有人发消息 整个站点的所有人
```

## Socket.Io 客户端处理消息

```
发送action命令
S: socket.emit('action');
C:socket.on('action',function(){...});
```

```
发送action命令 带data数据 
S: socket.emit('action',data);
C:socket.on('action',function(data){...});
```

```
发送action命令 带data数据 两个 数据
S: socket.emit('action',arg1,arg2);
C:socket.on('action',function(arg1,arg2){...});
```

```
发送一个action 命令 在emit方法中包含回调函数
S: socket.emit('action',data,function(arg1,arg2){...});
C:socket.on('action',function(data,fn){fn('a','b')}); fn:回调函数
```

## 为什么使用socket.io 

```
socket.io 是WebSocket 超集  底层tcp
socket.io 有房间的概念  房间服务器 信令服务器
socket.io 跨平台，跨终端，跨语言 

```

## 改造服务端(node.JS)的基本流程

```
安装 socket.io
引入 socket.io
处理 connection消息

```

## WebRTC 端对端连接

### RTCPeerConnection   

核心类 媒体协商 媒体流 

```
基本格式
pc  = new RTCPeerConnection([configuration])  参数可有可无
```

RTCPeerConnection   方法分类

```
媒体协商
Stream/Track 
传输相关
统计相关
```

**媒体协商过程**![1569036845265](C:\Users\flyme\AppData\Roaming\Typora\typora-user-images\1569036845265.png)

![1569037152314](C:\Users\flyme\AppData\Roaming\Typora\typora-user-images\1569037152314.png)

```
createOffer 会获取本地所支持的音视频编码格式，以及传输相关参数信息

createAnswer 
setLocalDescription  
setRemoteDescription
```

### Track方法

```
addTrack
格式 .addTrack()
 removeTrack
```

![1569038331674](C:\Users\flyme\AppData\Roaming\Typora\typora-user-images\1569038331674.png)