---
layout: post
title: Share 기능 구현 (UIActivityViewController )
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-10-30 09:19:00 +0900
typora-copy-images-to: ../images/2018-10-30-Share_Activity
---

iOS에서 공유 버튼을 누르면 사진첩저장, 복사, 프린트, 메시지, 메모등에 추가할 수 있는 `공유`기능이 나옵니다.

![img](https://i.stack.imgur.com/4uhWz.png)
이 기능은 `UIActivityViewController`로 간단히 구현할 수 있습니다.

다음은 코드입니다.

```swift
@IBAction func actionShare(_ sender: UIBarButtonItem) {
    let imageShare = self.viewModel.photos
    guard imageShare.count > 0 else { return  }
    
    let activityViewController = UIActivityViewController(activityItems: imageShare , applicationActivities: nil)
    activityViewController.popoverPresentationController?.sourceView = self.view
    self.present(activityViewController, animated: true, completion: nil)
}
```

사진, 텍스트등 여러가지를 한꺼번에 공유하려면 다음과 같이 합니다.
```swift
@IBAction func actionShareAll(_ sender: UIBarButtonItem) {
    
    let text = "Hello, How are you doing?...."
    let image = UIImage(named: "test.png")
    let someWebsite = URL(string:"https://heapoversomexflow.com")
    let shareAll:[Any] = [text , image! , someWebsite!]
    
    let activityViewController = UIActivityViewController(activityItems: shareAll , applicationActivities: nil)
    activityViewController.popoverPresentationController?.sourceView = self.view
    self.present(activityViewController, animated: true, completion: nil)
}
```