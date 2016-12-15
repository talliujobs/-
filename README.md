#代码规范

##空间名(namespace)

###规范

* 一个完全标准的命名空间(namespace)和类(class)的结构是这样的：\<Vendor Name>\(<Namespace>\)*<Class Name>
* 每个命名空间(namespace)都必须有一个顶级的空间名(namespace)("组织名(Vendor Name)")。
* 每个命名空间(namespace)中可以根据需要使用任意数量的子命名空间(sub-namespace)。
* 从文件系统中加载源文件时，空间名(namespace)中的分隔符将被转换 DIRECTORY_SEPARATOR。
* 类名(class name)中的每个下划线_都将被转换为一个DIRECTORY_SEPARATOR。下划线_在空间名(namespace)中没有什么特殊的意义。
* 完全标准的命名空间(namespace)和类(class)从文件系统加载源文件时将会加上.php后缀。
* 组织名(vendor name)，空间名(namespace)，类名(class name)都由大小写字母组合而成。

###示例

	\Doctrine\Common\IsolatedClassLoader => /path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php
	\Symfony\Core\Request => /path/to/project/lib/vendor/Symfony/Core/Request.php
	\Zend\Acl => /path/to/project/lib/vendor/Zend/Acl.php
	\Zend\Mail\Message => /path/to/project/lib/vendor/Zend/Mail/Message.php

##基本代码规范

###1. 概述

* 源文件必须只使用 <?php 和 <?= 这两种标签。

* 源文件中php代码的编码格式必须只使用不带字节顺序标记(BOM)的UTF-8。

* 一个源文件建议只用来做声明（类(class)，函数(function)，常量(constant)等）或者只用来做一些引起副作用的操作（例如：输出信息，修改.ini配置等）,但不建议同时做这两件事。

* 命名空间(namespace)和类(class) 必须遵守PSR-0标准。

* 类名(class name) 必须使用骆驼式(StudlyCaps)写法 (译者注：驼峰式(cameCase)的一种变种，后文将直接用StudlyCaps表示)。

* 类(class)中的常量必须只由大写字母和下划线(_)组成。

* 方法名(method name) 必须使用驼峰式(cameCase)写法(译者注：后文将直接用camelCase表示)。

###2. 文件

####2.1. PHP标签

PHP代码必须只使用长标签(<?php ?>)或者短输出式标签(<?= ?>)；而不可使用其他标签。

####2.2. 字符编码

PHP代码的编码格式必须只使用不带字节顺序标记(BOM)的UTF-8。

####2.3. 副作用

一个源文件建议只用来做声明（类(class)，函数(function)，常量(constant)等）或者只用来做一些引起副作用的操作（例如：输出信息，修改.ini配置等）,但不建议同时做这两件事。

短语副作用(side effects)的意思是 在包含文件时 所执行的逻辑与所声明的类(class)，函数(function)，常量(constant)等没有直接的关系。

副作用(side effects)包含但不局限于：产生输出，显式地使用require或include，连接外部服务，修改ini配置，触发错误或异常，修改全局或者静态变量，读取或修改文件等等

下面是一个既包含声明又有副作用的示例文件；即应避免的例子：

	<?php
	// 副作用：修改了ini配置
	ini_set('error_reporting', E_ALL);
	
	// 副作用：载入了文件
	include "file.php";
	
	// 副作用：产生了输出
	echo "<html>\n";
	
	// 声明
	function foo()
	{
	    // 函数体
	}

下面是一个仅包含声明的示例文件；即应提倡的例子：

	<?php
	// 声明
	function foo()
	{
	    // 函数体
	}
	
	// 条件式声明不算做是副作用
	if (! function_exists('bar')) {
	    function bar()
	    {
	        // 函数体
	    }
	}

###3. 空间名(namespace)和类名(class name)

命名空间(namespace)和类(class)必须遵守 PSR-0.

这意味着一个源文件中只能有一个类(class)，并且每个类(class)至少要有一级空间名（namespace）：即一个顶级的组织名(vendor name)。

类名(class name) 必须使用StudlyCaps写法。

PHP5.3之后的代码必须使用正式的命名空间(namespace) 例子：

	<?php
	// PHP 5.3 及之后:
	namespace Vendor\Model;
	
	class Foo
	{
	}

###4. 类的常量、属性和方法

术语类(class)指所有的类(class)，接口(interface)和特性(trait)

####4.1. 常量

