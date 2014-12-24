---
layout: post
title: "iOS8定位服务的变化"
date: 2014-12-24 10:06:55 +0800
comments: true
categories: 技术探索|iOS
---
###定位授权

iOS 8 中定位服务发生了一个小变化，系统重新定义了定位授权的选项:

永不 - 用户不允许应用访问定位信息

使用期间 - 只有当应用处于前台时，应用才可以访问定位信息，后台时则不可以

始终 - 只要应用运行，无论前台后台，都可以访问定位信息

PS：应用运行指的是包含前台和后台。

###请求定位授权

在 iOS 8 以前，当应用请求定位- startUpdatingLocation或是开启 iBeacon 监听- startMonitoringForRegion:和- startRangingBeaconsInRegion:时，系统会自动弹出授权请求。

而在 iOS 8 中，访问定位信息首先需要请求授权：

- requestWhenInUseAuthorization -> 请求在应用前台时使用定位
- requestAlwaysAuthorization -> 请求在应用运行时使用定位
注意：以上两个方法只在 iOS 8 SDK 中才有。

一个简单的例子：

	//创建CLLocationManager对象
    self.locationManager = [[CLLocationManager alloc] init];
    //设置代理为自己
    self.locationManager.delegate = self;
    self.locationManager.desiredAccuracy = kCLLocationAccuracyThreeKilometers;
    self.locationManager.distanceFilter = 0;
    
    [self.locationManager requestWhenInUseAuthorization];
    
    [self.locationManager startUpdatingLocation];
    
###填写授权提示信息

除了在代码中请求授权之外，还需要在工程的Info.plist文件中填写授权提示信息（该文件在 Xcode 5 中常被命名为工程名-Info.plist）.

你需要在Info.plist中添加一个字段叫做NSLocationWhenInUseUsageDescription或NSLocationAlwaysUsageDescription，分别对应不同的授权请求。

![picture1](http://i.imgur.com/ERF9vIZ.png?1)  

这样就可以在 iOS 8 中使用定位信息了，实际应用中的对话框可能是这样的：

![picture2](http://www.yxkfw.com/wp-content/uploads/2014/10/315.png)

另外一点需要注意的是，如果你的应用请求的是- requestAlwaysAuthorization，代表在后台的时候它也有可能获取位置信息，那么 iOS 系统可能会隔一段时间会再次弹出授权对话框请求用户授权以确保隐私安全。

![picture3](http://git.devzeng.com/images/ios8_location/ios8_location_alert.png)
  
###向下兼容

	// Check for iOS 8. Without this guard the code will crash with "unknown selector" on iOS 7.
    if([[[UIDevice currentDevice] systemVersion] floatValue] >=8.0)
    {
        [self.locationManager startUpdatingLocation];
    }
    
或者：

	
    if ([self.locationManager respondsToSelector:@selector(requestWhenInUseAuthorization)]) {
        [self.locationManager requestWhenInUseAuthorization];
    }
    
    
    