---
layout: post
title: Operation - BlockOperation에 대하여.
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift, Operation, GCD]
comments: true
date: 2018-07-31 21:40:00 +0900
---

예제를 위해 먼저 시간측정하는 `Util.swift` 파일을 하나 만들고 저장하자.

```swift
//  Util.swift

var lastTime:TimeInterval?

func startTimer( handler:()->()){

  let now = Date()
  handler()
  let howLongTimePassed = Date().timeIntervalSince(now)
  print("소요시간: \(howLongTimePassed)")
  
}
```


예제 시작!!!

### 1. 여러 개의 operation을 BlockOperation에 추가할 수 있다.

```swift

var globalValue : Int = 0
func singleOp() {
  
  let addBlockOperation = BlockOperation {
    self.globalValue = 2 + 5
    sleep(1)
  }
  
  startTimer {
    addBlockOperation.start()
  }
  //소요시간: 1.00106596946716 와 비슷하게 표시될 것임.
  print("값 -- : \(self.globalValue)")
  

}
```
Operation은 synchronos하게 실행됨. 즉 동기로!!!. 비동기가 아니다.
Operation 자체는 동기 작업(synchronous  task)과 같다.
만약 원한다면 GCD 큐에 작업을 dispatch할 수도 있다.이렇게 하면 main thread를 벗어나서 백그라운드에서 원하는 작업할 수 있다.

그 다음 코드를 보자. 
BlockOperation를 먼저 만들고 `addExecutionBlock`를 사용하여 task들을 추가하는 것을 볼 수 있다.
```swift
func multipleOperations()
{
  let blockOp2 = BlockOperation()
  blockOp2.addExecutionBlock {  print("hello") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("my") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("name") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("is") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("kuku") ; sleep(1) }
  
  startTimer {
    blockOp2.start()
  }
  //소요시간: 2.00279700756073 로 나옴. 즉 concurrency가 발생했다.    
}
```

총 5초가 걸릴것 같지만 2초 조금 넘게 걸렸다.
BlockOperation는 단순히 default global dispatch queue의 래퍼(wrapper)이다.
즉 5개의 블럭을 실행하고자 default queue의 스레드 3개를 사용한 것 처럼 보인다.

> 중요: 블럭은 각각의 블럭에 대해 independent 하다. 
  A 블럭이 B 블럭의 결과를 조작할 수는 없음.


### 3. dispatch group 처럼 동작
```swift
func multipleOperations_withCompletionBlock()
{
  let blockOp2 = BlockOperation()
  blockOp2.completionBlock = {
    print("모두 수행완료")
  }
  blockOp2.addExecutionBlock {  print("hello") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("my") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("name") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("is") ; sleep(1) }
  blockOp2.addExecutionBlock {  print("kuku") ; sleep(1) }
  
  startTimer {
    blockOp2.start()
  }
  
}
```

### 4. Operation 서브 클래싱하는 법
A. 먼저 Operation 서브클래스를 만들자
```swift
class TiltShiftOperation: Operation {
  var inputImage: UIImage?
  var outputImage: UIImage?
  
  override func main() {
    outputImage = makeBlur(image: inputImage)
  }
 
 func makeBlur(image: UIImage?) -> UIImage? {
    guard let image = image else { return .none }
    sleep(1)
    //image를 blur하게 만드는 작업 생략.
    return image 
  }
}
```
B. 그다음 위위 Operation를 서브클래싱한 TiltShiftOperation를 사용한다.
예시는 다음과 같다.

```swift
let inputImage = UIImage(named: "dark_road_small.jpg")
let processor = TiltShiftOperation()
processor.inputImage = inputImage

startTimer {
  processor.start() 
  //소요시간: 1.11426794528961 , 근데 tableView등에서 쓰기에는 좀 느리다~~~
}

if let output = processor.outputImage {
  print(output)
}
```
Operation 클래스는 start()를 호출하면, 그때부터 작업이 수행된다.
단. TiltShiftOperation의 내부 동작은 생각하지 말자.

