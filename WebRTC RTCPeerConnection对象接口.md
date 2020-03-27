## WebRTC RTCPeerConnection对象接口





RTCPeerConnection API是每个浏览器之间点对点连接的核心。要创建RTCPeerConnection对象,只需编写:

var pc = RTCPeerConnection(config);

config配置参数中至少包含iceServers参数。它是包含有关STUN和TURN服务器的信息的URL对象数组,在查找ICE候选时使用。您可以在code.google.com找到可用的公共STUN服务器的列表。



根据您是发起者还是被发起对象,在连接的每一边使用稍微不同的方式使用RtcPeerConnection对象。



**下面是用户流程:**

注册onicecandidate处理程序,它将任何ICE候选发送给其他对等方。

注册onaddstream处理程序,它负责处理从远程计算机接收到的视频流的显示。

注册消息处理程序。您的信令服务器还应该有一个处理来自远程计算机的消息处理程序。如果消息包含RTCSessionDescription对象,则应该使用RTCSessionDescription()方法将其添加到RTCPeerConnection对象。如果消息包含RTCIceCandidate对象,则应该使用addIceCandidate()方法将其添加到RTCPeerConnection对象。

使用getUserMedia()设置本地媒体流,并使用addstream()方法将其添加到RTCPeerConnection对象。

开始提供/回答协商过程,这是呼叫者的流量不同于被呼叫者的唯一步骤。调用者使用createoffer( )方法开始协商,并注册一个收到rtcsessiondescription对象的回调。然后,这个回调应该使用setlocaldescription( )将这个rtcsessiondescription对象添加到rtcpeerconnection对象中。最后,调用者应该使用信令服务器将这个rtcsessiondescription发送到远程计算机。另一方面,被呼叫者,在createanswer()方法中注册相同的回调。请注意,只有在从调用者收到通知后,才会启动流。

**RTCPeerConnection API说明**

##  属性列表

RTCPeerConnection.iceConnectionState (只读):返回描述连接状态的RTCIceConnectionState枚举。当此值更改时,将触发IceConnectionStateChange事件。'

#### 取值范围

new-ICE代理正在等待远程候选或收集地址。

checking-ICE代理有远程候选,正在检查可用连接。

connected-ICE代理找到了可用的连接,但仍在检查更多的候选以获得更好的连接。

completed-ICE代理找到一个可用的连接,并停止测试远程候选。

failed-ICE代理没有找到可以匹配的链接。

disconnected-ICE代理已经断开链接。

closed-ICE代理已经关闭链接。

RTCPeerConnection.iceGatheringState (只读):返回描述连接的ICE状态的RTCIceGatheringState枚举。

new - 对象被创建

gathering -ICE正在收集候选

complete - ICE已完成收集

RTCPeerConnection.localDescription (只读):返回描述本地会话的RTCSessionDescription。如果尚未设置,则可以为空。

RTCPeerConnection.peerIdentity (只读):返回一个RTCIdentityAssertion。它由国内流离失所者(域名)和表示远程对等项身份的名称组成。

RTCPeerConnection.remoteDescription (只读):返回描述远程会话的RTCSessionDescription 。如果尚未设置,则可以为空。



RTCPeerConnection.signalingState (只读):返回描述本地连接的信令状态的RTCSignalingState枚举。这个状态描述了SDP的提供。当此值更改时,将触发signalingstatechange事件。

#### 取值范围:

stable - 初始状态。在进度中没有SDP提议/应答交换。

have-local-offer - 连接的本地端本地使用SDP提议。

have-remote-offer - 连接的远程端本地使用SDP提议。

have-local-pranswer - 已接受远程SDP提议,且一个SDPpranswer在本地应用

have-remote-pranswer - 已应用本地SDP,且远程也已应用SDPpranswer。

closed  - 链接断开



### **事件处理**



**RTCPeerConnection.onaddstream**:在触发addstream事件时调用此处理程序。当远程计算机加入到此连接时,将发送此事件。

**RTCPeerConnection.ondatachannel**:在触发datachannel事件时调用此处理程序。当将rtcdatachannel添加到此连接时,将发送此事件。

