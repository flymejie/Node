# Python 小结

## 条件分支

### if   判断

```python
if 条件:
    条件为真的操作
else :
    条件为假的操作
elif 条件：
	条件执行的操作
temp = input('this is bianliang:')
guess = int(temp)
if guess == 8:
    print('this is true')
    print('you are good')
else:
    print('this is false')
    print('you are looser')
```

### while循环

```python
while 条件:
    条件为真执行的操作， 循环体
    
```

### for 循环

```python
for 目标 in 表达式：
	循环体
```

### range()

```python
range([start],stop[,step=1]) 开始值，结束值，步进值
range(0,5)
list(range(5))
[0,1,2,3,4]

for i in range(5):
    print(i)
 0 1 2 3 4
for i in range(2,9):
    print(i)
2 3 4 5 6 7 8
for i in range(1 , 10, 2):
    print(i)
1 3 5 7 9 


```

### break

```python
终止循环，跳出本层循环
```

### continue

```python
跳出本轮循环
```



### 逻辑运算符

and

## random 模块

```python	
randint(), 返回一个随机的整数
import random
num = random.randint(1,10)
```

## 数据类型

### 字符串

### 整型

### 浮点型

### 布尔类型 bool

true false  特殊的整型 true == 1；false==0；

e记法 ---> 科学记数法

### 类型转换

![5b99173b-0ab0-4a01-9bad-570f3a8e8cb0](C:\Users\Admin\Desktop\5b99173b-0ab0-4a01-9bad-570f3a8e8cb0.png)

```python
整数 int（）
字符串 str（）
浮点数 float（）
浮点数转换为整数 小数点后面直接砍掉
```

### 获取类型

```python
type() 函数 获取数据类型
isinstance() 函数 获取数据类型 两个参数 第一个要测试的内容 第二个判断的类型 返回布尔值

```

## 算术操作符

```python
+ - * / %  ** // 
// 除法 取整除法，浮点数
** 幂运算  3**2 3*3
```

### 优先级

```python
先 * / 后 + - 
```

## 逻辑操作符

```python
and 并且 同真为真，一假为假
or  或 同假为假 
not 取反 
3 < 4 < 5 == (3 < 4) and (4 < 5)
```

### 优先级

```python
幂运算 > 正负号 > 算术操作符 > 比较操作符 > 逻辑运算符
```

## 断言 assert 

当这个关键字后边的条件为假的时候，程序自动崩溃并抛出AssertionError 的异常

## 列表 数组

###  添加元素

```python
创建列表用[]
append() 向列表添加元素 一个元素
	arr.append('this is append')
extend() 向列表添加多个元素 列表形式添加
	arr.extend(['this','is','extend'])
insert() 向列表添加固定位置的元素 第一个参数位置，第二个为元素
	arr.insert(1,'insert')
```

### 从列表中获取元素

```python
arr[index]
```

### 从列表删除元素

```python
remove() arr.remove(元素) 必须知道元素名称
del 是一个语句  del arr[1]
pop() arr.pop(index)
.clear()  清空
```

### 列表分片

```python
一次性获取多个元素
arr[1,3] 不包括3
arr[:3] 获取3以下的元素
arr[:] 获取所有元素
arr[1:] 获取1以后的元素
```

## 元组

```python
元组和列表在实际的使用上是非常相似的，但元组的元素不可随意改变
创建元组用（）逗号,是关键；tuple
tuple1 = (1,2,3,4,5,6)
tuple2 = 1,2,3,5,4,6
元组
```

### 更新和删除一个元组

```python
添加
temp = ('one','two','four','five')
temp = temp[:2] + ('three',) + temp[2:] 先切片在添加
temp = ('one','two','three','four','five')
注意：逗号和括号缺一不可

删除

```

### 元组操作符

```python
+ * 比较 逻辑 关系
```



## 字符串

```python
str = r'this is str' //原始字符串 r
str = '''this is str
this is str2
this is str3
''' // 分行
```



## 字符串的方法

