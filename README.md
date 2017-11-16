# Yaf 框架源码分析注释

本项目基于 3.0.4版本

## PHP扩展开发相关资料

- [PHP扩展开发及内核应用](http://www.cunmou.com/phpbook/index.md)
- [深入理解PHP内核](http://www.php-internals.com/)

## PHP源码相关的宏定义

 - CG    -> Complier Global      编译时信息，包括函数表等(zend_globals_macros.h:32)
 - EG    -> Executor Global      执行时信息(zend_globals_macros.h:43)
 - PG    -> PHP Core Global      主要存储php.ini中的信息
 - SG    -> SAPI Global          SAPI信息

 - CG() 用来访问核心全局变量。(zend/zend_globals_macros.h)
 - PG() PHP全局变量。我们知道php.ini会映射一个或者多个PHP全局结构。(main/php_globals.h)
 - FG() 文件全局变量。大多数文件I/O或相关的全局变量的数据流都塞进标准扩展出口结构。(ext/standard/file.h)

## YAF中相关的宏定义

 - YAF_G