类常量必须只由大写字母和下划线(_)组成。 例子：

	<?php
	namespace Vendor\Model;
	
	class Foo
	{
	    const VERSION = '1.0';
	    const DATE_APPROVED = '2012-06-01';
	}

####4.2. 属性

本指南中故意不对$StulyCaps，$camelCase或者$unser_score中的某一种风格作特别推荐，完全由读者依据个人喜好决定属性名的命名风格。

但是不管你如何定义属性名，建议在一个合理的范围内保持一致。这个范围可能是组织(vendor)级别的，包(package)级别的，类(class)级别的，或者方法(method)级别的。

####4.3. 方法

方法名则必须使用camelCase()风格来声明。

##代码风格

###1. 概述

- 代码必须遵守 PSR-1。

- 代码必须使用4个空格来进行缩进，而不是用制表符。

- 一行代码的长度不建议有硬限制；软限制必须为120个字符，建议每行代码80个字符或者更少。

- 在命名空间(namespace)的声明下面必须有一行空行，并且在导入(use)的声明下面也必须有一行空行。

- 类(class)的左花括号必须放到其声明下面自成一行，右花括号则必须放到类主体下面自成一行。

- 方法(method)的左花括号必须放到其声明下面自成一行，右花括号则必须放到方法主体的下一行。

- 所有的属性(property)和方法(method) 必须有可见性声明；抽象(abstract)和终结(final)声明必须在可见性声明之前；而静态(static)声明必须在可见性声明之后。

- 在控制结构关键字的后面必须有一个空格；而方法(method)和函数(function)的关键字的后面不可有空格。

- 控制结构的左花括号必须跟其放在同一行，右花括号必须放在该控制结构代码主体的下一行。

- 控制结构的左括号之后不可有空格，右括号之前也不可有空格。

####1.1. 示例

	<?php
	namespace Vendor\Package;

	use FooInterface;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;

	class Foo extends Bar implements FooInterface
	{
	    public function sampleFunction($a, $b = null)
	    {
	        if ($a === $b) {
	            bar();
	        } elseif ($a > $b) {
	            $foo->bar($arg1);
	        } else {
	            BazClass::bar($arg2, $arg3);
	        }
	    }
	
	    final public static function bar()
	    {
	        // 方法主体
	    }
	}

###2. 通则

####2.1 基础代码规范

代码必须遵守 PSR-1 中的所有规则。

####2.2 源文件

所有的PHP源文件必须使用Unix LF(换行)作为行结束符。

所有PHP源文件必须以一个空行结束。

纯PHP代码源文件的关闭标签?> 必须省略。

####2.3. 行

行长度不可有硬限制。

行长度的软限制必须是120个字符；对于软限制，代码风格检查器必须警告但不可报错。

一行代码的长度不建议超过80个字符；较长的行建议拆分成多个不超过80个字符的子行。

在非空行后面不可有空格。

空行可以用来增强可读性和区分相关代码块。

一行不可多于一个语句。

####2.4. 缩进

代码必须使用4个空格，且不可使用制表符来作为缩进。

####2.5. 关键字和 True/False/Null

PHP关键字(keywords)必须使用小写字母。

PHP常量true, false和null 必须使用小写字母。

###3. 命名空间(Namespace)和导入(Use)声明

命名空间(namespace)的声明后面必须有一行空行。

所有的导入(use)声明必须放在命名空间(namespace)声明的下面。

一句声明中，必须只有一个导入(use)关键字。

在导入(use)声明代码块后面必须有一行空行。

示例：

	<?php
	namespace Vendor\Package;
	
	use FooClass;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;
	
	// ... 其它PHP代码 ...

###4. 类(class)，属性(property)和方法(method)

术语“类”指所有的类(class)，接口(interface)和特性(trait)。

####4.1. 扩展(extend)和实现(implement)

一个类的扩展(extend)和实现(implement)关键词必须和类名(class name)在同一行。

类(class)的左花括号必须放在下面自成一行；右花括号必须放在类(class)主体的后面自成一行。

	<?php
	namespace Vendor\Package;
	
	use FooClass;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;
	
	class ClassName extends ParentClass implements \ArrayAccess, \Countable
	{
	    // 常量、属性、方法
	}

实现(implement)列表可以被拆分为多个缩进了一次的子行。如果要拆成多个子行，列表的第一项必须要放在下一行，并且每行必须只有一个接口(interface)。

	<?php
	namespace Vendor\Package;
	
	use FooClass;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;
	
	class ClassName extends ParentClass implements
	    \ArrayAccess,
	    \Countable,
	    \Serializable
	{
	    // 常量、属性、方法
	}

