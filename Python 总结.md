# Python 总结

## Python的字符串 

```python
ord()函数获取字符的整数表示 
chr()函数把编码转换为对应的字符 
encode() 方法可以编码为指定的bytes
要把bytes变为str，就需要用 str.decode() 方法
len()函数计算的是str的字符数，如果换成bytes，len()函数就计算字节数：
```



```python
ord()函数获取字符的整数表示 
chr()函数把编码转换为对应的字符 
>>> ord('A')
65
>>> ord('中')
20013
>>> chr(66)
'B'
>>> chr(25991)
'文'
由于Python的字符串类型是str，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把str变为以字节为单位的bytes。

Python对bytes类型的数据用带b前缀的单引号或双引号表示：

x = b'ABC'
要注意区分'ABC'和b'ABC'，前者是str，后者虽然内容显示得和前者一样，但bytes的每个字符都只占用一个字节。

 str.encode() 方法可以编码为指定的bytes
 要把bytes变为str，就需要用 str.decode() 方法
如果bytes中只有一小部分无效的字节，可以传入errors='ignore'忽略错误的字节

要计算str包含多少个字符，可以用len()函数：

>>> len('ABC')
3
>>> len('中文')
2
len()函数计算的是str的字符数，如果换成bytes，len()函数就计算字节数：

>>> len(b'ABC')
3
>>> len(b'\xe4\xb8\xad\xe6\x96\x87')
6
>>> len('中文'.encode('utf-8'))
6
```





