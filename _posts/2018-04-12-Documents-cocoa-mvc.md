---
categories: "Documents"
comment: 
date: '2018-04-12'
info: 
layout: post
published: true
sha: 3e70fdac283c74447b75b9f9920d5b3c8f505b5a
slug: Documents-the-post-1
tags: []
title: "Cocoa의 MVC 패턴"
type: post

---

# Cocoa의 MVC 패턴

최근 유행하는 MVVM 개념을 정리하기 앞서서 MVC 를 제대로 사용하고 있는지에 대한 의문이 생겼습니다.

하지만 MVC 디자인 패턴에 대해서 공부할수록 혼란은 가중되었습니다.



제가 알고 있는 MVC 패턴에서는 View와 Model이 격리된 구조로 짜야 함에도 불구하고,

인터넷에 있는 MVC 패턴의 소개에서는 View와 Model이 서로에 관여하는 구조로 설명이 되어 있었습니다.



결국 검색을 거쳐 Apple의 [Concepts in Objective-C Programming](https://developer.apple.com/library/content/documentation/General/Conceptual/CocoaEncyclopedia/Model-View-Controller/Model-View-Controller.html) 에서 해답을 찾게 되었습니다.



간략히 정리하자면

원래의 고전적인 MVC는 Smalltalk의 개념으로 Composite, Strategy 및 Observer 패턴이 복합적으로 적용 되었습니다.

그리고 각각 Model,View,Controller가 각자의 역할에 따라 동작합니다.

- Controller : View를 통해 들어온 사용자 액션을 처리하고, View에게 Update를 요청함으로서 Model의 표시 방법을 바꿀수 있습니다. 또한 모델에 Update를 요청함으로서 Model의 상태를 변경할수도 있죠,
- Model : Model의 상태에 변화가 있을때 뷰에 이를 통보합니다. View는 Model의 최신 데이터를 반영할수 있습니다. (다른 버전의 MVC에서는 Controller에 통보 하기도 합니다. 이로서 Controller는 특정한 명령을 수행할수 있죠)
- View : Model의 상태 변경과 Controller의 Update 요청에 따라 View에 반영합니다.



![](/Users/dnax/Documents/%E1%84%80%E1%85%A2%E1%84%87%E1%85%A1%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5/iOS_Dev/resource/traditional_mvc.gif)



애플의 Cocoa Framework개발자들은 Smalltalk의 MVC를 Objective C에서 사용하길 원했고, 고전적인 MVC 패턴대신 수정된 MVC 패턴을 사용했습니다. Cocoa version의 MVC 패턴이 고전적인 MVC와 다른 점은 View와 Model은 완전히 분리 되어 있다는 점입니다. Model은 변경에 대해 View가 바로 받는 대신에 둘 사이의 중재는 모두 Controller가 합니다.



![](/Users/dnax/Documents/%E1%84%80%E1%85%A2%E1%84%87%E1%85%A1%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5/iOS_Dev/resource/cocoa_mvc.gif)



Apple은 이런 Cocoa version의 MVC 패턴을 적용하면 Controller의 비중이 커지지 않을껄로 예상했겠지만, 대부분의 OSX와 iOS 개발자들은 ViewController의 비중이 매우 큰 Massive ViewController 형태로 사용했습니다. 이런 이유는 ViewController 자체가 View의 라이프 사이클과 강하게 연결되어 있어, 확실하게 분리할수 없었기 때문입니다. 이로서 ViewController와 View의 재활용도 힘들게 되었습니다.

또한 이렇게 Massive ViewController 형태의 개발이 성행하게 된건 iOS와 Obejctive C라는 생소한 플랫폼과 언어에 진입하는 사람들에게 기초를 제공해 줬던 수많은 OSX와 iOS의 입문 서적들이 여러가지 이유로(사용자의 쉬운 이해와 지면의 낭비를 막고자 하는등)로 인해 실제 예제코드에서 MVC 패턴을 사용한 코드를 제공하지 않았던것도 하나의 이유가 되지 않았나 싶습니다.



여기까지 왔다가 하나의 궁금증이 생겼습니다.



만일 비행기의 타임테이블을 서버에서 10분마다 받아와 갱신하는 App을 만든다고 했을때

서버의 데이터를 받아와 Model의 데이터에 갱신해주는 처리는 Controller와 Model중에 어디에서 처리해 줘야 하는것일까?

개인적인 견해로는 Model쪽이 처리해 주는게 맞는게 아닌가 합니다.

Model쪽이 데이터에 대한 모든 부분(데이터 레이어와 비지니스로직, 네트워크, 데이터베이스 API 관리등)을 맡아서 처리하는게 MVC의 원래 의도에 더 가깝지 않나 합니다.



참고 :

[Concepts in Objective-C Programming](https://developer.apple.com/library/content/documentation/General/Conceptual/CocoaEncyclopedia/Model-View-Controller/Model-View-Controller.html)

[안드로이드 Architecture 패턴 Part 1: 모델 뷰 컨트롤러 (Model-View-Controller)](https://medium.com/upday-devs/android-architecture-patterns-part-1-model-view-controller-3baecef5f2b6)

[위키백과 - 모델-뷰-컨트롤러](https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC)
