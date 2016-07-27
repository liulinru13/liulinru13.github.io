---
title: Android Studio日常问题系列
tags:
  - Android Studio
  - 配置问题
date: 2016-07-27 21:57:37
categories: 
	- Android Studio
	- Android
---

## Error(1,0) Plugin with id 'com.android.application' not found

今天在公司，用Android Studio导入项目时，发生错误，错误提示如下：
> Error(1,0) Plugin with id 'com.android.application' not found

经过搜索相关答案后，问题原因是Gradle的配置文件没有完整。
解决方案：

在project的build.gradle文件中，`apply plugin: 'com.android.application'`之后的配置应该是
```

	buildscript{
	    repositories{
	        //本地仓库配置
	        //flatDir{
	        //    dirs 'libs'
	        //}
	        mavenCentral()
	        //maven仓库
	        //或者是 jcenter()
	    }
    
    	dependencies{
    	//gradle的版本
        classpath 'com.android.tools.build:gradle:2.0.0'
    	}
	} 
	
	```


