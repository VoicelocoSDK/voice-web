# Voiceloco SDK - Web 시작하기

> ## 시작하기
  
  Demo : https://api.voiceloco.com/demo
* ### Supported Browser
  Voiceloco SDK - Web은 Webrtc를 지원하는 브라우져 Chrome, Opera등에서 작동합니다.
 
* ### Web SDK 설정 - Static import

  Voiceloco의 Call SDK를 사용하기 위해서는 아래와 같이 voicelocojs_min.js를 HTML파일에 추가해야 합니다.

  ```
  <script src="import: https://github.com/VoicelocoSDK/voice-web/blob/master/voicelocojs_min.js"></script>
  ```

* ### AccessToken 요청 및 미디어 서버 등록

  VoiceLoco Call SDK를 사용하기 위해서는 AccessToken을 VoiceLoco 서버로부터 발급받아야 합니다. 
  AccessToken은 사용자의 인증키로 사용이 되며, 보안을 위해 AcessToken은 자체 서버에서 구현하여 발급 받아야 합나다.
  테스트 용 SDK에서는 AccessToken 없이 사용할 수 있도록 개발 되었습니다.


  ```
    Register register = Register.getInstance();
    register.start(MainActivity.this, id, appId, result, fcmToken);
  ```

  .

* ### 사용법

  ## Register

  ```
   var config = {
            userId: userId,
            appId: "testAppId",
            accessToken: "",

            //for video - optional
            video: {
                local: "video_local",
                remote: "video_remote"
            }
        }
   var voiceApi = new VoicelocoJs(config);
   
  ```

  ## Call

  # 전화 발신
  ```
  //1. Audio Call
  voiceApi.call(remoteUserId)

  //2. Video Call
  voiceApi.call(remoteUserId, "video");
  ```

  # 발신 취소 / 전화 끊기
  ```
  voiceApi.hangup();
  ```

  # 전화 받기
  ```
  voiceApi.accept();
  ```

  # 전화 거절  
  ```
  voiceApi.reject();
  ```

  ## Event Handler
  
  #General Event
  ```
  voiceApi.on_event = function (e) {
            // event handling
            // e.type, e.message, e.reason

            switch (e.message) {
                case "initiating":
                    break;
                case "ready":
                    break;
                case "connecting":
                    break;
                case "connected":
                    break;
                case "busy":
                    break;
                case "terminating":
                    break;
                case "terminated":
                    break;
                case "new_call":
                    break;
            }

        };
  ```

  #Error Event
  ```
  voiceApi.on_error = function (e){
            //error handling
            // e.type, e.message, e.reason
            window.console.info(e.message);
  };
  ```




