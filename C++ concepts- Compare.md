


# C++ concepts: Compare
###1. C++ std标准库里面的比较方法 (sort等方法里的第三个参数)

> ####equiv(a, b), an expression equivalent to !comp(a, b) && !comp(b, a)


----------
| Expression      |    Return type	 | Requirements  |
| :-------------- | ----------------:| :-----------: |
| comp(a, b)      | implicitly convertible to bool   | Establishes strict weak ordering relation with the following properties For all a, comp(a,a)==false If comp(a,b)==true then comp(b,a)==false if comp(a,b)==true and comp(b,c)==true then comp(a,c)==true






