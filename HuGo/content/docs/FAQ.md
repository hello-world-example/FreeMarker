# 常见问题



## 输出

> - [处理不存在的值](http://www.kerneler.com/freemarker2.3.23/dgui_template_exp.html#dgui_template_exp_missing)

### 默认值

```
name!"unknown"
(user.name)!"unknown" 
```

### 空字符串

```
name!
(user.name)!
```

### 判空

```
<#if (user.name)??>
  user.name 非空
</#if>

<#if !(user.name)??>
  user.name 为空
</#if>
```

### 时间格式化

```
${.now?string('yyyy-MM-dd HH:mm:ss.SSS')}
```

### Boolean 类型输出

```
${(1 == 2)?string('true','false')}
```



## 循环

### List

> [序列切分](http://www.kerneler.com/freemarker2.3.23/dgui_template_exp.html#dgui_template_exp_seqenceop_slice)
>
> [循环变量内建函数](http://www.kerneler.com/freemarker2.3.23/ref_builtins_loop_var.html)

```html
<#list items as item>
  ${item?index}
</#list>

<!-- 拼接 -->
<#list ["Joe", "Fred"] + ["Julia", "Kate"] as user>
  ${user}
</#list>

<!-- 切分 -->
<#assert seq = ["A", "B", "C", "D", "E"]>
<#list seq[1..3] as i>${i}</#list>
```



### Map

```html
<#list map as k,v>
  ${k}:${v}
</#list>

<!-- key 只能是 string -->
<#list map?keys as key>
    ${key}:${map[key]}
</#list>
```



## 函数

- 集合包含：`${items?seq_contains("item")?string('包含','不包含')`
- 字符串包含：`${'str'?contains('s')?string('包含','不包含')}`
- 集合大小：`${items?size}`
- 字符串大小：`${'str'?length}`
- 集合拼接：`${items?join(',')}`



## Read More

- [模板一览](http://www.kerneler.com/freemarker2.3.23/dgui_quickstart_template.html)
- [表达式](http://www.kerneler.com/freemarker2.3.23/dgui_template_exp.html)