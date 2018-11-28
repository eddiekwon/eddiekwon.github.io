---
layout: post
title: UserDefaults에 Array를 저장하는 방법, 어제오늘 구하기.
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-11-27 09:11:00 +0900
typora-copy-images-to: ../images/2018-11-27-UserDefaultsDate
---

## UserDefaults에 Array를 저장하는 방법, 어제 오늘 구하기

#### Save Date Array

```swift
let array = [Date(), Date(), Date(), Date()]

let defaults = UserDefaults.standard
defaults.set(array, forKey: "SavedDateArray")
```

#### Retrieve array

```swift
let defaults = UserDefaults.standard
let array = defaults.array(forKey: "SavedDateArray")  as? [Date] ?? [Date]()
```
## 어제 오늘 그제 구하기
```swift
let today = Calendar.current.startOfDay(for: Date())
let yesterday =  Calendar.current.date(byAdding: .day, value: -1, to: today)!
let thedbyesterday = Calendar.current.date(byAdding: .day, value: -2, to: today)!
```

## 모델 필터링하기 - 어제 오늘 그제중 하나라면 모델 데이터에서 제거하기

`가정 uploadModel에 startTime, endTime 이라는 Date? 속성이 있다고 가정.`

```swift
let today = Calendar.current.startOfDay(for: Date())
let yesterday =  Calendar.current.date(byAdding: .day, value: -1, to: today)!
let thedbyesterday = Calendar.current.date(byAdding: .day, value: -2, to: today)!
let datesAsCandiates = [today, yesterday, thedbyesterday ]// read from userDefaults.

uploadViewModel.readings = uploadViewModel.readings?.filter({ ( uploadModel) -> Bool in

    if let startDate = uploadModel.startTime, let endTime = uploadModel.endTime {

        var result: Bool = true
        verifyingDateLabel: for aTime in datesAsCandiates {
            if aTime.isInclusiveBetween(from: startDate, until: endTime) {
                result = false
                break verifyingDateLabel
            }
        }     // 사이의 날짜가 맞으면 false 를 리턴하게 끔 함.
      		  // true가 되면 필터링에서 걸러지지 않으므로 
        return result  
	}

	return true
})

```

 