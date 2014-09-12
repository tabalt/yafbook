
### 3、Yaf应用程序的目录结构

上一节编写的`hello yaf`示例程序，只有两个文件和两个目录，是一个最简单的Yaf程序的目录结构。通常情况下，一个比较完善的目录结构如下：

```
- application/					#应用目录
  - Bootstrap.php   			#初始化类文件
  + controllers					#控制器目录
     - Index.php				
  + views    					#模板文件目录
     |+ index   				
        - index.phtml			
  - library						#类库目录
  - models						#模型类存放目录
  - plugins						#插件类存放目录
+ conf
  |- application.ini			#配置文件
- index.php						#入口文件
```

和hello yaf的示例代码相比，这一次我们有了更多的目录和文件，也更灵活、方便扩展。要使得我们的代码在新的结构下能运行起来，需要做一定的改造。

首先，不再使用数组定义配置，改为在入口文件里实例化Yaf_Application时，直接传入配置文件的路径；入口文件index.php中的内容如下：

```
<?php
define("APPLICATION_PATH",  dirname(__FILE__));
$app = new Yaf_Application(APPLICATION_PATH . "/conf/application.ini");
$app->bootstrap()->run();

```

其次，新增Yaf的配置文件conf/application.ini，该文件是INI格式，支持配置节的继承。

```
[yaf]
; APPLICATION_PATH 是在入口文件中定义的常量
application.directory=APPLICATION_PATH "/application/" 

; product 可以继承 yaf 的配置
[product:yaf]
foo=bar
```

接下来，在application目录下新建Bootstrap.php文件，该文件里是一个继承自Yaf_Bootstrap_Abstract的类Bootstrap，用来在Yaf应用程序运行前做一些初始化的工作。Bootstrap类中所有以"_init"开头的公有方法, 都会被按照定义顺序依次在Yaf_Application::bootstrap() 中被调用。Bootstrap.php中的内容如下：

```
<?php
class Bootstrap extends Yaf_Bootstrap_Abstract {
    public function _initConfig(Yaf_Dispatcher $dispatcher) {
        //..
    }
    public function _initPlugin(Yaf_Dispatcher $dispatcher) {
        //..
    }
}
```

然后，修改默认控制器Index.php，向模板中引入变量name，值为 yaf，删除关闭Yaf的自动渲染模板的代码，修改后的代码如下：

```
<?php
class IndexController extends Yaf_Controller_Abstract {
    public function indexAction() {
        $this->getView()->assign('name', 'yaf');
    }
}
```

创建模板文件views/Index/index.phtml，输出name变量：


```
 <p> hello <?php echo $name; ?></p>
```

最后，对于常用类文件可以放在application/library 目录下，模型类文件存放在application/models目录下，Yaf插件类则存放在application/plugins目录下。

现在，一个完整的Yaf应用程序已经编写成功了，部署代码并通过浏览器中访问，可以看到输出的内容：

```
hello yaf
```


代码地址[ http://github.com/phpsource/yaf/base_struct](http://github.com/phpsource/yaf/base_struct)
