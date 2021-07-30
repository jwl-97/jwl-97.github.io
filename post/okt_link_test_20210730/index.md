---
layout: post
title:  "okt 형태소 분석기 API, JAR 비교 및 단어사전(dictionary) 추가 방법"
type: "Android"
post: true
text: true
date:   2021-07-30
author: "Jiwoo Lee"
comments: true
---

<br><br>
## 1. 배경
모종의 이유로 안드로이드 앱 자체에서 특정 텍스트를 파싱해서 서버로 보내줘야 하는 일이 생겼다. <br>
그로인해 자연어 처리 도입을 고민하다가, 형태소 분석 후 명사를 가져오는 과정만 도입해도 좋을 것 같아서 도입하게 되었다.<br>

한글이 영어권처럼 띄어쓰기로만 명확하지 않고 의존부사 등 여러가지 케이스를 다 고려하기엔 비효율적이라고 생각해서,<br>
한글 형태소 분석기(okt, kkma, komoran..)를 찾았고, <br>
소요시간과 분석력을 비교해서 최종적으로 [okt](https://github.com/open-korean-text/open-korean-text)(구 twitter)로 결정했다.<br><br>

대부분의 형태소 분석 및 자연어 처리는 python 친화적..(KoNLPy👍) 이라서 <br>
안드로이드 상(kotlin)에서 연동했을 때 겪었던 어려웠던 점을 적어놓고자 한다.
<br><br>
<hr><br>

## 2. okt 연동방법
### 2-1. API
* [공식 okt 사이트](https://github.com/open-korean-text/open-korean-text)에 들어가면 가장 먼저 API 연동이 보인다.<br>
가장 간편해보이고 속도도 가장 빠른 방법이다.<br><br>
<img src="https://user-images.githubusercontent.com/59545680/127616308-f0d0d0c6-088d-4b15-aaf4-1b0d64ce41d0.png" width="65%" align="left">
<br><br><br><br><br><br><br><br><br><br><br><br>

### 2-2. maven 
* 지원 언어에 kotlin은 커녕 java도 없어서 불가<br><br>

### 2-3. 직접 JAR 만들어서 사용
*  maven을 이용한 방법은 불친절해보이기도 하고, 이것저것 할게 많아보인다.<br><br>
<img src="https://user-images.githubusercontent.com/59545680/127620269-7277dbb4-9628-4620-8fb5-4af3196f2857.png" width="52%" align="left">
<br><br><br><br><br><br><br><br>

#### 👉 <span>먼저 제일 간단한 API를 통해 원하는 결과를 내보도록 하자.</span>
<br>
<hr><br>

## 3. okt API
```
1. 방울 방울 보라색 물 풍선 한가득
2. 워라밸을 지키기엔 일정이 너무 바빠
```
위에 주어진 요청 텍스트가 있다. <br>
여기서 ```보라색 물풍선```과 ```워라밸```을 골라내고 싶다.<br>
<br><br>

🔽 결과 <br>
> 코드는 아래 7번 링크에서 볼 수 있다.<br>

```
"방울(Noun: 0, 2)",
"방울 방울(Noun: 0, 5)",
"방울 방울 보라색(Noun: 0, 9)",
"방울 방울 보라색 물(Noun: 0, 11)",
"방울 방울 보라색 물 풍선(Noun: 0, 14)", /// 제일 비슷
"보라색(Noun: 6, 3)",
"풍선(Noun: 12, 2)"
```

```
"일정(Noun: 10, 2)"
```
<br><br>
<span>
🤔 음.. ```보라색 물풍선```은 어찌저찌 가공해서 쓰면 되긴되겠지만, 원하는 바가 아니다. <br>
설령 가공한다 하더라고 모든 케이스에서 정확하게 받아올 수 있다는 보장이 없다.<br>
그리고 ```워라밸```은 아예 받아오지 못한다.
</span>
<br><br>
<hr><br>

## 4. dictionary의 존재 확인
자연어 처리의 전처리 방식은 아래와 같다.                     [관련문서](https://paul-hyun.github.io/nlp-tutorial-01-01-sequence-prediction/)

> 1. 토큰화
2. 정답데이터 입력
3. 사전(dictionary)) 생성
4. 학습

<br>
띄어쓰기, 혹은 구문단위로 토큰화를 진행하고 사전에 단어를 계속 추가하고 학습시키면서 정확도를 높이는 방법이다.<br> 
하지만, 나는 만들어진 형태소 분석기(okt)를 사용하다 보니 정해져 있는 사전을 이용한 데이터만 받을 수 있었고,<br>
okt 공식 사이트에서 따로 정의되어 있는 사전 추가 방법은 없었다.<br><br>

그러다, 사전에 원하는 단어를 추가 할 수 있다는 내용의 [한 문서](https://wikidocs.net/92961)(KoNLPy)를 보게 되었고,
<img src="https://user-images.githubusercontent.com/59545680/127625151-e99a9183-cdb6-4af1-b686-e74419c17c4e.png" width="75%" align="left">
<br><br><br><br><br><br><br><br><br><br><br>
*참고)<br> okt는 구 twitter다.<br><br>

KoNLPy 라이브러리에서 가능하다면 분명히 따로 추가할 수 있는 방법이 있을 거라 생각했고,<br>
KoNLPy github issue에서 [사전 추가 방법](https://github.com/konlpy/konlpy/issues/249)을 찾았다.<br><br>
<br>

이를 적용하기 위해서 아래의 과정으로 코드를 변경했다.
>1. API -> JAR 로 연동 방법 변경
2. dictionary 추가 후 JAR 빌드해서 적용

<br> 
👉 <span>일단, JAR로 변경하여 결과를 확인해보자 </span>
   
<br>
<hr><br>

## 5. JAR 생성 & 적용
### 5-1. JAR 생성 방법
1. 해당 프로젝트 클론<br>
   git clone https://github.com/open-korean-text/open-korean-text.git <br>
   
2. 환경세팅(mac 기준)<br>
   >환경세팅에서 애를 좀 먹어서 버전까지 남겨놓는다. <br>
   특히 scala 최신 버전은 2.13.@ 인데 해당 프로젝트에서 돌아가기 위해 2.12.@를 설치해야한다.<br>
   
   jdk(8)   [1.8.0_301]          ->    oracle 설치 <br>
   scala     [2.12.14]            ->      brew install scala@2.12 <br>
   mvn      [3.8.1]                ->       brew install mvn <br>
   <br>
   
3. mvn compile (run)
4. mvn package (JAR 생성)
<br><br><br>

### 5-2. JAR 적용 방법 in Android Studio 
1. /Users/ljw/getNotiMessageApp/app/libs 안에 위에서 생성한 jar 파일 삽입
2. jar 파일 오른쪽 클릭 후 Add as Library 클릭

3. gradle에 아래 코드 추가 <br>
   ```
   implementation'com.twitter.penguin:korean-text:4.4.4'
   implementation 'org.scala-lang:scala-library:2.12.4'
   ```
4. OktTextExample 에 적용되어있는 형식대로 함수 사용

<br><br>

🔽 결과 <br>
```
방울
방울 방울
방울 방울 보라색
방울 보라색
방울 방울 보라색 물
방울 보라색 물
보라색 물
방울 방울 보라색 물 풍선
방울 보라색 물 풍선
//// 보라색 물 풍선 ////
물 풍선
보라색
풍선
```
```
일정
```

<br>
<span>
🤔 이제 ```보라색 물풍선```은 완벽하게 얻어올 수 있다. 그러나 여전히 ```워라밸```은 받아오지 못한다.
사전에 단어를 추가해보자.
</span>

<br>
<hr><br>

## 6. dictionary 추가
1. 아까 클론했던 open-korean-text 파일에 들어간다.<br>
   cd open-korean-text
   
2. src/main/resources/org/openkoreantext/processor/util/noun/wikipedia_title_nouns.txt<br>
   에서 원하는 명사를 추가해준다. 여기서는 ```워라밸```을 추가했다.<br>
   <img src="https://user-images.githubusercontent.com/59545680/127668929-09069975-811e-42df-a3e3-69afee01e965.png" width="40%" align="left">
   <br><br><br><br><br><br>
   
3. src/main/scala/org/openkoreantext/processor/tools/DeduplicateAndSortDictionaries.scala<br>
   사전 정리 파일(인덱싱 처리)을 실행한다.
   
4. 위에서 진행했던 JAR 생성 & 적용을 해준다.

<br><br>
🔽 결과 <br>
```
워라밸
일정
```

<span>
👏 ```워라밸``` 등장 👏
</span>

<br>
<hr><br>

## 7. 코드
전체 코드는 [여기서](https://github.com/jwl-97/oktTestApp) 볼 수 있다.
<br><br>
