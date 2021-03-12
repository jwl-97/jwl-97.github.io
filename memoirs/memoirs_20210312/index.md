---
layout: post
title:  "예비 2년차 회고록"
type: "2020"
memoirs: true
text: true
date:   2021-03-12
author: "Jiwoo Lee"
comments: true
---
<br>

## 1. 블로그 시작의 이유
취준시절 제외하고는 블로그 작성의 필요성을 느끼지 못했었는데<br>
이번에 새 안드로이드 개발자분이 들어오셔서 코드 리뷰를 하다보니, <br>
그리고 안드로이드 개발자회의(장황해 보이지만 CTO 이사님 제외 두명!)를 제안하고 나니 이력정리의 필요성을 느꼈다. <br>
그 전에 겸사겸사 회사에 들어오고 느꼈던 것들을 정리하면 좋을 것 같아서 약 11개월간의 회고록을 작성하고자 한다.<br><br>

## 2. 팀의 시작
2020년 4월, 처음 팀을 들어왔을 때는 4명이 전부였다.<br> 
각각 서버, 웹, ios, aos(나) 였고, 이사님 총괄이었다.<br>
참고로 현재는 운영팀과 사업기획팀이 추가되어 현재는 8명으로 구성되어있다.<br><br>  간단히 내가 맡은 앱을 소개하자면, <br>
탁송을 요청하는 요청앱([렌톡](https://play.google.com/store/apps/details?id=kr.co.avara.rentalk&hl=ko))과
그 탁송을 수행하는 앱([수퍼드라이버](https://play.google.com/store/apps/details?id=kr.co.avara.rendrivers))가 있다.

입사직후 당장 2개월 뒤 앱 출시 일정이 잡혀있었고, 나에게 주어진 건 두개의 앱중에 하나인 수퍼드라이버였다.<br>
나름 코틀린을 좋아했던 터라 자바로 되어있던 레거시 코드를 코틀린으로 바꾸었고 새로운 기능도 넣고.. <br>
되돌아보면 지금까지 통틀어서 가장 바빴던 시간이었다.<br>

예상했겠지만 상용에 나가면서 펑펑 터졌고 겪을 수 있는 모든 실수들을 다 한 것같다... <br>
다행이 혼내고 다그치시기보단 필드테스트란 핑계로,, 바람도 쐬게 해주시고 분위기 환기도 해주시면서 믿고 맡겨주셨다.<br><br>

## 3. 인식의 변환
### a. 신기술에 대한 욕심
이게 모든 개발자가 그런건진 몰라도 신기술에 대한 욕심이 있었다. <br>
기술에 대한 욕심은 물론 좋은것이지만 기본기가 탄탄해야 그 욕심이 긍정적으로 작용하는 건데 마냥 신기술만 쫓았던 것 같다.<br><br>
처음 레거시 코드를 봤을때 기교도 없고, 패턴도 없는 무난한 코드였다. 주석도 없었는데 마냥 쭉쭉읽어졌다.<br>
사실 이게 엄청나게 대단한 코드(가독성무엇)였는데… 그 당시에는 이것도 넣고 싶고 저것도 넣고 싶고 그냥 신기술을 쓰고 싶었다.<br>
마냥 mvvm적용해보고 rx적용하고 그랬다가 다시 빼고.. 일단 적용하고 봤다.<br>

그럴때 마다 이사님은 기술 적용을 막으시진 않앗지만, 사용해야되는 이유와 기본에 대한 중요성을 강조해주셨다.<br>
라이브러리를 쓰더라도 그게 어떻게 돌아가는지 알고 사용하고,
패턴을 쓰더라도 왜 필요한지를 알고 사용하라고 조언해주셨다.

이제는 어깨넘어 배워온대로.. 라이브러리는 최대한 적게,  최소한 어떻게 돌아가는지는 파악하고 사용하고, <br>
패턴도 유행이라고 마냥 따라가기보단 적용할 이유를 찾아가며 사용하자(예를 들어 테스트 코드작성을 위해 뷰와 로직을 분리하기위한 mvp)라고 관점이 변하게 되었다. <br><br>

이 얘기완 별개로,
mvvm을 속도면에서 좋은 것같아서 렌톡에서 가장 많이 접근하는 화면에 적용해 봤었는데,<br> 
얼마전 코드리뷰를 준비하다보니 너무 가독성이 없단 것을 깨달았고, 다시 원복했다. <br>
사실 그렇게 많은 사람들이 사용하는 이유가 있을 것같긴한데 아직은 매력적인 이유를 모르겠다.
내 생각엔 지금의 앱엔 아직까지는 필요하지 않을 것같다. 대신, 요즘 테스트코드를 작성하면서 ui에 대한 테스트뿐아니라 실제 로직에 대한 테스트도 있으면 안정성이 높아질거같아서 뷰와 로직을 분리하기위해 mvp 패턴을 적용중이다.<br><br>

### b. 관점의 전환
입사 면접부터 리더들이 강조하던 것이 고객관점사고(항상 고객이 바꾸라면 바꾸는 거다)와, 투명한 커뮤니케이션을 강조해왔다.<br> 

그래서 어느샌가 바꾸면 바꾸는 거지. 시간만 넉넉하게 주세요. 라는 인식이 생겼는데 이게 이후 들어온 팀원들에겐 신선했나보다. 이런 팀원들은 처음봤다며 놀라워했었다.
이후 들어온 팀원들은 대부분 경력직이었고 운영팀과 사업기획, 디자인 등 비개발직군이었다.<br> 

그들의 겪었던 개발팀은 무조건 안돼요를 외쳤다고는 하는데.. 사실 그것도 이해를 못하는바는 아니다.<br> 
내가 인턴할때 봤던 개발자들은 회사가 갑이 아닌 을이였으며 늘 기한과 잦은 요구사항변경, 야근에 휩쓸려다녔다.<br> 
사실 개발팀은 어느쪽에서도 욕먹기 좋고 가장 데드라인과 맞닿아 있는 직군이기 떄문에 안된다..를 달고 사는것도 정말 이해된다.<br>

바꾸면 바꾸는 거지라고 생각할 수 있기까지, 리더들의 지속적인 가이드와 많은 시행착오들이 있었지만, <br>
`일하는 방식`의 영향도 한 몫했다.

1. 언제까지 해주세요가 아닌 언제까지 가능해요? 가 질문이었고,<br> 
2. 왜 그 기능이 필요한지(서비스에 도움이 되거나 사용자가 불편해한다면)를 충분히 이야기했고,<br>
3. 만약 그 기능이 기술적으로 오래걸리거나 어렵다면, 왜 안되는지 그리고 대안을 제시했다.
4. 또한, 모든 구성원이 개선사항회의에 참여하여 더 좋은 방안과 그 안건에 대한 개발여부을 논의했다.

그러다보니 새로온 팀원들에게 개발은 하면된다. 바꿀 이유가 있다면(서비스에 도움이 되거나 사용자가 불편해한다면) 바꾸는 거다. 시간만 달라ㅋㅋㅋ 라고 말하고 다니곤 한다.<br><br><br>

사실 이렇게 생각하기까지 많은 `시행착오`가 있었는데. <br>바로 비개발직군이 들어오면서 부터이다.<br>

서비스를 일단 출시하는게 목표였기때문에 code & fix로 진행되다가 갑자기 SRS며 문서며 개선사항회의며 절차가 늘어나기 시작했다. 개발자임에도 불구하고(이때는 이렇게 생각했다. 물론 지금은 아님) 들어오는 멤버들에게 앱소개며
모든 서비스 관련 질문에 대답을 해야했고 업무시간내 100%이던 개발시간이 채 50%도 안되며 할 일이 늘어나기 시작했다.<br>

내가 왜 이걸해야되지.. 개발시간 없어지는데.. 나 할 일 많은데.. 이렇게 생각했던 것 같다.<br>

이 생각이 깨진게 한 한달 쯤 후 부터였는데, <br>
기존의 개발해주세요. 하면 개발하던 수동적이였던 일에서 프로세스에 따라 개선 의견을 제안하고 그 의견에 대한 개발여부 및 보완점을 다같이 결정하게 되는 것으로 바뀌면서 일이 능동적으로 바뀌게 되었다.<br>

또한, 리더들은 개발 직군한테는 사업회사다 바꾸자하면 바꾸는거다 라는 인식을 심어줬듯,
반대로 비개발 직군에게는 개발자의 시간은 금이다. 꼭 필요한것만 요구해야한다. 요구하기전에 고객적 관점에서 꼭 필요한 것인지. 데이터로, 상황으로 개발자를 설득해야한다며 인식을 심어줬다.

덕분에 나는 이 프로세스가 결코 내 개발 시간을 뺏는것이 아니며
오히려 내 개발시간을, 업무를 줄이기 위한 과정이라는 것을 깨달았고 참 좁은 관점을 가지고 있었구나라고 느꼈다.<br><br><br>

## 4. 마무리

이런 인식의 전환으로 내 스스로도 11개월만에 많이 성장함을 느꼈고 
주변에 좋은 사람들과 성취감을 느끼면서 일한다는 것이 참 운이 좋다고 생각한다.
하지만, 좋은 것이 있으면 나쁜 것이 있듯 나도 부족함을 느끼는 부분이 있었다.

바로 기술적인 외로움이었다.
개발도 다 파트별로 담당제로 나누어져있고 서로의 영역이 너무 다르다보니(그나마 ios는 비슷하지만 충족시켜주지는 못한다) 이게 돌아가긴 하는데 이게 맞는 코드일까하는 의문도 있었고 신기술을 바로 적용하진 않더라도 알고 공유할 수 있는 러닝메이트가 있었으면 싶었다.
코로나 시국이라 커뮤니티나 밖으로 나다니지 못한 것도 한 몫했다.

다행히 최근에 다른 팀이지만(같은 그룹) 안드 신입개발자가 오셨고 
이야기를 나눠보니 내가 딱 처음 시작했을 떄 재미.. 열정 이런게 가득차신 분이었다.
매주 30분씩 돌아가면서 자유주제로 aos개발자 회의를 하면 어떨까요? 라며 제안을 했고
하는김에 블로그에 남겨놓으면 나의 성장(이라하고 이직준비라 읽는다)에 도움이 될 것같아 작성하려고 한다.