| capitalize()                              | 把字符串的第一个字符改为大写                                 |
| ----------------------------------------- | ------------------------------------------------------------ |
| casefold()                                | 把整个字符串的所有字符改为小写                               |
| center(width)                             | 将字符串居中，并使用空格填充至长度 width 的新字符串          |
| count(sub[, start[, end]])                | 返回 sub 在字符串里边出现的次数，start 和 end 参数表示范围，可选。 |
| encode(encoding='utf-8', errors='strict') | 以 encoding 指定的编码格式对字符串进行编码。                 |
| endswith(sub[, start[, end]])             | 检查字符串是否以 sub 子字符串结束，如果是返回 True，否则返回 False。start 和 end 参数表示范围，可选。 |
| expandtabs([tabsize=8])                   | 把字符串中的 tab 符号（\t）转换为空格，如不指定参数，默认的空格数是 tabsize=8。 |
| find(sub[, start[, end]])                 | 检测 sub 是否包含在字符串中，如果有则返回索引值，否则返回 -1，start 和 end 参数表示范围，可选。 |
| index(sub[, start[, end]])                | 跟 find 方法一样，不过如果 sub 不在 string 中会产生一个异常。 |
| isalnum()                                 | 如果字符串至少有一个字符并且所有字符都是字母或数字则返回 True，否则返回 False。 |
| isalpha()                                 | 如果字符串至少有一个字符并且所有字符都是字母则返回 True，否则返回 False。 |
| isdecimal()                               | 如果字符串只包含十进制数字则返回 True，否则返回 False。      |
| isdigit()                                 | 如果字符串只包含数字则返回 True，否则返回 False。            |
| islower()                                 | 如果字符串中至少包含一个区分大小写的字符，并且这些字符都是小写，则返回 True，否则返回 False。 |
| isnumeric()                               | 如果字符串中只包含数字字符，则返回 True，否则返回 False。    |
| isspace()                                 | 如果字符串中只包含空格，则返回 True，否则返回 False。        |
| istitle()                                 | 如果字符串是标题化（所有的单词都是以大写开始，其余字母均小写），则返回 True，否则返回 False。 |
| isupper()                                 | 如果字符串中至少包含一个区分大小写的字符，并且这些字符都是大写，则返回 True，否则返回 False。 |
| join(sub)                                 | 以字符串作为分隔符，插入到 sub 中所有的字符之间。            |
| ljust(width)                              | 返回一个左对齐的字符串，并使用空格填充至长度为 width 的新字符串。 |
| lower()                                   | 转换字符串中所有大写字符为小写。                             |
| lstrip()                                  | 去掉字符串左边的所有空格                                     |
| partition(sub)                            | 找到子字符串 sub，把字符串分成一个 3 元组 (pre_sub, sub, fol_sub)，如果字符串中不包含 sub 则返回 ('原字符串', '', '') |
| replace(old, new[, count])                | 把字符串中的 old 子字符串替换成 new 子字符串，如果 count 指定，则替换不超过 count 次。 |
| rfind(sub[, start[, end]])                | 类似于 find() 方法，不过是从右边开始查找。                   |
| rindex(sub[, start[, end]])               | 类似于 index() 方法，不过是从右边开始。                      |
| rjust(width)                              | 返回一个右对齐的字符串，并使用空格填充至长度为 width 的新字符串。 |
| rpartition(sub)                           | 类似于 partition() 方法，不过是从右边开始查找。              |
| rstrip()                                  | 删除字符串末尾的空格。                                       |
| split(sep=None, maxsplit=-1)              | 不带参数默认是以空格为分隔符切片字符串，如果 maxsplit 参数有设置，则仅分隔 maxsplit 个子字符串，返回切片后的子字符串拼接的列表。 |
| splitlines(([keepends]))                  | 在输出结果里是否去掉换行符，默认为 False，不包含换行符；如果为 True，则保留换行符。。 |
| startswith(prefix[, start[, end]])        | 检查字符串是否以 prefix 开头，是则返回 True，否则返回 False。start 和 end 参数可以指定范围检查，可选。 |
| strip([chars])                            | 删除字符串前边和后边所有的空格，chars 参数可以定制删除的字符，可选。 |
| swapcase()                                | 翻转字符串中的大小写。                                       |
| title()                                   | 返回标题化（所有的单词都是以大写开始，其余字母均小写）的字符串。 |
| translate(table)                          | 根据 table 的规则（可以由 str.maketrans('a', 'b') 定制）转换字符串中的字符。 |
| upper()                                   | 转换字符串中的所有小写字符为大写。                           |
| zfill(width)                              | 返回长度为 width 的字符串，原字符串右对齐，前边用 0 填充。   |

### 字符串格式化

```python
字符串格式化
replacement 由花括号{}
"{0} love {1}.{2}".format("I","book","com")
"I love book.com"
打印花括号
"{{0}}".format("不打印")
结果 "{0}"
"{0:.1f}{1}".format(27.685,'GB')
结果 '27.7GB'   
f 定点数 与浮点数类似 都是小数  {1} 打印 ＧＢ
: 在替换域中表示格式化符号的开始
．１表示保留一位小数

```



### 字符串格式化符号含义

| **符号** | **说明**                                   |
| -------- | ------------------------------------------ |
| %c       | 格式化字符及其 ASCII 码                    |
| %s       | 格式化字符串                               |
| %d       | 格式化整数                                 |
| %o       | 格式化无符号八进制数                       |
| %x       | 格式化无符号十六进制数                     |
| %X       | 格式化无符号十六进制数（大写）             |
| %f       | 格式化浮点数字，可指定小数点后的精度       |
| %e       | 用科学计数法格式化浮点数                   |
| %E       | 作用同 %e，用科学计数法格式化浮点数        |
| %g       | 根据值的大小决定使用 %f 或 %e              |
| %G       | 作用同 %g，根据值的大小决定使用 %f 或者 %E |

