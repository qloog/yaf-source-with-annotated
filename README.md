# Yaf 框架源码分析注释

本项目基于 3.0.4版本

## PHP扩展开发相关资料

- [PHP扩展开发及内核应用](http://www.cunmou.com/phpbook/index.md)
- [深入理解PHP内核](http://www.php-internals.com/)


## Zend引擎相关函数说明

### zend_API.h Zend引擎提供的常用API函数

 - `RETURN_STR(s)`： 返回一个zend_string字符串
 - RETURN_STRING(s)： 返回一个char *字符串
 - ZEND_PARSE_PARAMETERS_START(min_num_args, max_num_args)： 在使用FAST ZPP方式解析PHP方法传入的参数时，会用到这个宏方法。这个宏方法用于指定参数的最小个数和最大个数
 - ZEND_API int zend_parse_parameters(int num_args, const char *type_spec, ...)： 解析PHP方法函数传入的参数。把传入的参数转换为PHP内核相应的类型
 - int zend_set_local_var(zend_string *name, zval *value, int force)： 设置本地变量，变量名为zend_string.
 - int zend_set_local_var_str(const char *name, size_t len, zval *value, int force)： 设置本地变量，变量名为字符串指针。
 - array_init(arg)： 初始化数组。宏方法
 - object_init_ex(arg, ce)： 使用指定的class_entry初始化对象。宏方法

### zend_execute_API.h 类的操作，方法的执行等相关API方法

 - zend_class_entry *zend_fetch_class(zend_string *class_name, int fetch_type)： 获取类

### zend_string.h 字符串zend_string结构相关操作

 - ZSTR_LEN(zstr)： 用于获取zend_string字符串的长度
 - ZSTR_VAL(zstr)： 用于获取zend_string字符串的值
 - zend_string *zend_string_init(const char *str, size_t len, int persistent)： 初始化zend_string字符串
 - void zend_string_release(zend_string *s)： 释放zend_string，如果引用数为0，则释放内存。

### zend_typs.h 对于zval结构体的操作方法

### Zend/zend_hash.h 哈希处理方法

### main/spprintf.h 字符处理


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