**RTCPeerConnection.onicecandidate**:在触发icecandidate事件时调用此处理程序。当将rtcicecandidate对象添加到脚本时,将发送此事件。

**RTCPeerConnection.oniceconnectionstatechange**:在触发iceconnectionstatechange事件时调用此处理程序。当iceconnectionstate更改的值时,将发送此事件。

**RTCPeerConnection.onidentityresult**:在触发identityresult事件时调用此处理程序。当在创建报价或通过getidentityassertion( )的应答期间生成身份断言时,将发送此事件。

**RTCPeerConnection.onidpassertionerror**:在触发idpassertionerror事件时调用此处理程序。当国内流离失所者(identitry提供程序)在生成身份断言时发现错误时,将发送此事件。

**RTCPeerConnection.onidpvalidation**:在触发idpvalidationerror事件时调用此处理程序。当国内流离失所者(identitry提供程序)在验证身份断言时发现错误时发送此事件。

**RTCPeerConnection.onnegotiationneeded**:在触发negotiationneeded事件时调用此处理程序。此事件由浏览器发送以通知协商,在将来的某个时间将需要协商。

**RTCPeerConnection.onpeeridentity:**在触发peeridentity事件时调用此处理程序。当在此连接上设置和验证对等身份时,将发送此事件。

**RTCPeerConnection.onremovestream**:在触发signalingstatechange事件时调用此处理程序。当signalingstate更改的值时,将发送此事件。

**RTCPeerConnection.onsignalingstatechange**:在触发removestream事件时调用此处理程序。当从此连接中删除mediastream时,将发送此事件。

### **方法说明**

**RTCPeerConnection()**:返回一个新的RTCPeerConnection对象.

**RTCPeerConnection.createOffer()**:创建一个提议(请求)来查找远程节点,方法的前两个参数是成功和错误的回调,第三个参数是可选项,例如是否启用音频或视频流。

**RTCPeerConnection.createAnswer()**:提议/应答的协商过程中创建对远程节点收到提议的答复,方法的前两个参数是成功和错误回调,第三个参数是要创建的答案的可选项。

**RTCPeerConnection.setLocalDescription()**:更改本地的连接描述,描述定义连接的属性。连接必须能够支持新的和旧的描述。方法有三个参数,即:RTCSessionDescription对象,更改成功的回调,更改失败的回调。

**RTCPeerConnection.setRemoteDescription()**:更改远端的连接描述,描述定义连接的属性。连接必须能够支持新的和旧的描述。方法有三个参数,即:RTCSessionDescription对象,更改成功的回调,更改失败的回调。

**RTCPeerConnection.updateIce()**:更新ICE代理的状态

**RTCPeerConnection.addIceCandidate()**:为ICE代理提供远程候选。

**RTCPeerConnection.getConfiguration()**:返回一个RTCConfiguration对象,它表示RTCPeerConnection对象的配置。

**RTCPeerConnection.getLocalStreams()**:返回本地MediaStream连接的数组。

**RTCPeerConnection.getRemoteStreams()**:返回远程MediaStream连接的数组。

**RTCPeerConnection.getStreamById()**:返回指定id的本地或远程MediaStream。

**RTCPeerConnection.addStream()**:添加一个MediaStream作为本地视频或音频源。

**RTCPeerConnection.removeStream()**:移除作为本地视频或音频源的MediaStream。

**RTCPeerConnection.close()**:关闭一个链接。

**RTCPeerConnection.createDataChannel()**:创建一个新的RTCDataChannel。

**RTCPeerConnection.createDTMFSender()**:创建与特定MediaStreamTrack关联的新rtcdtmfsender。允许通过连接发送DTMF(双音多频)电话信令.

**RTCPeerConnection.getStats()**:创建包含连接的统计信息的新RTCStatsReport。

**RTCPeerConnection.setIdentityProvider()**:设置身份提供者,获取三个参数—名称、用于通信的协议和可选的用户名。

**RTCPeerConnection.getIdentityAssertion()**:收集身份断言,预期在应用程序中不会处理此方法。因此,您可以显式地调用它来预测需求。


  