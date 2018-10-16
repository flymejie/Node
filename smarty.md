# smarty

```php 
基本用法
<?php
class login{
    function  __construct()
    {
        $this->smarty = new Smarty(); /* 实例化 */
        $this->smarty ->setTemplateDir('app');/*设置模板位置*/
        $this->smarty ->setCompileDir('compile');/*编译*/
    }
    function index(){
        $title = 'hello';
        $this->smarty->assign('aa' （/* 变量名 */）,$title); 
        $this->smarty->display('view/login.html');
    }
}
{HTML
(调用aa{aa})
{aa}

}
///////////////////////////////////////////////////////////////
class login extends main {
    /* extends main 继承 */
    function  __construct()
    {
      /*调用 construct*/
      parent::__construct();
      
    }
    function index(){
        $title = 'hello';
        $this->smarty->assign('aa','view'); /* smarty assign 声明变量 */
        $this->smarty->display('view/login.html');
      				/* smarty display 在页面中显示内容*/
    }

}
```

