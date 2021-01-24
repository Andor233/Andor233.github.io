---
layout: post
title: "Ros in Unreal"
date: 2021-1-24
description: 
image: /assets/images/Hana/1.jpg
author: Mayhem Drown
tags: 
  - Ros
  - Tech
  - Unreal
---

现在越来越多的仿真器开始使用`Unreal`，但是几乎所有人在和`ROS`通讯时都是在中间套了一层，几乎没有人直接和`ROS`通讯的，而且`Ros Bridge`那个东西性能也着实不行。

<!--break-->

于是我就在寻思能不能把`Ros`直接编译到`Unreal`里，可是遇到了一个问题，`Unreal`为了躲避GPL使用了`Clang`和`libc++`，甚至还是静态链接的`abi`。而ROS的预编译版本全都是基于`libstdc++`的。虽然`UnrealBuildTools`里装模做样地留了一些有关`GCC`和`libstdc++`的代码，但是已经是不知道是什么北京猿人生活时期的代码了，已经完全不能使用。网上也找不到任何文明发展后的有做过类似的事情的人，只能找到一份看起来像是石器时代的`gist`。

那就自己来呗，反正下载SDK的时候也内置了编译器和标准库。但是有碰到了一个很傻逼的问题，`Unreal`的`libc++`是静态链接的，而`ROS`还需要开启异常和`RTTI`，这就很操蛋了，我尝试了各种方法，但是总死在把第一个string传参进函数的时候。后来想通了既然都已经改了这么多为什么不把`ROS`整个丢进去呢。于是在大刀阔斧的修改下有了这儿一个东西。

https://github.com/Andor233/RosInUnreal

希望可以帮到大家

C++什么时候才能把module用起来啊