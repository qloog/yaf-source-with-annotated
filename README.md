# Yaf 框架源码分析注释

本项目基于 3.0.4版本

## PHP扩展开发相关资料

- [PHP扩展开发及内核应用](http://www.cunmou.com/phpbook/index.md)
- [深入理解PHP内核](http://www.php-internals.com/)

## YAF中相关的宏定义

 - YAF_G

## PHP源码里的宏定义

 - CG    -> Complier Global      编译时信息，包括函数表等(zend_globals_macros.h:32)
 - EG    -> Executor Global      执行时信息(zend_globals_macros.h:43)
 - PG    -> PHP Core Global      主要存储php.ini中的信息
 - SG    -> SAPI Global          SAPI信息

 - CG() 用来访问核心全局变量。(zend/zend_globals_macros.h)
 - PG() PHP全局变量。我们知道php.ini会映射一个或者多个PHP全局结构。(main/php_globals.h)
 - FG() 文件全局变量。大多数文件I/O或相关的全局变量的数据流都塞进标准扩展出口结构。(ext/standard/file.h)
 
## Zend引擎相关函数说明

### zend_API.h Zend引擎提供的常用API函数

 - `RETURN_STR(s)`： 返回一个zend_string字符串
 - `RETURN_STRING(s)`： 返回一个char *字符串
 - `ZEND_PARSE_PARAMETERS_START(min_num_args, max_num_args)`： 在使用FAST ZPP方式解析PHP方法传入的参数时，会用到这个宏方法。这个宏方法用于指定参数的最小个数和最大个数
 - `ZEND_API int zend_parse_parameters(int num_args, const char *type_spec, ...)`： 解析PHP方法函数传入的参数。把传入的参数转换为PHP内核相应的类型
 - `int zend_set_local_var(zend_string *name, zval *value, int force)`： 设置本地变量，变量名为zend_string.
 - `int zend_set_local_var_str(const char *name, size_t len, zval *value, int force)`： 设置本地变量，变量名为字符串指针。
 - `array_init(arg)`： 初始化数组。宏方法
 - `object_init_ex(arg, ce)`： 使用指定的class_entry初始化对象。宏方法

### zend_execute_API.h 类的操作，方法的执行等相关API方法

 - `zend_class_entry *zend_fetch_class(zend_string *class_name, int fetch_type)`： 获取类

### zend_string.h 字符串zend_string结构相关操作

 - `ZSTR_LEN(zstr)`： 用于获取zend_string字符串的长度
 - `ZSTR_VAL(zstr)`： 用于获取zend_string字符串的值
 - `zend_string *zend_string_init(const char *str, size_t len, int persistent)`： 初始化zend_string字符串
 - `void zend_string_release(zend_string *s)`： 释放zend_string，如果引用数为0，则释放内存。

### zend_typs.h 对于zval结构体的操作方法

> zval操作相关宏方法命名规律：
> ZVAL_ 开头的方法，是用于设置值的相关方法。

 - `ZVAL_NULL(zval *)`: 设置值为null。宏方法
 - `ZVAL_LONG(zval *, long)`: 设置值为整型。宏方法。
 - `ZVAL_STR(zval *, zend_string *)`: 设置值为字符串。宏方法。

### Zend/zend_hash.h 哈希处理方法

 - `zend_hash_num_elements`: 获取哈希/数组的元素个数
 - `array_init(arg)`: 初始化一个数组
 - `array_init_size(arg, size)`: 初始化一个数组，指定初始化数组的元素个数。
 - `ZEND_HASH_FOREACH_KEY_VAL` 和 `ZEND_HASH_FOREACH_END`: 配合使用，实现foreach的效果。

### main/spprintf.h 字符处理

 - `zend_bool ZEND_FASTCALL zend_hash_exists(const HashTable *ht, zend_string *key)`: 检测指定的key在哈希中是否存在。key为字符串
 - `zend_bool ZEND_FASTCALL zend_hash_index_exists(const HashTable *ht, zend_ulong h)`: 检测指定的key在哈希中是否存在。key为数字。
 - `zval* ZEND_FASTCALL zend_hash_find(const HashTable *ht, zend_string *key)`: 根据key查找指定的值。key为字符串。
 - `zval* ZEND_FASTCALL zend_hash_index_find(const HashTable *ht, zend_ulong h)`: 根据key查找指定的值。key为数字。
 - `zend_hash_update(ht, key, pData)`: 更新指定key的值。key为字符串。
 - `zend_hash_index_update(ht, h, pData)`: 更新指定key的值。key为数字.

 
 
 ## 参考
 
  - [PHP 核心：骇客指南](http://php.net/manual/zh/internals2.php)
  - http://www.bo56.com/category/programming-language/php-programming-language/
  
