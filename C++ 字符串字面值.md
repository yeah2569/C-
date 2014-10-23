


# C++ 字符串字面值
## C++ 基本字符串类型
1.  C++ 字符串类型 char 和 wchar_t
2.  c11 新增了 char16_t 和 char32_t 

> 例子：
> ```
  wchat_t title[] = L"char_t";   // w_char string
  char16_t name[] = u"char16";   // char16 string
  char32_t car[] = U"char 32";   // char32 string
> ```

## C11新增类型
1. c11 支持Unicode字符编码方案UTF-8.C++使用前缀u8表示字符串字面值
2. c11添加了原始字符串类型（raw），将"(和)"作为定界符， 可以使用"+*(和+*)"代替默认定界符"(和)"
> ` R("hello "jack" ！！！")`  -->输出hello "jack"!!!
> ` R+*("(hello "jack"!!!)+*"`   --->输出 "(hello "jack"!!!)