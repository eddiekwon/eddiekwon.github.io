---
layout: post
title: URLComponents 사용법
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-10-20 09:49:00 +0900
typora-copy-images-to: ../images/2018-10-20-URLComponents
---

URLComponents 를 설명한 그림입니다.

![F2CE5C05-67A2-490A-821F-6F3023306896](/images/2018-10-20-URLComponents/F2CE5C05-67A2-490A-821F-6F3023306896.png)

다음은 코드입니다.

```swift
func learnComponents(){
  
  let urlString = "http://www.myhelloworld.com?param1=value1&param2=value2"
  
  let url = URL(string: urlString)!
  
  let myCompo = URLComponents(url: url, resolvingAgainstBaseURL: false)
  let items = myCompo?.queryItems

  items?.forEach({ (item) in
    print(item.name , String(item.value!) )
  })
  //result:
  //param1 Optional("value1")
  //param2 Optional("value2")
}
```