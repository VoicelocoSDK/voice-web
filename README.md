# Voiceloco SDK - Web 시작하기

> ## 시작하기
  Voiceloco SDK Web은 Web기반 Application에 실시간 Voice/Video 기능을 추가 해줍니다.
  
  Voiceloco Api Homepage : https://api.voiceloco.com
  
  Demo: https://api.voiceloco.com/demo
  
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
 
* ### 사용법

  ## Register
  Voiceloco SDK의 Call 기능을 사용하기 위한 과정으로써, Config validation, AccessToken 인증, Call에 필요한 초기화 작업을 수행한다.
  ```
   var config = {
            userId: userId, //사용자의 userId
            appId: "testAppId", //Voiceloco SDK를 적용한 어플리케이션의 appId
            accessToken: "", //사용자 인증에 필요한 key로써 테스트용 SDK에는 필요하지 않음

            //for video - optional
            video: {
                local: "video_local", //사용자의 화면을 표시할 video element의 id
                remote: "video_remote" //상대방의 화면을 표시할 video element의 id
            }
        }
   var voiceApi = new VoicelocoJs(config);
   
  ```

  ## Call

  #### 전화 발신
  상대방의 userId를 입력하여 call 함수를 호출. Video Call인 경우 "video" 인자값을 추가로 입력한다.
  ```
  //1. Audio Call
  voiceApi.call(remoteUserId)

  //2. Video Call
  voiceApi.call(remoteUserId, "video");
  ```

  #### 발신 취소 / 전화 끊기
  현재 발신 시도중인 Call 연결을 취소하거나, 현재 Call이 연결된 상태에서 통화 종료를 할 때 호출한다.
  ```
  voiceApi.hangup();
  ```

  #### 전화 받기
  Call 요청을 수락할 때 호출한다.
  ```
  voiceApi.accept();
  ```

  #### 전화 거절  
  Call 요청에 대한 거절을 할 때 호출한다.
  ```
  voiceApi.reject();
  ```

  ## Event Handler
  
  ### General Event
  정상적인 Call 시나리오에 대한 Event 리스너로써, 최초 Call 발신으로부터 시작하여 Call 종료까지 각각의 상태에 대한 처리를 위한 함수

  | message | 설명 |
  | -------- | -------- |
  | initiating | Api 초기화를 시작함. Config Validation 및 AccessToken 인증 과정을 수행|
  | ready | Api 초기화가 정상적으로 수행되어, 정상적으로 Call 발신/수신을 할수 있는 상태|
  | connecting | Call 발신을 시작하는 상태 |
  | connected | 정상적으로 Call 연결이 된 상태 |
  | busy | 상대방이 현재 통화중인 상태 |
  | terminating | Call 종료를 시작하는 상태|
  | terminated | Call 종료에 대한 작업이 정상적으로 처리된 상태 |
  | new_call | 새로운 Call이 요청된 상태 |  

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
  ### Error Event
  AccessToken 인증 오류, Config Validation에러 및 잘못된 Api사용 등으로 발생하는 에러에 대한 event 리스너.
  ```
  voiceApi.on_error = function (e){
            //error handling
            // e.type, e.message, e.reason
            window.console.info(e.message);
  };
  ```
