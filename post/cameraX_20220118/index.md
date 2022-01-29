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

## 2. 3A 설정
### 2-1. 3A란?
<br><br>

### 2-2. 3A값 세팅
AWB, AF, AE 각각의 모드를 명시적으로 바꿀수 있다.<br>
바꿀 수 있는 모든 상태값은 [이 링크](https://source.android.google.cn/devices/camera/camera3_3Amodes?hl=ko)에서 볼 수 있으며, 대부분 
빠른 자동 초점 조절을 위한 AF_MODE_CONTINUOUS_PICTURE을 많이 사용한다.<br><br>

기존 camera2에서는,<br>
사진을 찍기위해 생성한 captureRequest의 Builder에 set하여 모드를 세팅하면 되었는데,
~~~ kotlin
captureBuilder.set(CaptureRequest.CONTROL_AE_MODE, CaptureRequest.CONTROL_AE_MODE_ON);
~~~

<br>
cameraX에서는 preview를 선언하기 전 Extender를 사용해서 미리 세팅한다.
~~~ kotlin
// Preview
val previewBuilder = Preview.Builder()

val previewExtender = Camera2Interop.Extender(previewBuilder)
previewExtender.setCaptureRequestOption(
    CaptureRequest.CONTROL_AF_MODE, CaptureRequest.CONTROL_AF_MODE_CONTINUOUS_PICTURE
)

val preview = previewBuilder.setTargetAspectRatio(screenAspectRatio)
    .setTargetRotation(rotation)
    .build()
~~~

<br><br>
또한, Extender에 setSessionCaptureCallback 콜백함수를 달아서, <br>
리턴되는 [TotalCaptureResult](https://developer.android.com/reference/android/hardware/camera2/TotalCaptureResult)를 통해 3A 상태를 확인할 수 있다.<br><br>
프로젝트에서는 촬영 가능 상태값을 정의해두고 리턴값에 따라 촬영 버튼의 클릭 가능 여부(enable)를 바꾸어주었다.

~~~kotlin
previewExtender.setSessionCaptureCallback(object : CameraCaptureSession.CaptureCallback() {
    override fun onCaptureCompleted(
        session: CameraCaptureSession, request: CaptureRequest, result: TotalCaptureResult
    ) {
        super.onCaptureCompleted(session, request, result)

        val afState = result.get(CaptureResult.CONTROL_AF_STATE)
        val aeState = result.get(CaptureResult.CONTROL_AE_STATE)
        val awbState = result.get(CaptureResult.CONTROL_AWB_STATE)
        val lensState = result.get(CaptureResult.LENS_STATE)
        Log.d(
            "TEST",
            "afState : $afState, awbState : $awbState, aeState : $aeState, lensState : $lensState"
        )

        val value = afState == CaptureResult.CONTROL_AF_STATE_PASSIVE_FOCUSED
                && awbState == CaptureRequest.CONTROL_AWB_STATE_CONVERGED
                && lensState == CaptureRequest.LENS_STATE_STATIONARY

        if(value){
            //shutter on
        }else{
            
        }
    }
})
~~~

<br><br>
<hr><br>

## 3. 코드
전체 코드는 [여기서](https://github.com/jwl-97/camera-samples/tree/main/CameraXBasic/app/src/main/java/com/android/example/cameraxbasic) 볼 수 있다.
<br><br>
