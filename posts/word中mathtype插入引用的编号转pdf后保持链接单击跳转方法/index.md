# Word中Mathtype插入引用的编号转PDF后保持链接（单击跳转）方法

Mathtype插入引用的编号转PDF后不能单机跳转的原因：Mathtype引用采用的是GOTOBUTTON（域代码）。

右键切换域代码如下：

![](https://pic4.zhimg.com/v2-3086a54154e78920e281db7a0b5908e3_r.jpg)

要是PDF能单击跳转需要引用是超链接类型，单个引用可以右键编辑域代码，批量操作的话需要用到宏。再编一个宏事后运行的话多一个步骤有些不便捷，于是从Mathtype插入引用的原始命令处修改是最好的，一次性解决。

Mathtype插入命令在`C:\Program Files (x86)\Microsoft Office\root\Office16\STARTUP\MathType Commands 2016.dotm`，Word中打开该文件（不要文件夹里打开），再在`开发者工具 - Visual Basic`打开模块MTPlaceRef找到：

![](https://pic4.zhimg.com/v2-db8384a1518569fc84f084a8bad27acb_r.jpg)

```vb
'insert nested reference field to display equation text
'(\! causes seq not to be reevaluated at current location)
.Fields.Add Range:=.Range, Type:=wdFieldRef, _
    Text:=eqnBkMrk$ + " " + Strings.ChrW(&H5C) + "* Charformat " + Strings.ChrW(&H5C) + "!"
```

将

```vb
Text:=eqnBkMrk$ + " " + Strings.ChrW(&H5C) + "* Charformat " + Strings.ChrW(&H5C) + "!"
```

修改为

```vb
Text:=eqnBkMrk$ + " \h " + Strings.ChrW(&H5C) + "* Charformat " + Strings.ChrW(&H5C) + "!"
```

`\h`表示超链接，保存替换原文件。

修改后再插入的编号PDF中单击跳转，Word中还是双击跳转而不是Ctrl+单击。

> [!note]
> 附上成品，替换原文件即可：[https://www.aliyundrive.com/s/netVpZPSiid](https://www.aliyundrive.com/s/netVpZPSiid)



---

> 作者: [Jason](https://github.com/actforjason)  
> URL: https://actforjason.github.io/posts/word%E4%B8%ADmathtype%E6%8F%92%E5%85%A5%E5%BC%95%E7%94%A8%E7%9A%84%E7%BC%96%E5%8F%B7%E8%BD%ACpdf%E5%90%8E%E4%BF%9D%E6%8C%81%E9%93%BE%E6%8E%A5%E5%8D%95%E5%87%BB%E8%B7%B3%E8%BD%AC%E6%96%B9%E6%B3%95/  

