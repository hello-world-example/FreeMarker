

# 拆分模板



## include

> http://www.kerneler.com/freemarker2.3.23/ref_directive_include.html
>
> 主要用于导入模板片段

```html
<!-- 查找指定文件 -->
<#include "/common/copyright.ftl">
  
<!-- 从任意目录查找 -->
<#include "*/commons/footer.ftl">
```



## import

> http://www.kerneler.com/freemarker2.3.23/ref_directive_import.html
>
> 主要用来定 声明命名空间，导入指定模板中 **宏**、**函数**、**变量** 等

```html
<#import "/libs/mylib.ftl" as my>

<@my.copyright date="1999-2002"/>
```



## macro

> http://www.kerneler.com/freemarker2.3.23/ref_directive_macro.html

### 无参数宏

```html
<#macro test>
  Test text
</#macro>

<!-- 调用 宏 -->
<@test/>
```

### 有参数宏

```html
<#macro test foo bar baaz>
  Test text, and the params: ${foo}, ${bar}, ${baaz}
</#macro>

<@test foo="a" bar="b" baaz=5*5-2/>
```

### 可变参数宏

```html
<#macro img src extra...>
  <img src="/context${src?html}" 
  <#list extra?keys as attr>
    ${attr}="${extra[attr]?html}"
  </#list>
  >
</#macro>

<@img src="/images/test.png" width=100 height=50 alt="Test"/>
```

### 嵌套宏

> 可用来定制整个页面的结构

```html
<#macro do_twice>
  1. <#nested>
  2. <#nested>
</#macro>

<@do_twice>something</@do_twice>
```





## function

> http://www.kerneler.com/freemarker2.3.23/ref_directive_function.html

```html
<#function avg nums...>
  <#local sum = 0>
  <#list nums as num>
    <#local sum = sum + num>
  </#list>
  <#if nums?size != 0>
    <#return sum / nums?size>
  </#if>
</#function>
    
${avg(10, 20)}
${avg(10, 20, 30, 40)}
${avg()!"N/A"}
```

## Read More

- [指令参考](http://www.kerneler.com/freemarker2.3.23/ref_directives.html)
