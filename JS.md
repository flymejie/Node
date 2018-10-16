# JS

```javascript
form.serialize()
form.serializeArray()
let formdate = new formDate()
	processDate:false
	contentType:false
	submit.on('click',function(e){
        e.preventDefault();
        // let str =form.serialize();
        let formdata = new FormData();
        formdata.append('username','zhangsan');
        $.ajax({
            url:'/meizu/index.php/catemanage/add',
            type:'post',
            data:formdata,
            processData:false,
            contentType:false,
            success:function(data){
                console.log(data)
            }
        })
    })
```

## ajax

```
context:this;
在ajax中设置this指向
```

