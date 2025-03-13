---
title: "世界，您好！"
date: "2020-04-07"
categories: 
  - "collection-box"
---

你好, 我是阿航

```

import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

Future main() async {
  // set preferred orientations (landscape only)
  await SystemChrome.setPreferredOrientations([
    DeviceOrientation.landscapeLeft,
    DeviceOrientation.landscapeRight,
  ]);

  // disable all UI overlays (show fullscreen)
  await SystemChrome.setEnabledSystemUIOverlays([]);
}

// start app
runApp(
  Directionality(
    textDirection: TextDirection.ltr,
    child: Stack(
      children: [
        // placeholder for game
        Container(
          color: Color(0xff27ae60),
        ),

        // joypad overlay
        Container(),
      ],
    ),
  ),
);


```
