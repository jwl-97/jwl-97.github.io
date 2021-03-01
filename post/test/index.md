---
layout: post
title:  "안드로이드 죽지않는 서비스(Immortal Service) 구현"
type: "Android"
post: true
text: true
date:   2021-03-01
author: "Jiwoo Lee"
---

<br>
## 배경

내가 담당하고 있는 앱 중 하나인 [수퍼드라이버](https://play.google.com/store/apps/details?id=kr.co.avara.rendrivers)의 가장 중요한 기능 중 하나는 `위치서비스`다.<br>
앱 출시 초창기(20년 6월~8월) 위치 서비스는 가장 큰 이슈중에 하나였다. <br>

우리 앱은 드라이버의 위치를 일정 간격으로 받아 주변의 콜을 안내해주고,<br>
탁송 수행 중 드라이버의 현재위치를 발주처에게 알려주기 위해 위치서비스가 꼭 필요하다.<br> 

단순하게 앱 속  `출근하기`로 서비스를 키고, `퇴근하기`로 서비스를 끄는데 <br>
이 `퇴근하기`를 하루에 한 번씩 하는 것이 아니라 일주일이 될지, 한 달이 될지 영영 하지 않을지.. 모르는 것이었다.<br>

따라서 시간이 일주일 이상 흘러감에 따라 정확하지 않은 위치 데이터가 넘어오거나 출근상태임에도 불구하고<br> 
위치데이터가 들어오지 않는 등 여러가지 변수가 있어 위치 서비스의 안정성이 크게 떨어졌다.<br>

이 때, 이사님(@Ryan)의 제안으로 Immortal Service를 적용하게 되었다.<br><br>

## Immortal Service
단순히 죽지 않는 서비스이다. <br>
메인 서비스를 A라고 한다면, 서브 서비스 B를 만들어서<br>
서로서로 감시하여 onDestroy()가 호출된다면, AlarmManager를 통해 다시 서비스를 킨다.<br>

따라서 서비스 A가 모종의 이유로 죽으면,<br>
AlarmManager가 호출되어 서비스B가 실행되고 다시 서비스A가 실행된다.<br>
반대로, 서비스 B가 죽는다면 서비스A를 통해 서비스B가 다시 실행된다.

말로써 푸니까 엄청 복잡해보이는데 코드로 보면 되게 간단하다.<br>

```
// Service A
class ServiceA : Service() {
    override fun onStartCommand() {      
        if (intent?.getStringExtra("type")이 B이면){
            startService(서비스B)
        }
    }

    override fun onDestroy() {
        // 알람 매니저 호출
    }

    private fun callAlarmManger() {
        // 알람 매니저 등록
    }
}

class AlarmReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        if(버전 오레오 이상이면){
            intent.putExtra("type", "A")
            startForegroundService(서비스B)
        }else {
            startService(서비스A)
        }
    }
}
```

```
// Service B
class ServiceB : Service() {
    override fun onStartCommand() {      
        if (intent?.getStringExtra("type")이 A이면){
            startService(서비스A)
        }
    }

    override fun onDestroy() {
        // 알람 매니저 호출
    }

    private fun callAlarmManger() {
        // 알람 매니저 등록
    }
}

class AlarmReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        if(버전 오레오 이상이면){
            intent.putExtra("type", "B")
            startForegroundService(서비스A)
        }else {
            startService(서비스B)
        }
    }
}
```
<br>

## 서비스 종료
추가로, 서비스 종료하는 건 preIsRealStop 변수를 preference에 추가하여 stopService를 할때 <br>
preIsRealStop값도 같이 변경하여 알람 매니저 호출을 하지 않으면 정상적으로 종료가 된다.
<br>
```
// MainActivity
PreferenceUnit.getInstance().preIsRealStop = true //
stopService(Intent(applicationContext, ServiceA::class.java))
stopService(Intent(applicationContext, ServiceB::class.java))
```

```
// In Service
if (!PreferenceUnit.getInstance().preIsRealStop) {
    callAlarmManger() //
}
```
<br>
## 코드
전체 코드는 [여기서](https://github.com/jwl-97/Android_immortalService) 볼 수 있다.
<br><br><br>
