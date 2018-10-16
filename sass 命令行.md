# sass 命令行

### 命令行编译配置选项;

命令行编译`sass`有配置选项，如编译过后css排版、生成调试map、开启debug信息等，可通过使用命令`sass -v`查看详细。我们一般常用两种`--style``--sourcemap`。

```
//编译格式
sass --watch input.scss:output.css --style compact

//编译添加调试map
sass --watch input.scss:output.css --sourcemap

//选择编译格式并添加调试map
sass --watch input.scss:output.css --style expanded --sourcemap

//开启debug信息
sass --watch input.scss:output.css --debug-info
```

- `--style`表示解析后的`css`是什么排版格式;
  sass内置有四种编译格式:`nested``expanded``compact``compressed`。
- `--sourcemap`表示开启`sourcemap`调试。开启`sourcemap`调试后，会生成一个后缀名为`.css.map`文件。

### 四种编译排版演示;

```
//未编译样式
.box {
  width: 300px;
  height: 400px;
  &-title {
    height: 30px;
    line-height: 30px;
  }
}
```

### nested 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style nested

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px; }
  .box-title {
    height: 30px;
    line-height: 30px; }
```

### expanded 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style expanded

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px;
}
.box-title {
  height: 30px;
  line-height: 30px;
}
```

### compact 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style compact

/*编译过后样式*/
.box { width: 300px; height: 400px; }
.box-title { height: 30px; line-height: 30px; }
```

### compressed 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style compressed

/*编译过后样式*/
.box{width:300px;height:400px}.box-title{height:30px;line-height:30px}
```