####4.2. 属性(property)

所有的属性(property)都必须声明其可见性。

变量(var)关键字不可用来声明一个属性(property)。

一条语句不可声明多个属性(property)。

属性名(property name) 不推荐用单个下划线作为前缀来表明其保护(protected)或私有(private)的可见性。

一个属性(property)声明看起来应该像下面这样。
	
	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
	    public $foo = null;
	}

####4.3. 方法(method)

所有的方法(method)都必须声明其可见性。

方法名(method name) 不推荐用单个下划线作为前缀来表明其保护(protected)或私有(private)的可见性。

方法名(method name)在其声明后面不可有空格跟随。其左花括号必须放在下面自成一行，且右花括号必须放在方法主体的下面自成一行。左括号后面不可有空格，且右括号前面也不可有空格。

一个方法(method)声明看来应该像下面这样。 注意括号，逗号，空格和花括号的位置：

	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
	    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
	    {
	        // 方法主体部分
	    }
	}

####4.4. 方法(method)的参数

在参数列表中，逗号之前不可有空格，而逗号之后则必须要有一个空格。

方法(method)中有默认值的参数必须放在参数列表的最后面。

	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
	    public function foo($arg1, &$arg2, $arg3 = [])
	    {
	        // 方法主体部分
	    }
	}

参数列表可以被拆分为多个缩进了一次的子行。如果要拆分成多个子行，参数列表的第一项必须放在下一行，并且每行必须只有一个参数。

当参数列表被拆分成多个子行，右括号和左花括号之间必须又一个空格并且自成一行。

	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
	    public function aVeryLongMethodName(
	        ClassTypeHint $arg1,
	        &$arg2,
	        array $arg3 = []
	    ) {
	        // 方法主体部分
	    }
	}

####4.5. 抽象(abstract)，终结(final)和 静态(static)

当用到�抽象(abstract)和终结(final)来做类声明时，它们必须放在可见性声明的前面。

而当用到静态(static)来做类声明时，则必须放在可见性声明的后面。

	<?php
	namespace Vendor\Package;
	
	abstract class ClassName
	{
	    protected static $foo;
	
	    abstract protected function zim();
	
	    final public static function bar()
	    {
	        // 方法主体部分
	    }
	}

####4.6. 调用方法和函数

调用一个方法或函数时，在方法名或者函数名和左括号之间不可有空格，左括号之后不可有空格，右括号之前也不可有空格。参数列表中，逗号之前不可有空格，逗号之后则必须有一个空格。

	<?php
	bar();
	$foo->bar($arg1);
	Foo::bar($arg2, $arg3);

参数列表可以被拆分成多个缩进了一次的子行。如果拆分成子行，列表中的第一项必须放在下一行，并且每一行必须只能有一个参数。

	<?php
	$foo->bar(
	    $longArgument,
	    $longerArgument,
	    $muchLongerArgument
	);

###5. 控制结构

下面是对于控制结构代码风格的概括：

- 控制结构的关键词之后必须有一个空格。
- 控制结构的左括号之后不可有空格。
- 控制结构的右括号之前不可有空格。
- 控制结构的右括号和左花括号之间必须有一个空格。
- 控制结构的代码主体必须进行一次缩进。
- 控制结构的右花括号必须主体的下一行。

每个控制结构的代码主体必须被括在花括号里。这样可是使代码看上去更加标准化，并且加入新代码的时候还可以因此而减少引入错误的可能性。

####5.1. if，elseif，else

下面是一个if条件控制结构的示例，注意其中括号，空格和花括号的位置。同时注意else和elseif要和前一个条件控制结构的右花括号在同一行。

	<?php
	if ($expr1) {
	    // if body
	} elseif ($expr2) {
	    // elseif body
	} else {
	    // else body;
	}

推荐用elseif来替代else if，以保持所有的条件控制关键字看起来像是一个单词。

####5.2. switch，case

下面是一个switch条件控制结构的示例，注意其中括号，空格和花括号的位置。case语句必须要缩进一级，而break关键字（或其他中止关键字）必须和case结构的代码主体在同一个缩进层级。如果一个有主体代码的case结构故意的继续向下执行则必须要有一个类似于// no break的注释。

	<?php
	switch ($expr) {
	    case 0:
	        echo 'First case, with a break';
	        break;
	    case 1:
	        echo 'Second case, which falls through';
	        // no break
	    case 2:
	    case 3:
	    case 4:
	        echo 'Third case, return instead of break';
	        return;
	    default:
	        echo 'Default case';
	        break;
	}

