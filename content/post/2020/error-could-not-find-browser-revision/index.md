---
title: "ERROR: Could not find browser revision"
date: "2020-12-16"
categories: 
  - "collection-box"
tags: 
  - "npm"
---

在使用npm进行开发时, 出现了报错

    `... PuppetPuppeteerBridge start() exception: Error: Could not find browser revision 818858. Run "PUPPETEER_PRODUCT=firefox npm install" or "PUPPETEER_PRODUCT=firefox yarn install" to download a supported Firefox browser binary. ...`

解决方案:

1. 删除项目目录中的`node_modules`文件
2. 重新运行`npm install`
