# ES6 Class

```javascript
 # ES5  方法一
function Person(name,age){
        this.name = name;
        this.age = age;
    }
    Person.prototype.showName = function(){
        return `名字为：${this.name}`;
    };
    Person.prototype.showAge = function(){
        return `年龄为：${this.age}`;
    };
    let p1 = new Person('flyme',20);
    console.log(p1.showName());//名字为：flyme
    console.log(p1.showAge()); //年龄为：20
```

```javascript
 #  ES5 方法二
 # assign 合并对象
function Person(name,age){
        this.name = name;
        this.age = age;
    }
    Object.assign(Person.prototype,{
        showName(){
            return `名字为：${this.name}`;
        },
        showAge(){
            return `年龄为：${this.age}`;
        }
    });
    let p1 = new Person('flyme',20);
    console.log(p1.showName());//名字为：flyme
    console.log(p1.showAge()); //年龄为：20
```

```javascript
# ES6 class 没有提升功能， ES5 存在提升
# ES6  constructor
    class Person{
        constructor(name,age){ // 构造函数 调用自动执行
            console.log(`构造函数执行了：${name},${age}`);
        }
    }
    let p1 = new Person('flyme',20);
////////////////////////////////////////
# ES6 
    class Person{
        constructor(name,age){ // 构造函数 调用自动执行
            //console.log(`构造函数执行了：${name},${age}`);
            this.name = name;
            this.age = age;
        }
        showName(){
            return `名字为：${this.name}`;
        }
        showAge(){
            return `年龄为：${this.age}`;
        }
    }
    let p1 = new Person('flyme',20);
    console.log(p1.showName());//名字为：flyme
    console.log(p1.showAge()); //年龄为：20

# ES6
    let aaa = 'flyme';
    let bbb = 'flymejie';

    class Person {
        constructor(name, age) { // 构造函数 调用自动执行
            //console.log(`构造函数执行了：${name},${age}`);
            this.name = name;
            this.age = age;
        }

        showName() {
            return `名字为：${this.name}`;
        }

        showAge() {
            return `年龄为：${this.age}`;
        }

        [aaa+bbb]() {
            return `变量......`;
        }
    }

    let p1 = new Person('flyme', 20);
    // console.log(p1.showName(),p1.showAge());//名字为：flyme 年龄为：20
    // console.log(p1.flyme());
    // console.log(p1.flymeflymejie());
    // console.lo   g(p1[aaa]());
    // console.log(p1[aaa+bbb]());
```

**Class 里面取值用get,存值用set**

```javascript
 class Person{
        constructor(){

        }
        get aaa(){
            return `aaa的属性`
        }
        set aaa(val){
            console.log(`设置aaa属性，值为：${val}`);
        }
    }

    let p1 = new Person();
    console.log(p1.aaa);
```



静态方法：就是类身上的方法 static

### 矫正this

```javascript
1.  fn.call()
2.  fn.apply()
3.  fn.bind()
```



## 类的继承

```javascript
    # // 类的继承 es5
    function Person(name) {
        this.name = name;
    }
    Person.prototype.showName = function () {
        return `名字是:${this.name}`;
    };
    function Student(name, skill) {
        Person.call(this, name); // 继承属性
        this.skill = skill
    }
    Student.prototype = new Person();// 继承方法
    let stu = new Student('flyme','nameflyme');
    console.log(stu.name);
    console.log(stu.showName());
```

```javascript
//es6 extends
    class Person{
        constructor(name){
            this.name = name;
        }
        showName(){
            console.log(`name is ${this.name}`);
        }
    }
    class Student extends Person{

    }
```