####5.3. while，do while

下面是一个while循环控制结构的示例，注意其中括号，空格和花括号的位置。

	<?php
	while ($expr) {
	    // structure body
	}

下面是一个do while循环控制结构的示例，注意其中括号，空格和花括号的位置。

	<?php
	do {
	    // structure body;
	} while ($expr);

####5.4. for

下面是一个for循环控制结构的示例，注意其中括号，空格和花括号的位置。

	<?php
	for ($i = 0; $i < 10; $i++) {
	    // for body
	}

####5.5. foreach

下面是一个foreach循环控制结构的示例，注意其中括号，空格和花括号的位置。

	<?php
	foreach ($iterable as $key => $value) {
	    // foreach body
	}

####5.6. try, catch

下面是一个try catch异常处理控制结构的示例，注意其中括号，空格和花括号的位置。

	<?php
	try {
	    // try body
	} catch (FirstExceptionType $e) {
	    // catch body
	} catch (OtherExceptionType $e) {
	    // catch body
	}

###6. 闭包

声明闭包时所用的function关键字之后必须要有一个空格，而use关键字的前后都要有一个空格。

闭包的左花括号必须跟其在同一行，而右花括号必须在闭包主体的下一行。

闭包的参数列表和变量列表的左括号后面不可有空格，右括号的前面也不可有空格。

闭包的参数列表和变量列表中逗号前面不可有空格，而逗号后面则必须有空格。

闭包的参数列表中带默认值的参数必须放在参数列表的结尾部分。

下面是一个闭包的示例。注意括号，空格和花括号的位置。

	<?php
	$closureWithArgs = function ($arg1, $arg2) {
	    // body
	};
	
	$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
	    // body
	};

参数列表和变量列表可以被拆分成多个缩进了一级的子行。如果要拆分成多个子行，列表中的第一项必须放在下一行，并且每一行必须只放一个参数或变量。

当列表（不管是参数还是变量）最终被拆分成多个子行，右括号和左花括号之间必须要有一个空格并且自成一行。

下面是一个参数列表和变量列表被拆分成多个子行的示例。

	<?php
	$longArgs_noVars = function (
	    $longArgument,
	    $longerArgument,
	    $muchLongerArgument
	) {
	   // body
	};
	
	$noArgs_longVars = function () use (
	    $longVar1,
	    $longerVar2,
	    $muchLongerVar3
	) {
	   // body
	};
	
	$longArgs_longVars = function (
	    $longArgument,
	    $longerArgument,
	    $muchLongerArgument
	) use (
	    $longVar1,
	    $longerVar2,
	    $muchLongerVar3
	) {
	   // body
	};
	
	$longArgs_shortVars = function (
	    $longArgument,
	    $longerArgument,
	    $muchLongerArgument
	) use ($var1) {
	   // body
	};
	
	$shortArgs_longVars = function ($arg) use (
	    $longVar1,
	    $longerVar2,
	    $muchLongerVar3
	) {
	   // body
	};

把闭包作为一个参数在函数或者方法中调用时，依然要遵守上述规则。

	<?php
	$foo->bar(
	    $arg1,
	    function ($arg2) use ($var1) {
	        // body
	    },
	    $arg3
	);

##日志接口

本文档描述了日志类库的通用接口。

主要目标是让类库获得一个Psr\Log\LoggerInterface对象并能通过简单通用的方式来写日志。有自定义需求的框架和CMS可以根据情况扩展这个接口，但推荐保持和该文档的兼容性，以确保应用中使用到的第三方库能将日志集中写到应用日志里。

RFC 2119中的必须(MUST)，不可(MUST NOT)，建议(SHOULD)，不建议(SHOULD NOT)，可以/可能(MAY)等关键词将在本节用来做一些解释性的描述。

关键词实现者在这个文档被解释为：在日志相关的库或框架实现LoggerInterface接口的开发人员。用这些实现者开发出来的类库的人都被称作用户。

###1. 规范

####1.1 基础

- LoggerInterface暴露八个接口用来记录八个等级(debug, info, notice, warning, error, critical, alert, emergency)的日志。

