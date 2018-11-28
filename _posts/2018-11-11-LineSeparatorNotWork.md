---
layout: post
title: Pretty print JSON issue  
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-11-11 09:12:00 +0900
typora-copy-images-to: ../images/2018-11-11-LineSeparatorNotWork.md
---

### Problem:
```swift
let myPrerryJson = prettyPrintResponse(from: httpResp.allHeaderFields)
print(myPrerryJson)
```
I wanted to pretty print `json response` as follows. 

```json
======================== Header ========================
{
  "Connection" : "keep-alive",
  "Access-Control-Allow-Origin" : "*",
  "Date" : "Mon, 12 Nov 2018 07:36:25 GMT",
  "Access-Control-Allow-Credentials" : "true",
  "Content-Type" : "application\/json; charset=utf-8",
  "Acc
```

However for some reason the result printed so ugly as below:

```json
======================== Header ========================
Optional("{\n  \"Date\" : \"Mon, 12 Nov 2018 08:09:58 GMT\",\n  \"Access-Control-Allow-Origin\" : \"*\",\n  \"Content-Type\" : \"application\\/json; charset=utf-8\",\n  \"Access-Control-Allow-Methods\" : \"GET, POST\",\n  \"Server\" : \"openresty\",\n  \"Access-Control-Allow-Credentials\" : \"true\",\n  \"Content-Length\" : \"40\",\n  \"Connection\" : \"keep-alive\",\n  \"X-Cache-Key\" : \"\\/data\\/2.5\\/weather?APPID=2a6e5a8a3e3d92e541d0323dc7279961&q=seo%20ul\"\n}")
```
As you can see. The result is composed of just one line of long string.

### Solution:  

My Bad!!!

`carriage return character` aka ` \n `  is ignored because printing `Optional` means just printing optional value itself, so you need unwrap optional value like this:

```swift
if let myPrerryJson = prettyPrintResponse(from: httpResp.allHeaderFields){
    print(myPrerryJson)
}
```


Finally I can see pretty printed result:

```json
======================== Header ========================
{
  "Connection" : "keep-alive",
  "Access-Control-Allow-Origin" : "*",
  "Date" : "Mon, 12 Nov 2018 07:36:25 GMT",
  "Access-Control-Allow-Credentials" : "true",
  "Content-Type" : "application\/json; charset=utf-8",
  "Access-Control-Allow-Methods" : "GET, POST",
  "X-Cache-Key" : "\/data\/2.5\/weather?APPID=sxdd9961&q=sxt%20l",
  "Server" : "openresty",
  "Content-Length" : "40"
}
```