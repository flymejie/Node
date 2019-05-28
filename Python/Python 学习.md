# Python 学习

## 格式化输出

```python
# __author__: flyme
# data: 2019/1/22

# 占位符  %s  s => string

name = input("Name:")
age = input("age:")
job = input("Job:")
salary = input("Salary:")

msg = '''
------- info of %s --------
Name : %s
Age : %s
Job : %s
salary : %s
--------  end ----------
''' % (name,name,age,job,salary)

# %s 字符串 %d d= digit 整数 %f f=float 浮点数 isdigit() 判断是否是整数
print(msg)

```

**总结：** **%s 字符串 s=string %d d= digit 整数 %f f=float 浮点数 ****

**isdigit() 判断是否是整数**