- 第九个方法是log，接受日志等级作为第一个参数。用一个日志等级常量来调用这个方法必须和直接调用指定等级方法的结果一致。用一个本规范中未定义且不为具体实现所知的日志等级来调用该方法必须抛出一个Psr\Log\InvalidArgumentException。不推荐使用自定义的日志等级，除非你非常确定当前类库对其有所支持。

####1.2 消息

- 每个方法都接受一个字符串，或者一个有__toString方法的对象作为message参数。实现者 可以对传入的对象有特殊的处理。如果没有，实现者 必须将它转换成字符串。

- message参数中可能包含一些可以被context参数的数值所替换的占位符。

- 占位符名字必须和context数组类型参数的键名对应。
 
- 占位符名字必须使用一对花括号来作为分隔符。在占位符和分隔符之间不能有任何空格。
 
- 占位符名字应该只能由A-Z，a-z，0-9，下划线_和句号.组成。其它的字符作为以后占位符规范的保留字。
 
- 实现者 可以使用占位符来实现不同的转义和翻译日志成文。因为用户并不知道上下文数据会是什么，所以不推荐提前转义占位符。

下面提供一个占位符替换的例子，仅作为参考：

	<?php
	/**
	* Interpolates context values into the message placeholders.
	*/
	function interpolate($message, array $context = array())
	{
	  // build a replacement array with braces around the context keys
	  $replace = array();
	  foreach ($context as $key => $val) {
	      $replace['{' . $key . '}'] = $val;
	  }
	
	  // interpolate replacement values into the message and return
	  return strtr($message, $replace);
	}
	
	// a message with brace-delimited placeholder names
	$message = "User {username} created";
	
	// a context array of placeholder names => replacement values
	$context = array('username' => 'bolivar');
	
	// echoes "Username bolivar created"
	echo interpolate($message, $context);

####1.3 上下文

- 每个方法接受一个数组作为context参数，用来存储不适合在字符串中填充的信息。数组可以包括任何东西。实现者 必须确保他们尽可能包容的对context参数进行处理。一个context参数的给定值不可导致抛出异常，也不可产生任何PHP错误，警告或者提醒。

- 如果在context参数中传入了一个异常对象，它必须以exception作为键名。记录异常轨迹是通用的模式，并且可以在日志系统支持的情况下从异常中提取出整个调用栈。实现者在将exception当做异常对象来使用之前必须去验证它是不是一个异常对象，因为它可能包含着任何东西。

####1.4 助手类和接口

- Psr\Log\AbstractLogger类可以让你通过继承它并实现通用的log方法来方便的实现LoggerInterface接口。而其他八个方法将会把消息和上下文转发给log方法。
 
- 类似的，使用Psr\Log\LoggerTrait只需要你实现通用的log方法。注意特性是不能用来实现接口的，所以你依然需要在你的类中implement LoggerInterface。
 
- Psr\Log\NullLogger是和接口一起提供的。它在没有可用的日志记录器时，可以为使用日志接口的用户们提供一个后备的“黑洞”。但是，当context参数的构建非常耗时的时候，直接判断是否需要记录日志可能是个更好的选择。
 
- Psr\Log\LoggerAwareInterface只有一个setLogger(LoggerInterface $logger)方法，它可以在框架中用来随意设置一个日志记录器。
 
- Psr\Log\LoggerAwareTrait特性可以被用来在各个类中轻松实现相同的接口。通过它可以访问到$this->logger。
 
- Psr\Log\LogLevel类拥有八个日志等级的常量。

###2. 包

