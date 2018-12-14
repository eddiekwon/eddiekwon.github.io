---
layout: post
title: Dash line 그리기
category: iOS
permalink: /swift/:year/:month/:day/:title/

tags: [iOS]
comments: true
date: 2018-12-13 09:13:10 +0900
typora-copy-images-to: ../images/2018-12-13-DrawDashLine
---

Dash line 그리기입니다.

![FF09FAA8-BFBA-4376-B76C-6DF40ED01CF7](/images/2018-12-13-DrawDashLine/FF09FAA8-BFBA-4376-B76C-6DF40ED01CF7.png)

Code:

```swift
final class PrettyView: UIView {
    func drawLine() {
        // draw dashed line 
        let bzPath = UIBezierPath()

        let startingPoint = CGPoint(x: 0, y: height / 2)
        let endingPoint = CGPoint(x: width, y: height / 2)

        bzPath.move(to: startingPoint)
        bzPath.addLine(to: endingPoint)
        bzPath.setLineDash([10, 10], count: 2, phase: 0)

        bzPath.lineWidth = 5
        bzPath.lineCapStyle = .round
        bzPath.stroke()
    }
    override func draw(_ rect: CGRect) {
        height = rect.size.height
        width = rect.size.width
        drawLine()
    }
    init(data: chartData ) {
      //some initialization
       super.init(frame: .zero)
    }

    required init?(coder aDecoder: NSCoder) {
      fatalError("init(coder:) has not been implemented")
    }
}
```



참고: 
공식문서 https://goo.gl/2DPPdp
일어 https://goo.gl/krxXey