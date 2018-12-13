---
layout: post
title: Background Fetch / Swift
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-11-27 09:11:00 +0900
typora-copy-images-to: ../images/2018-12-01-BackgroundFetch
---

#### 2018-12-01-BackgroundFetch

Targets - Capabilities에 `Background fetch`를 켜줍니다. / Test환경: Xcode 10, swift 4

![A9589800-F4F6-4FE8-8770-51718E9A49D9](/images/2018-12-01-BackgroundFetch/A9589800-F4F6-4FE8-8770-51718E9A49D9.png)

```swift
import  UserNotifications


func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

    UIApplication.shared.setMinimumBackgroundFetchInterval(UIApplication.backgroundFetchIntervalMinimum)
    if #available(iOS 10.0 , *){ //10이후에만 작동하므로.
        UNUserNotificationCenter.current().requestAuthorization(options: .badge) { (granted, error) in
            if error != nil {
                // success!
            }
        }
    }
    
    return true
}

func application(_ application: UIApplication, performFetchWithCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
    
    print("haha 실행됨.")
    UIApplication.shared.applicationIconBadgeNumber = 20
   //completionHandler(.newData)
   //completionHandler(.noData)
}
```

실행하자마자 앱을 내리고( 홈버튼 을 누르고)  

 ![CDB9FCF9-D97B-4BA7-8D93-A94A267DE327]( /images/2018-12-01-BackgroundFetch/CDB9FCF9-D97B-4BA7-8D93-A94A267DE327.png)

Xcode - Debug - Simulate Background Fetch를 선택하면 print 문이 출력되는 것을 확인할 수 있습니다. 또한 다음처럼 아이콘이 바뀝니다.

 ![D92D5F64-C91A-4955-8F47-8E58854AF961](/images/2018-12-01-BackgroundFetch/D92D5F64-C91A-4955-8F47-8E58854AF961.png)

끝.

참고: http://avilos.codes/mobile/ios-swift/ios-swift-멀티태스킹multitasking-백그라운드background-페치fetch/