[psr/log](https://packagist.org/packages/psr/log)中提供了上文描述过的接口和类，以及相关的异常类，还有一组用来验证你的实现的单元测试。

###3. Psr\Log\LoggerInterface

	<?php
	
	namespace Psr\Log;
	
	/**
	 * Describes a logger instance
	 *
	 * The message MUST be a string or object implementing __toString().
	 *
	 * The message MAY contain placeholders in the form: {foo} where foo
	 * will be replaced by the context data in key "foo".
	 *
	 * The context array can contain arbitrary data, the only assumption that
	 * can be made by implementors is that if an Exception instance is given
	 * to produce a stack trace, it MUST be in a key named "exception".
	 *
	 * See https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
	 * for the full interface specification.
	 */
	interface LoggerInterface
	{
	    /**
	     * System is unusable.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function emergency($message, array $context = array());
	
	    /**
	     * Action must be taken immediately.
	     *
	     * Example: Entire website down, database unavailable, etc. This should
	     * trigger the SMS alerts and wake you up.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function alert($message, array $context = array());
	
	    /**
	     * Critical conditions.
	     *
	     * Example: Application component unavailable, unexpected exception.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function critical($message, array $context = array());
	
	    /**
	     * Runtime errors that do not require immediate action but should typically
	     * be logged and monitored.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function error($message, array $context = array());
	
	    /**
	     * Exceptional occurrences that are not errors.
	     *
	     * Example: Use of deprecated APIs, poor use of an API, undesirable things
	     * that are not necessarily wrong.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function warning($message, array $context = array());
	
	    /**
	     * Normal but significant events.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function notice($message, array $context = array());
	
	    /**
	     * Interesting events.
	     *
	     * Example: User logs in, SQL logs.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function info($message, array $context = array());
	
	    /**
	     * Detailed debug information.
	     *
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function debug($message, array $context = array());
	
	    /**
	     * Logs with an arbitrary level.
	     *
	     * @param mixed $level
	     * @param string $message
	     * @param array $context
	     * @return null
	     */
	    public function log($level, $message, array $context = array());
	}

###4. Psr\Log\LoggerAwareInterface

	<?php
	
	namespace Psr\Log;
	
	/**
	 * Describes a logger-aware instance
	 */
	interface LoggerAwareInterface
	{
	    /**
	     * Sets a logger instance on the object
	     *
	     * @param LoggerInterface $logger
	     * @return null
	     */
	    public function setLogger(LoggerInterface $logger);
	}

###5. Psr\Log\LogLevel

	<?php
	
	namespace Psr\Log;
	
	/**
	 * Describes log levels
	 */
	class LogLevel
	{
	    const EMERGENCY = 'emergency';
	    const ALERT     = 'alert';
	    const CRITICAL  = 'critical';
	    const ERROR     = 'error';
	    const WARNING   = 'warning';
	    const NOTICE    = 'notice';
	    const INFO      = 'info';
	    const DEBUG     = 'debug';
	}

##自动加载

###1. 概况

这个 PSR 描述的是通过文件路径[自动载入类](http://php.net/autoload)的指南；它作为对 PSR-0 的补充；根据这个 指导如何规范存放文件来自动载入；

###2. 说明（Specification）

1. 术语「类」是一个泛称；它包含类，接口，traits 以及其他类似的结构；

1. 完全限定类名应该类似如下范例：

	`<NamespaceName>(<SubNamespaceNames>)*<ClassName>`
	
	1. 完全限定类名必须有一个顶级命名空间（Vendor Name）；
	1. 完全限定类名可以有多个子命名空间；
	1. 完全限定类名应该有一个终止类名；
	1. 下划线在完全限定类名中是没有特殊含义的；
	1. 字母在完全限定类名中可以是任何大小写的组合；
	1. 所有类名必须以大小写敏感的方式引用；

1. 当从完全限定类名载入文件时：
 
	1. 在完全限定类名中，连续的一个或几个子命名空间构成的命名空间前缀（不包括顶级命名空间的分隔符），至少对应着至少一个基础目录。
	1. 在「命名空间前缀」后的连续子命名空间名称对应一个「基础目录」下的子目录，其中的命名 空间分隔符表示目录分隔符。子目录名称必须和子命名空间名大小写匹配；
	1. 终止类名对应一个以 .php 结尾的文件。文件名必须和终止类名大小写匹配；

1. 自动载入器的实现不可抛出任何异常，不可引发任何等级的错误；也不应返回值；

###3. 范例

如下表格展示的是与完全限定类名、命名空间前缀和基础目录相对应的文件路径：

|完全限定类名|命名空间前缀|基础目录|实际的文件路径|
|:----:|:----:|:----:|:----:|
|\Acme\Log\Writer\File_Writer|Acme\Log\Writer|./acme-log-writer/lib/|./acme-log-writer/lib/File_Writer.php|
|\Aura\Web\Response\Status|Aura\Web|/path/to/aura-web/src/|/path/to/aura-web/src/Response/Status.php|
|\Symfony\Core\Request|Symfony\Core|./vendor/Symfony/Core/|./vendor/Symfony/Core/Request.php|
|\Zend\Acl|Zend|/usr/includes/Zend/|/usr/includes/Zend/Acl.php|

例子中的自动载入器非常适应这个指南，请参照 [示例文件](http://www.php-fig.org/psr/psr-4/PSR-4-autoloader-examples.md)。由于可能随时变更，实例不能作为指南的一部分。
