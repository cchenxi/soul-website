---
title: waf插件
keywords: waf
description: waf插件
---


## 说明

* 本篇注意讲解waf插件适合的场景以及如何使用

## 插件设置

* 在 `soul-admin` 管理后台，插件管理-> waf ,设置为开启。

## 场景

* waf插件也是soul的前置插件，主要用来拦截非法请求，或者异常请求，并且给与相关的拒绝策略。

* 当你发现有大的攻击的适合，你可以根据ip或者host来进行匹配，拦截掉非法的ip与host，设置reject策略。

* 如果用户不想使用此功能，请在admin后台停用此插件。