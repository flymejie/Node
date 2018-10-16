# keyCode对照表及JS监听组合按键

## keyCode对照表

1、 字母和数字键的键码值(keyCode)

| 按键 | 键码 | 按键 | 键码 | 按键 | 键码 | 按键 | 键码 |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 65   | J    | 74   | S    | 83   | 1    | 49   |
| B    | 66   | K    | 75   | T    | 84   | 2    | 50   |
| C    | 67   | L    | 76   | U    | 85   | 3    | 51   |
| D    | 68   | M    | 77   | V    | 86   | 4    | 52   |
| E    | 69   | N    | 78   | W    | 87   | 5    | 53   |
| F    | 70   | O    | 79   | X    | 88   | 6    | 54   |
| G    | 71   | P    | 80   | Y    | 89   | 7    | 55   |
| H    | 72   | Q    | 81   | Z    | 89   | 8    | 56   |
| I    | 73   | R    | 82   | 0    | 48   | 9    | 57   |

2、数字键盘上的键的键码值

| 按键 | 键码 | 按键  | 键码 |
| ---- | ---- | ----- | ---- |
| 0    | 96   | 8     | 104  |
| 1    | 97   | 9     | 105  |
| 2    | 98   | *     | 106  |
| 3    | 99   | +     | 107  |
| 4    | 100  | Enter | 108  |
| 5    | 101  | -     | 109  |
| 6    | 102  | .     | 110  |
| 7    | 103  | /     | 111  |

3、功能键的键码值

| 按键 | 键码 | 按键 | 键码 |
| ---- | ---- | ---- | ---- |
| F1   | 112  | F7   | 118  |
| F2   | 113  | F8   | 119  |
| F3   | 114  | F9   | 120  |
| F4   | 115  | F10  | 121  |
| F5   | 116  | F11  | 122  |
| F6   | 117  | F12  | 123  |

4.、控制键的键码值(keyCode)

| 按键      | 键码 | 按键       | 键码 | 按键        | 键码 | 按键 | 键码 |
| --------- | ---- | ---------- | ---- | ----------- | ---- | ---- | ---- |
| BackSpace | 8    | Esc        | 27   | Right Arrow | 39   | -_   | 189  |
| Tab       | 9    | Spacebar   | 32   | Down Arrow  | 40   | .>   | 190  |
| Clear     | 12   | Page Up    | 33   | Insert      | 45   | /?   | 191  |
| Enter     | 13   | Page Down  | 34   | Delete      | 46   | `~   | 192  |
| Shift     | 16   | End        | 35   | Num Lock    | 144  | [{   | 219  |
| Control   | 17   | Home       | 36   | ;:          | 186  | /\|  | 220  |
| Alt       | 18   | Left Arrow | 37   | =+          | 187  | ]}   | 221  |
| Cape Lock | 20   | Up Arrow   | 38   | ,<          | 188  | ‘”   | 222  |

5、多媒体键的键码值(keyCode)

| 按键   | 键码 |
| ------ | ---- |
| 音量加 | 175  |
| 音量减 | 174  |
| 停止   | 179  |
| 静音   | 193  |
| 浏览器 | 172  |
| 邮件   | 180  |
| 搜索   | 170  |
| 收藏   | 171  |

## onkeyup的缺陷处理

**场景说明**：在html的input框中限制指定内容输入，例如只允许输入数字（其他情况都是正则表达式变化）。方法很多，以如下代码为例：

```
<!DOCTYPE>
<html>
<head>
    <meta charset="UTF-8">
</head>
<body>
<input type="text" onkeyup='this.value=this.value.replace(/[^\w_]/g,"");'/>
</body>12345678
```

**代码缺陷**：上边代码中，input框只能输入数字（本文想阐述的不是这个），但是该方法有个缺陷，当用户输入数字后想修改时，键盘的←键无法使光标向左移动，即便鼠标点击，使光标到指定位置，在按下键盘任意键修改时，光标还是会跑到最右端。 
**解决方案及原理**：onkeyup中代码是键盘每一次按下放开之后将input框中的value按照正则处理，不符合正则的替换成“”，也就是去掉，具体可以查看js的replace函数。那么上述代码缺陷就可以从keyCode入手。代码如下

```
<!DOCTYPE>
<html>
<head>
    <meta charset="UTF-8">
</head>
<body>
<input type="text"  onkeyup='if(event.keyCode!=8 && event.keyCode!=37 && event.keyCode!=16 && event.keyCode!=20 && event.keyCode!=39 && (event.keyCode<48 || event.keyCode>105) && (!event.shiftKey && event.keyCode != 189))this.value=this.value.replace(/[^\w_]/g,"");'/>
</body>12345678
```

**代码说明**：上边event.keyCode后边的数字代表的是键盘对应的按键，可以查看上边的keyCode对照表。上边代码中是按下键盘上数字按键，Backspace按键，←，→按键时，不作正则处理，从而避免了第一段代码的问题。

## JS监听组合按键

组合按键一般分以下两种： 
两位组合建，如：ctrl（cmd）+ 其他按键，alt+其他按键，shift+其他按键 
三位组合键，如：ctrl（cmd）+ shift + 其他按键，Ctrl（cmd）+ alt + 其他按键 
在组合键中，js的event中有以下几种属性：ctrlKey（metaKey）、altKey、shiftKey 
以下以按下Shift+1组合键为例(其他的类似)：

```
<!DOCTYPE>
<html>
<head>
    <meta charset="UTF-8">
</head>
<body>
<input type="text" onkeyup="test()"/>
</body>
<script>
function test(){
    if(event.shiftKey && event.keyCode == 49){
        alert(1);
    }
}
</script>
12345678910111213141516
```

**代码说明**：执行上述代码后，按下组合键Shift+1在input框中输出！同时，会alert出1。**但是个人在测试过程中有个疑问，就是组合键的Shift+其他按键，js如何区分中英文的。**