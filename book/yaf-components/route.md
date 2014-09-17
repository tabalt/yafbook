## Yaf路由

路由是php mvc框架中很重要的一环，用于转发用户请求到正确的业务逻辑的实现。

Yaf的路由分为两部分：路由器(Yaf_Router)和路由协议(Yaf_Route_Abstract)。路由协议负责解析请求Url，提取映射module、controller、action的参数和用户自定义参数。路由器负责注册、管理、运行路由协议。

在一个项目中，只能有一个路由器，但是可以有多个路由协议。路由器按照路由协议的注册顺序的倒序依次尝试调用，即最后注册的协议最先尝试调用。当一个路由协议运行成功时，路由器将不再执行剩余的路由协议，而是将解析出来的参数传递给请求（Yaf_Request_Abstract）对象，并通过派遣器(Yaf_Dispatcher)定位执行正确的Controller类的action方法。


### 路由协议

Yaf内置路由协议有6种，分别是Yaf_Route_Simple、Yaf_Route_Supervar、Yaf_Route_Static
Yaf_Route_Map、Yaf_Route_Rewrite、Yaf_Route_Regex。通过实现接口Yaf_Route_Interface，也可以定义自己的路由协议。

* Yaf_Route_Static

Yaf_Route_Static是默认的路由协议，它分析处理这样格式的url： `/module/controller/action/var1/value1/var2/value2`，如果module未在配置modules="Index,Foo" 中定义，则会认为module为默认的模块，其他参数取值依次前移。

rewrite


请求中的request_uri, 在去除掉base_uri以后, 获取到真正的负载路由信息的request_uri片段, 具体的策略是, 根据"/"对request_uri分段, 依次得到Module,Controller,Action, 在得到Module以后, 还需要根据Yaf_Application::$modules来判断Module是否是合法的Module, 如果不是, 则认为Module并没有体现在request_uri中, 而把原Module当做Controller, 原Controller当做Action:

//TODO

* Yaf_Route_Simple
* Yaf_Route_Supervar
* Yaf_Route_Rewrite
* Yaf_Route_Regex
* Yaf_Route_Map
* 自定义路由协议


### 路由用法

1、在Bootstrap类中，定义一个_initRouter() 方法
2、在配置文件中直接指定路由协议

