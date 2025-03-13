---
title: "未命名可重用区块"
date: "2020-06-18"
---

## 代码高亮

### Line Numbers

展示代码行数

\[epcl\_tabs\] \[epcl\_tab title="Effect"\]

    `class A {     void main() => runApp(MyApp()); }`

\[/epcl\_tab\] \[epcl\_tab title="Code"\]

```

<pre class="line-numbers">
    <code class="lang-dart">
    </code>
</pre>
```

\[/epcl\_tab\] \[/epcl\_tabs\]

### Line Highlight

高亮指定行代码

\[epcl\_tabs\] \[epcl\_tab title="Effect"\]

    `class A {     void main() => runApp(MyApp()); }`

\[/epcl\_tab\] \[epcl\_tab title="Code"\]

```

<pre data-line="1">
    <code class="lang-dart">
    </code>
</pre>
```

\[/epcl\_tab\] \[/epcl\_tabs\]

> 指定`data-line`可以为: 1-2, 5, 9-20
> 
> 可与Line Numbers配合使用

### Diff Highlight

\[epcl\_tabs\] \[epcl\_tab title="Effect"\]

```diff-dart
- println("A");
+    println("B");
     println("C")
```

\[/epcl\_tab\] \[epcl\_tab title="Code"\]

```

<pre>
    <code class="language-diff-dart diff-highlight">
    </code>
</pre>
```

\[/epcl\_tab\] \[/epcl\_tabs\]

### Command Line

\[epcl\_tabs\] \[epcl\_tab title="Effect"\]

    `pwd /usr/home/chris/bin ls -la total 2 drwxr-xr-x   2 chris  chris     11 Jan 10 16:48 . drwxr--r-x  45 chris  chris     92 Feb 14 11:10 .. -rwxr-xr-x   1 chris  chris    444 Aug 25  2013 backup -rwxr-xr-x   1 chris  chris    642 Jan 17 14:42 deploy`

\[/epcl\_tab\] \[epcl\_tab title="Code"\]

```
<pre  data-output="" class="command-line" data-user="root" data-host="localhost">
    <code class="lang-bash">
    </code>
</pre>
```

\[/epcl\_tab\] \[/epcl\_tabs\]

> windows使用`data-prompt`参数代替`data-user`和`data-host`

## 布局

### 提示信息

\[epcl\_tabs\] \[epcl\_tab title="Effect"\] \[epcl\_box type="information"\]information\[/epcl\_box\] \[epcl\_box type="error"\]error\[/epcl\_box\] \[epcl\_box type="success"\]success\[/epcl\_box\] \[/epcl\_tab\] \[epcl\_tab title="Code"\]

```
[epcl_box type="information"][/epcl_box]
```

\[/epcl\_tab\] \[/epcl\_tabs\]
