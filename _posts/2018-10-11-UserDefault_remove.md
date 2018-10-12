---
layout: post
title: UserDefaults 객체 제거
date: 2018-10-11 21:42:01 +0900
category: Swift
comments: true
permalink: /swift/:year/:month/:day/:title/
---
 
### 기존에 사용하던 UserDefault객체중 하나를 제거하고 싶다면.
```swift
UserDefaults.standard.removeObject(forKey: "helloWorldStringKey")
```
### 전체 UserDefault객체 목록을 모두 보고 싶다면
```swift
 for (key, value) in UserDefaults.standard.dictionaryRepresentation() {
   print("\(key) = \(value) \n")
 }
```
또는
```swift
_=UserDefaults.standard.dictionaryRepresentation().map {print("[UserDefaults_CleandUp]:\($0.key): \($0.value)")}
```
또는
```swift

UserDefaults.standard.dictionaryRepresentation().forEach{ print("[UserDefaults_CleandUp]:\($0.key): \($0.value)") }

```
			