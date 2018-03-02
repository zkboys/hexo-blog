---
title: web打印
date: 2017-07-12 09:14:25
category: [前端]
tags: [打印]
---

# web打印

`window.print()`直接打印

## 打印分页

如果table 使用规范的结构,打印自动分页时,每一行都会有表头、表尾；

如果需要强制分页，通过添加空div.pageBreak，样式如下

```
<style type="text/css">
　　.pageBreak{ page-break-after:always;}
</style>
```

## 区分打印内容，不打印内容

不需要打印的内容，但是页面需要显示，添加`no-print`class类；
需要打印的内容，但是页面不需要显示，添加`just-print`class类


```
.just-print {
  display: none !important;
}

@media print {
  .no-print {
    display: none !important;
  }

  .just-print {
    display: block !important;
  }
}
```