### **格式化操作符辅助命令** 

| **符号** | **说明**                                                   |
| -------- | ---------------------------------------------------------- |
| m.n      | m 是显示的最小总宽度，n 是小数点后的位数                   |
| -        | 用于左对齐                                                 |
| +        | 在正数前面显示加号（+）                                    |
| #        | 在八进制数前面显示 '0o'，在十六进制数前面显示 '0x' 或 '0X' |
| 0        | 显示的数字前面填充 '0' 取代空格                            |

### **Python 的转义字符及其含义**

| **符号** | **说明**             |
| -------- | -------------------- |
| \'       | 单引号               |
| \"       | 双引号               |
| \a       | 发出系统响铃声       |
| \b       | 退格符               |
| \n       | 换行符               |
| \t       | 横向制表符（TAB）    |
| \v       | 纵向制表符           |
| \r       | 回车符               |
| \f       | 换页符               |
| \o       | 八进制数代表的字符   |
| \x       | 十六进制数代表的字符 |
| \0       | 表示一个空字符       |
| \\       | 反斜杠               |



## 列表 list

```python
# __author__: flyme
# data: 2019/2/20

a = ["a", "b", "c", "d", "e", "f", "g", "h"]

# print(a[3])
# 增删改查
# 增   切片
# print(a[1:4])  # 取1-4中间值 ['b', 'c', 'd']
# print(a[1:])  # 取 1-最后 ['b', 'c', 'd', 'e', 'f', 'g', 'h']
# print(a[1:-1])  # -1['b', 'c', 'd', 'e', 'f', 'g']
# print(a[1:-1:1])  # 1:-1:1 1 从左到右一个一个取
# print(a[1:-1:2])  # 1:-1:2 2 从左到右2个2个取
# print(a[2::-1])  # ['c', 'b', 'a']
# print(a[4::-2])  # ['e', 'c', 'a']

# 添加
# a.append("12") # 默认插到最后一位
# print(a) #['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', '12']

# a.insert(2,"21") # 插到指定位置
# print(a)

# 修改
# a[1] = "123"
# print(a) #['a', '123', 'c', 'd', 'e', 'f', 'g', 'h']
# a[1:3] = ["14","15"]
# print(a) #['a', '14', '15', 'd', 'e', 'f', 'g', 'h']
# a[1:4] = ["14","15","16"]
# print(a) #['a', '14', '15', '16', 'e', 'f', 'g', 'h']

# 删除 remove  pop del
# a.remove("a") #根据元素删除
# print(a)  # ['b', 'c', 'd', 'e', 'f', 'g', 'h']
# b = a.remove("a") # 没法取值
# print(b)  # None
# a.pop(1)
# print(a) #['a', 'c', 'd', 'e', 'f', 'g', 'h']
# b = a.pop(1) # 获取删除掉的值
# print(b)
# del a[1]
# print(a) # ['a', 'c', 'd', 'e', 'f', 'g', 'h']
# del a # 删除整个对象
# print(a)

# count 统计某个元素在列表中出现的次数
t = ['to','be','not','to','be']
#print(t.count('to'))

# extend()  给一个列表添加另一个列表
b = [1,2,3]
c = [4,5,6]
b.extend(c)
#print(b,c) #[1, 2, 3, 4, 5, 6] [4, 5, 6]

# index()  下标索引
#print(a.index("d")) # 3

d = ["a", "b", "c", "d", "e", "c","f", "g", "h"]
# 强制获取第二个c
c_index = d.index("c")
c_index_sm = d[c_index+1:].index("c")
c_index_big = c_index + c_index_sm + 1
print(c_index_big)

# reverse()  反转
d.reverse()
print(d)

# sort 排序  字母按ASIC 编码
num = [2,5,4,8,6,14,9]
num.sort(reverse=True) #reverse=True : 从大到小排序  == num.reverse()
print(num)
```

**总结**

### 列表 元组 增删改查

**切片**

```
.count() 查某个元素的出现次数
.index() 根据内容找其对应位置

```

**增加**

```python
.append()  增加一个元素 默认最后位置添加
.insert(index,"内容") 在index位置插入内容  
.extend() 扩展列表
```

**修改**

```python
a[index] = "新的值"
a[start:end] = [a,b,c]
```

**删除**

```python	
.remove("value") 
.pop(index) 根据index删除元素
.pop()  不指定index 删除最后一个
.del('value')
del() 全部删除
.clear()  清空
```

**排序**

```python
sort() 排序 默认从小到大
sort(reverse=True) 从大到小 
.reverse()
```

**身份判断**

```python
type(a) is list
```







