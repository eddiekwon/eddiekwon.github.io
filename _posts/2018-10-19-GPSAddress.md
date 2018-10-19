---
layout: post
title: GPS정보로 주소 출력하기
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-10-19 13:40:00 +0900
typora-copy-images-to: ./2018-10-19-GPSAddress
---

임포트

![CLLocationManagerDelegate](/images/2018-10-19-GPSAddress/F39B8793-436B-4802-A0F9-0CB42110A785.png)

흐름도

![BC1EA550-BE0D-4545-92A6-6263E295A9FB](/images/2018-10-19-GPSAddress/BC1EA550-BE0D-4545-92A6-6263E295A9FB.png)

전체 코드

```swift
import UIKit
import CoreLocation

class ViewController: UIViewController ,  CLLocationManagerDelegate{
    var locationManager:CLLocationManager!
    
  
    @IBOutlet weak var addressLabel: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        getLocationInfo()
    }
    
    
    func getLocationInfo(){
        locationManager = CLLocationManager()
        locationManager.delegate = self
        locationManager.desiredAccuracy = kCLLocationAccuracyBest
        locationManager.requestAlwaysAuthorization()
        
        if CLLocationManager.locationServicesEnabled() {
            locationManager.startUpdatingLocation()
            //locationManager.startUpdatingHeading()
        }else{
            print("오..이런..gps.")
        }
    }

    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        guard let location = manager.location else{
            return
        }
        let cor = location.coordinate
        printAddressBasedOnGPS(lati: cor.latitude , longi: cor.longitude)
    }
    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error)
    {
        print("Error \(error)")
    }
    
    @IBAction func actionSwitch(_ sender: UISwitch) {
        
        if sender.isOn {
            locationManager.startUpdatingLocation()
        }else{
            locationManager.stopUpdatingLocation()
        }
        
    }
}

// MARK: 로깅 부분
extension ViewController{
    func printAddressBasedOnGPS(lati:CLLocationDegrees, longi:CLLocationDegrees){
        let findLocation = CLLocation(latitude: lati, longitude: longi )
        let geocoder = CLGeocoder()
        let locale = Locale(identifier: "Ko-kr") //원하는 언어의 나라 코드를 넣어주시면 됩니다.
        
        geocoder.reverseGeocodeLocation(findLocation, preferredLocale: locale, completionHandler: {(placemarks, error) in
            
            
            if let address: [CLPlacemark] = placemarks {
                
                if let name: String = address.last?.name {
                    print(name , lati, address )
                    self.addressLabel.text = "\(name) :  gps\(lati)"
                    self.addressLabel.backgroundColor = UIColor.particle()
                }
                
                // refered to CLPlacemark 객체:
                // po address.last?.administrativeArea 경기도
                // po address.last?.locality 성남시
                // po address.last?.name     성남대로343번길
                // po address.last?.country  대한민국
                
                
            } }) 
         
    }
}
```

참고 사이트:  http://devsc.tistory.com/82 [You Know Programing?]

