---
layout: default
title: 引入 .c 文件出现的问题
---  

# 引入 .c 文件出现的问题
在做按字母排序的时候引入了一个第三方带有 .c 的文件，结果报了一堆类似于：Unknown type name 'NSString' 的错误，如图：  
![error_with_import_c_file.png](https://raw.githubusercontent.com/StillWalking/jekyll_demo/gh-pages/_resource/_images/error_with_import_c_file.png)

Google 了一下发现是当前项目使用了 .pch 预处理文件会导致这个问题，具体原因不知（原谅我初中英语八级的水平没敢仔细看下去^-^)，解决方法是在预处理文件及 .pch 中添加：

	﻿#ifdef __OBJC__
	
	#endif
然后将头文件声明（所以的？不知道，反正我是这么干的）放到里面去，例如现在变成酱紫：

	#ifdef __OBJC__
	#import <BlocksKit+UIKit.h>
	#import <Masonry.h>
	#import <AFNetworking.h>
	#import <UIImageView+WebCache.h>
	#import <MJRefresh.h>
	#import "YYModel.h"
	#endif

哦对了，还是自己看参考文章靠谱：[stackOverFlow](http://stackoverflow.com/questions/11857765/ios-parse-issues-in-nsobjcruntime-nszone-and-nsobject)

