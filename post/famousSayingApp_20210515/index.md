---
layout: post
title:  "FamousSayingApp"
type: "MiniProject"
post: true
text: true
date:   2021-05-15
author: "Jiwoo Lee"
comments: true
---

<br><br>
이번엔 명언 앱이다. 데이터(명언, 이름)를 서버를 통하거나 앱 자체 하드 코딩이 아닌, <br>
AWS Remote Config를 통해 받아올 수 있고, 또 변수에 따라서 보여지게 설정할 수 있다. <br><br>
여러모로 알아두면 실제 프로젝트에서도 <br>간단한 공지사항이던지 버튼 Visible 처리 등등을 쉽게 적용할 수 있을 것 같아 정리해두고 가려고 한다.

<br>
🔽 앱 동작
<img src="https://user-images.githubusercontent.com/59545680/118363491-80481f00-b5cf-11eb-9351-35f61196ff82.gif" width="32%">

<br><br>

## 1. Remote Config
<img src="https://user-images.githubusercontent.com/59545680/118363727-c2be2b80-b5d0-11eb-810b-3859365beb18.png" width="90%">

<br>
매개변수 추가 버튼을 통해 간단하게 추가하고,<br>
`Firebase.remoteConfig.getString("quotes")`를 통해 가져올 수 있다.<br>
다만, 맹신해서는 안되는 게, 데이터를 읽어오는데 시간이 생각보다 걸리고<br>
외부로 노출해서는 안되는 데이터는 사용하지 않는 것이 좋을 것 같다.

<br><br>

## 2. PagerAdapter 무한 스크롤 처리
대부분의 adapter를 쓸 때, `override fun getItemCount() = items.size`로 사용한다.<br>
이 방법은 item의 갯수만큼 리스트를 보여주게 하는데, <br>
명언앱 같은 경우는 계속 오른쪽 또는 왼쪽으로 스크롤이 되도록 처리해야한다. 따라서 아래와 같이 처리한다.

```kotlin
override fun onBindViewHolder(holder: QuoteViewHolder, position: Int) {
      val actualPosition = position % quotes.size //무한 스크롤 속임
      holder.bind(quotes[actualPosition], isNameRevealed)
  }
  
override fun getItemCount() = Int.MAX_VALUE //개수를 최대치로 
```

<br>
위 코드만 추가하면, 제일 처음 앱 진입시 왼쪽으로 스크롤 되지 않는 문제점이 있다.<br>
따라서 이를 해결하기 위해 adapter 세팅시 아래와 같이 첫 item의 index을 중간에 두게 설정해준다.<br>
```kotlin
viewPager.setCurrentItem(adapter.itemCount / 2, false)
```

<br><br>
## 3. 코드
전체 코드는 [여기서](https://github.com/jwl-97/goToBasic/tree/main/7_famousSayingApp) 볼 수 있다.
<br><br>
