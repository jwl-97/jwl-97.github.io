---
layout: post
title:  "cameraX의 이것 저것"
type: "Android"
post: true
text: true
date: 2022-01-18
author: "Jiwoo Lee"
comments: true
---

<br><br>
## 1. 배경
작년 이맘 때 쯤, 카메라를 사용하는 서비스를 운영 했었다.<br>
증명을 위해 여러장의 사진(원본)을 찍어 s3로 올려야하는데 이 부분에서 업로드 지연, 사용자의 네트워크 상태로 인한 실패 등 여러 이슈들이 있었고, 그게 그 당시의 큰 숙제였다.<br>

어떻게 하면 사용자의 불편함을 덜면서 사진을 전송할 수 있을까 고민하고 결과를 낼때쯤.. 프로젝트가 무산되어 결국 제대로 적용해보지 못하고 덮어두었었다.

<br>
이번에 위와 결이 비슷한 앱을 개발 검토하게 되면서 작년에 고민했던 것들을 다시 떠올려보았다.<br>
작년과 크게 다른 것은 올려야하는 사진의 수가 두 배 이상이라는 것.<br>

사용자 특성상 '찍는 속도', '업로드 속도'가 중요할 것이라고 생각했고, <br>
기존에 사용하던 Intent-startActivityForResult 구조가 아닌, cameraX를 사용하면 사진 촬영에 소요되는 시간을 줄일 수 있지 않을까 싶어 적용을 해봤다.

<br>
-) 다른 androidX 라이브러리 처럼 단순히 가져다 쓰면 되지 않을까? 했던 예상과는 다르게,,,,<br>
3A 개념 이해부터 불친절한 camaraX document(모든 예제들이 camara2 및 camaraX 내부가 모두 camara2 기반)까지 생각지 못한 벽이 많아서 여기에 정리해 두고자 한다.



<br><br>
<hr><br>

## 2. 
### 2-1. 
* 


<br><br>
<hr><br>

## 3. 코드
전체 코드는 [여기서](https://github.com/jwl-97/camera-samples/tree/main/CameraXBasic/app/src/main/java/com/android/example/cameraxbasic) 볼 수 있다.
<br><br>
