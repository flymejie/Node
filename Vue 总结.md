# Vue 总结

## 指令：

el: 绑定页面中的元素

data: 存放数据

v-show：显示隐藏    元素存在但不显示

v-if: (显示隐藏元素不存在)

```
v-for: 迭代指令
v-for="list in item" {{list.obj}}
```

```
v-bind ：缩写 ：
动态绑定 
```

```html
v-on: 动态绑定事件 缩写@
v-on="onClick",
methods:{
    onClick(){
        
    }
}
<form v-on:submit.prevent='onSubmit'>
    <input type="text">
    <button type="submit"></button>
</form>
// submit.prevent   submit.stop 阻止浏览器默认行为
```

```
v-model:	自定义指令 数据绑定，
v-model.lazy: 惰性更改 输入完成后改变
v-model.trim： 去掉空格
v-model.number: 数字类型
data：{
    input框中更改value
}
```

## 控制流指令

```
v-if=""
v-else-if=''
```

## 计算属性

```javascript
computed:{ //有缓存
    sum:function(){
        return ()
    }
}
```



```
点赞

data:function(){
    return{
        like_count:20,
        liked: false,
    }
}
methods:{
    toggle(){
        if(!this.liked)
        	this.like_count++;
        else
        	this.like_count--;
        this.liked = !this.liked;
    }
}
```

## 父子组件通信

```javascript
父传子：prop 外部往内部传
子传父 ：事件
 平行组件之间通信：事件调度器
 var Event = new Vue(); // 事件调度器
 Vue.component('huahua',{
     template:`
		<div>
		我说：<input @keyup="on_change" v-model="i_said" type="text">
		</div>
	`,
     methods:{
         on_change:function(){
             Event.$emit('huahua-said-something',this.i-said);
         }
     },
     data:function(){
         return{
             i_said:'',
         }
     }
 })

Vue.component('shuandan',{
    template:`<div> 花花说：{{huahua_said}}</div>`,
    data: function(){
        return{
            huahua_said:'',
        };
    },
    mounted:function(){
        var me = this;
        Event.$on('huahua-said-something',function(data){
            me.huahua_said = data;
        })
    }
})

```

## 过滤器 currency

```javascript
Vue.filter('currency',function(val,unit){
    val = val || 0;
    unit = unit ||'',
        return val + unit; // 值 + 单位
})
```



