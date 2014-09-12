
### 2、hello yaf

没错，我们将遵循惯例，参照最经典的`hello world`，建立一个最简单的Yaf应用程序，取名为`hello yaf`。


第一步，创建一个名为index.php的文件，做为Yaf应用程序的入口文件，这个文件的内容如下：

```
<?php
$configs = array(
    "application" => array(
        "directory" => dirname(__FILE__) . "/application"
    )
);
$app = new Yaf_Application($configs);
$app->run();
```

第二步，建立application目录，并在application目录中建立一个controllers目录。

第三步，在application/controllers目录中，创建文件Index.php，并填写如下内容：


```
<?php
class IndexController extends Yaf_Controller_Abstract {
    public function indexAction() {
        echo 'hello yaf';
        Yaf_Dispatcher::getInstance()->autoRender(false);
    }
}
```

第四步，将上面创建好的文件和目录，复制到一个能访问的web服务器的目录，并通过浏览器访问入口文件index.php；浏览器里将输出：

```
hello yaf
```

细心的同学可能会发现，相比普通的 hello world，我们编写的这个示例程序多了一行有点奇怪的代码：

	Yaf_Dispatcher::getInstance()->autoRender(false);

实际上，这是Yaf的特性导致的。Yaf默认会自动包含并渲染模板文件，加上这一句，关闭Yaf的自动渲染模板功能。


代码地址[ http://github.com/phpsource/yaf/helloyaf](http://github.com/phpsource/yaf/helloyaf)