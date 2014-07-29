Yet Another Framework
---
# http://pecl.php.net/package/yaf/  扩展

# http://www.laruence.com/manual/tutorial.firstpage.html

# 常量
		YAF_VERSION(Yaf\VERSION) Yaf框架的三位版本信息
		YAF_ENVIRON(Yaf\ENVIRON	Yaf的环境常量, 指明了要读取的配置的节, 默认的是product
		YAF_ERR_STARTUP_FAILED(Yaf\ERR\STARTUP_FAILED)	Yaf的错误代码常量, 表示启动失败, 值为512
		YAF_ERR_ROUTE_FAILED(Yaf\ERR\ROUTE_FAILED)	Yaf的错误代码常量, 表示路由失败, 值为513
		YAF_ERR_DISPATCH_FAILED(Yaf\ERR\DISPATCH_FAILED)	Yaf的错误代码常量, 表示分发失败, 值为514
		YAF_ERR_NOTFOUND_MODULE(Yaf\ERR\NOTFOUD\MODULE)	Yaf的错误代码常量, 表示找不到指定的模块, 值为515
		YAF_ERR_NOTFOUND_CONTROLLER(Yaf\ERR\NOTFOUD\CONTROLLER)	Yaf的错误代码常量, 表示找不到指定的Controller, 值为516
		YAF_ERR_NOTFOUND_ACTION(Yaf\ERR\NOTFOUD\ACTION)	Yaf的错误代码常量, 表示找不到指定的Action, 值为517
		YAF_ERR_NOTFOUND_VIEW(Yaf\ERR\NOTFOUD\VIEW)	Yaf的错误代码常量, 表示找不到指定的视图文件, 值为518
		YAF_ERR_CALL_FAILED(Yaf\ERR\CALL_FAILED)	Yaf的错误代码常量, 表示调用失败, 值为519
		YAF_ERR_AUTOLOAD_FAILED(Yaf\ERR\AUTOLOAD_FAILED)	Yaf的错误代码常量, 表示自动加载类失败, 值为520
		YAF_ERR_TYPE_ERROR(Yaf\ERR\TYPE_ERROR)	Yaf的错误代码常量, 表示关键逻辑的参数错误, 值为521
# Yaf 配置选项
		选项名称	默认值	可修改范围	更新记录
		yaf.environ	product	PHP_INI_ALL	环境名称, 当用INI作为Yaf的配置文件时, 这个指明了Yaf将要在INI配置中读取的节的名字
		yaf.library	NULL	PHP_INI_ALL	全局类库的目录路径
		yaf.cache_config	0	PHP_INI_SYSTEM	是否缓存配置文件(只针对INI配置文件生效), 打开此选项可在复杂配置的情况下提高性能
		yaf.name_suffix	1	PHP_INI_ALL	在处理Controller, Action, Plugin, Model的时候, 类名中关键信息是否是后缀式, 比如UserModel, 而在前缀模式下则是ModelUser
		yaf.name_separator	""	PHP_INI_ALL	在处理Controller, Action, Plugin, Model的时候, 前缀和名字之间的分隔符, 默认为空, 也就是UserPlugin, 加入设置为"_", 则判断的依据就会变成:"User_Plugin", 这个主要是为了兼容ST已有的命名规范
		yaf.forward_limit	5	PHP_INI_ALL	forward最大嵌套深度
		yaf.use_namespace	0	PHP_INI_SYSTEM	开启的情况下, Yaf将会使用命名空间方式注册自己的类, 比如Yaf_Application将会变成Yaf\Application
		yaf.use_spl_autoload	0	PHP_INI_ALL	开启的情况下, Yaf在加载不成功的情况下, 会继续让PHP的自动加载函数加载, 从性能考虑, 除非特殊情况, 否则保持这个选项关闭

# 基本目录
		+ public
		  |- index.php //入口文件
		  |- .htaccess //重写规则    
		  |+ css
		  |+ img
		  |+ js
		+ conf
		  |- application.ini //配置文件   
		+ application
		  |+ controllers
		     |- Index.php //默认控制器
		  |+ views    
		     |+ index   //控制器
		        |- index.phtml //默认视图
		  |+ modules //其他模块
		  |+ library //本地类库
		  |+ models  //model目录
		  |+ plugins //插件目录