---
layout: post
title: Swift 에러 처리 (번역 요약)
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift, error, translation]
comments: true
date: 2018-08-31 10:40:00 +0900
---
> 출처) https://www.swiftbysundell.com/posts/picking-the-right-way-of-failing-in-swift
등급) 2/5
의견) 좀 더 깊은 설명과 예제가 필요함.
배운점) `assert`는 릴리즈 빌드에서 작동하지 않는다.

Swift 에러 처리에 대한 블로그 글을 매우 간단하게 요약했으므로 원문과 예제를 보려면 출처 사이트를 참고하자.

### 에러 처리에 관한 메소드
-  assert()
-  precondition()
-  fatalError()
-  exit()

### 각 메소드의 차이점
- **nil 또는 error enum case 를 반환**.  가장 간단한 형태이다. 많은 상황에서 유용하지만 적당히 사용해야 한다.
- **Throwing an error** (using `throw MyError`),  호출한 측(caller)에서 에러 처리를 해야 하는 경우이며  `do, try, catch` 패턴을 사용한다. 또 다른 방법으로 에러를 무시하려면 호출 측에서  `try?`를 사용한다.
- **assert() , assertionFailure()**   특정 조건이 true인지 검증할 때 사용함. `DEBUG`빌드에서 이 메소드는 Crash를 발생시키지만, `RELEASE` 빌드에서는 무시된다. 일종의 런타임 `강력 경고`로 보자.
- **precondition() , preconditionFailure()**  assert()와의 가장 큰 차이는 `DEBUG` , `RELEASE` 빌드 모두에서 검증(evaluated) 된다는 점이다.  따라서 조건을 만족하지 못하면 절대로 다음 루틴이 진행되지 않는다.
- **fatalError()**  호출 즉시 프로세스를 죽인다. 즉 크래시 발생한다. 
- **exit()**   프로세스를 종료시킨다. 

### 에러처리 분류

#### 복구 가능한 종류(Recoverable)
- nil 또는 error enum case 를 반환
- throwing an error

#### 복구 불능한 종류(Non-recoverable)
- assert()
- precondition()
- fatalError()
- exit()

### 프로그래머의 실수 vs 실행 오류 (execution errors)

1. 프로그래머의 실수(잘못된 로직이나 config의 오류)
- 복구 불가능 옵션을 사용하자
- 유닛테스팅

2. 외부 요인에 의한 오류
