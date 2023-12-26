---
layout: post
title:  "Native Crash原理、分析与定位"
date:   2023-12-25 10:30:00 +0800
categories: crash
---

# 项目中遇到的问题

近期在Bugly平台上看到SIGSEGV的native crash激增，主要发生在“遥遥领先”新机型上，但是这个问题不是必现，在云测平台上找了相同型号的机器并未复现问题。好在是新机型，在公司附近一家手机体验店里的某台机器上必现。经过对比，未加固的包一切正常，那大概率是加固方案的问题了。

（这里吐槽下，因为店里手机不方便通过USB导出日志，所以想着能不能通过WiFi调试，然而“遥遥领先”机型竟然没有这个选项。。折腾了半天，最后通过开发者选项-提交错误报告导出了日志。看来有必要找个时间好好梳理下开发者选项的功能。）

回到主题，之前见到Native crash就头大，甚至选择当鸵鸟，能躲就躲。是时候好好了解一下相关原理和分析思路了。

# 信号列表

参考 [Linux 信号列表][Linux 信号列表] 。

# 捕获机制和处理流程

基于Android 7.0从源码角度介绍处理流程，参考 [理解Native Crash处理流程][理解Native Crash处理流程] 。

在 [Android 平台 Native 代码的崩溃捕获机制及实现][Android 平台 Native 代码的崩溃捕获机制及实现] 这篇文章中，腾讯Bugly团队在信号机制的基础上开发了捕获组件。

# 问题分析与定位

参考 [Android 平台 Native Crash 问题分析与定位][Android 平台 Native Crash 问题分析与定位] 。

[Linux 信号列表]: https://tennysonsky.blog.csdn.net/article/details/46010505?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~C

[理解Native Crash处理流程]: http://gityuan.com/2016/06/25/android-native-crash/

[Android 平台 Native 代码的崩溃捕获机制及实现]: https://mp.weixin.qq.com/s/g-WzYF3wWAljok1XjPoo7w?

[Android 平台 Native Crash 问题分析与定位]: https://juejin.cn/post/7124689738811834382/