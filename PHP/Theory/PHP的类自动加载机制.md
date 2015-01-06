# PHP的类自动加载机制  

  在PHP开发过程中，如果希望从外部引入一个class，通常会使用include和require方法，去把定义这个class的文件包含进来。这个在小规模开发的时候，没什么大问题。但在大型的开发项目中，这么做会产生大量的require或者include方法调用，这样不因降低效率，而且使得代码难以维护，况且require_once的代价很大。

  在PHP5之前，各个PHP框架如果要实现类的自动加载，一般都是按照某种约定自己实现一个遍历目录，自动加载所有符合约定规则的文件的类或函数。 当然，PHP5之前对面向对象的支持并不是太好，类的使用也没有现在频繁。 在PHP5后，当加载PHP类时，如果类所在文件没有被包含进来，或者类名出错，Zend引擎会自动调用__autoload 函数。此函数需要用户自己实现__autoload函数。 在PHP5.1.2版本后，可以使用spl_autoload_register函数自定义自动加载处理函数。当没有调用此函数，默认情况下会使用SPL自定义的spl_autoload函数。

## 1、 __autoload示例：

    function __autoload($class_name) {  
       echo '__autload class:', $class_name, '<br />';  
    }  
  
new Demo();  
以上的代码在最后会输出：__autload class:Demo。
并在此之后报错显示： Fatal error: Class ‘Demo’ not found

我们一般使用_autoload自动加载类如下：

<?php   
  
　　function __autoload($class_name) {   
　　     require_once ($class_name . “class.php”);   
　　}   
   $memo= new Demo();　　  
我们可以看出_autoload至少要做三件事情，第一件事是根据类名确定类文件名，第二件事是确定类文件所在的磁盘路径(在我们的例子是最简单的情况，类与调用它们的PHP程序文件在同一个文件夹下)，第三件事是将类从磁盘文件中加载到系统中。第三步最简单，只需要使用include/require即可。要实现第一步，第二步的功能，必须在开发时约定类名与磁盘文件的映射方法，只有这样我们才能根据类名找到它对应的磁盘文件。 

因此，当有大量的类文件要包含的时候，我们只要确定相应的规则，然后在__autoload()函数中，将类名与实际的磁盘文件对应起来，就可以实现lazy loading的效果。从这里我们也可以看出__autoload()函数的实现中最重要的是类名与实际的磁盘文件映射规则的实现。 

但现在问题来了，假如在一个系统的实现中，假如需要使用很多其它的类库，这些类库可能是由不同的开发工程师开发，其类名与实际的磁盘文件的映射规则不尽相同。这时假如要实现类库文件的自动加载，就必须在__autoload()函数中将所有的映射规则全部实现，因此__autoload()函数有可能会非常复杂，甚至无法实现。最后可能会导致__autoload()函数十分臃肿，这时即便能够实现，也会给将来的维护和系统效率带来很大的负面影响。在这种情况下，在PHP5引入SPL标准库,一种新的解决方案，即spl_autoload_register()函数。

2、spl_autoload_register()函数

此函数的功能就是把函数注册至SPL的__autoload函数栈中，并移除系统默认的__autoload()函数。下面的例子可以看出：

function __autoload($class_name) {  
    echo '__autload class:', $class_name, '<br />';  
}  
function classLoader($class_name) {  
    echo 'SPL load class:', $class_name, '<br />';  
}  
spl_autoload_register('classLoader');  
new Test();//结果：SPL load class:Test  
语法：bool  spl_autoload_register ( [callback $autoload_function] )    接受两个参数：一个是添加到自动加载栈的函数，另外一个是加载器不能找到这个类时是否抛出异常的标志。第一个参数是可选的，并且默认指向spl_autoload()函数，这个函数会自动在路径中查找具有小写类名和.php扩展或者.ini扩展名，或者任何注册到spl_autoload_extensions()函数中的其它扩展名的文件。


<?php    
class ClassLoader     
{     
    public static function loader($classname)     
    {     
        $class_file = strtolower($classname).".php";     
        if (file_exists($class_file)){     
            require_once($class_file);     
        }     
    }     
}      
// 方法为静态方法     
spl_autoload_register('ClassLoader::loader');      
$test = new Test();  
      一旦调用spl_autoload_register()函数，当调用未定义类时，系统会按顺序调用注册到spl_autoload_register()函数的所有函数，而不是自动调用__autoload()函数。如果要避免这种情况，需采用一种更加安全的spl_autoload_register()函数的初始化调用方法：

if(false === spl_autoload_functions()){      
    if(function_exists('__autoload')){      
        spl_autoload_registe('__autoload',false);      
    }      
 }     
spl_autoload_functions()函数会返回已注册函数的一个数组,如果SPL自动加载栈还没有被初始化,它会返回布尔值false。然后，检查是否有一个名为__autoload()的函数存在,如果存在，可以将它注册为自动加载栈中的第一个函数，从而保留它的功能。之后，可以继续注册自动加载函数。

还可以调用spl_autoload_register()函数以注册一个回调函数,而不是为函数提供一个字符串名称。如提供一个如array('class','method')这样的数组,使得可以使用某个对象的方法。

下一步，通过调用spl_autoload_call('className')函数，可以手动调用加载器，而不用尝试去使用那个类。这个函数可以和函数class_exists('className',false)组合在一起使用以尝试去加载一个类，并且在所有的自动加载器都不能找到那个类的情况下失败。

f(spl_autoload_call('className') && class_exists('className',false)){      
    
    } else {      
    }     
SPL自动加载功能是由spl_autoload() ,spl_autoload_register(), spl_autoload_functions() ,spl_autoload_extensions()和spl_autoload_call()函数提供的。
