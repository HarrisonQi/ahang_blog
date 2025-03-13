---
title: "在Flutter中使用16进制颜色"
date: "2020-05-13"
categories: 
  - "flutter"
tags: 
  - "flutter"
coverImage: "在Flutter中使用16进制颜色banner.png"
---

使用16进制表示颜色是较为主流的方式, 那么在本篇文章中将简单讲讲如何在Flutter中使用16进制颜色.

## 方法一: 使用原生方法

Flutter中, `Color`类仅接收整数作为参数. 你也可以使用`fromARGB`或者`fromRGBO`.

比如拿到了一个16进制颜色`#b74093`. 因为`Color`还需要传入透明度, `255`就是最大值(也就是不透明), 转为16进制就是`0xFF`, 所以我们只需这样表示:

```
const color = Color(0xffb74093);
```

正规一点的写法(可选, 因为大小写不敏感):

```
const color = Color(0xFFB74093);
```

## 方法二: 接收字符串格式, 转为Color

创建一个`HexColor`类:

```
class HexColor extends Color {
  static int _getColorFromHex(String hexColor) {
    hexColor = hexColor.toUpperCase().replaceAll("#", "");
    if (hexColor.length == 6) {
      hexColor = "FF" + hexColor;
    }
    return int.parse(hexColor, radix: 16);
  }

  HexColor(final String hexColor) : super(_getColorFromHex(hexColor));
}
```

然后进行调用:

```
Color color1 = HexColor("b74093");
Color color2 = HexColor("#b74093");
Color color3 = HexColor("#88b74093");
```

## 感谢

- [How do I use hexadecimal color strings in Flutter? - Stack Overflow](https://stackoverflow.com/questions/50081213/how-do-i-use-hexadecimal-color-strings-in-flutter)

## 结语

如果你对本篇文章有任何问题, 欢迎在下方评论区, 进行讨论, 或加入[阿航的技术小站QQ交流群](https://jq.qq.com/?_wv=1027&k=egT9rjgu)
