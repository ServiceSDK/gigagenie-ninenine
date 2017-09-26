# GiGA Genie 구구단
GiGA Genie 서비스 SDK를 이용한 구구단 게임입니다.

### 사용한 API

Service API는 매개변수인 Callback 함수를 통해 요청 결과를 수신합니다.

 1. `init`으로 API를 초기화
   * Service SDK 이용을 위해 반드시 초기화를 진행해야 합니다.
   * options은 다음과 같이 설정합니다.
     * options.apikey: 개발자 사이트에서 받은 api key
     * options.keytype: G-Box 상용키 GBOXCOMM (string)
   * callback으로 초기화 성공 여부를 수신
     * result_cd: 200(success)이 아닌 경우 API는 동작하지 않습니다.

        function init(){
          var options={};
          options.apikey="";
          options.keytype="GBOXCOMM";
          gigagenie.init(options,function(result_cd,result_msg,extra){
            if(result_cd===200){
              status='IS';
              appid=extra.appid;
              console.log('Initialize Success, appid:'+extra.appid);
              startNineNine();
            };
          });
         }
    

 2. `voice.getVoiceText`으로 음성인식을 요청
  * options은 다음과 같이 설정합니다.
     * options.voicemsg: 음성인식 요청 텍스트 (string), TTS 후 요청 수행
  * callback으로 음성인식 결과를 수신
     * result_cd가 200(success)인 경우 다음의 값이 전달됩니다.
     * extra.voicetext: 음성인식 결과 텍스트 (string)

        function startNineNine(){
          var options={};
          var numbers=getNumber();
          options.voicemsg=numbers[0]+' '+numbers[1];
          var solution=numbers[0]*numbers[1];
          gigagenie.voice.getVoiceText(options,function(result_cd,result_msg,extra){
            if(result_cd===200){
              console.log(extra.voicetext+':'+solution);
              if(parseInt(extra.voicetext)===solution){
                alert(extra.voicetext+" 정답입니다");
              } else {
                alert(extra.voicetext+" 틀렸습니다.");
              }
            } else {
              alert("다시해보세요");
            }
            startNineNine();
          });
        };
        

	
 3. `voice.stopTTS`으로 음성인식을 중단
  * stopTTS의 매개변수인 callback을 통해 

        function stopTTS() {
          alert("음성인식 중단 요청");
          var options={};
          gigagenie.voice.stopTTS(options,function(result_cd, result_msg, extra) {
            if (result_cd==200) {
              alert("음성인식 중단 성공");
            }
            else if (result_cd==404) {
              alert("음성인식 실행 중이 아님");
            }
            else {
              alert("음성인식 중단 실패: " + result_msg);
            }
          });
        }


 4. `voice.onRequestClose`으로 서비스 종료 수신


        function stopTTS() {
          alert("음성인식 중단 요청");
          var options={};
          gigagenie.voice.stopTTS(options,function(result_cd, result_msg, extra) {
            if (result_cd==200) {
              alert("음성인식 중단 성공");
            }
            else if (result_cd==404) {
              alert("음성인식 실행 중이 아님");
            }
            else {
              alert("음성인식 중단 실패: " + result_msg);
            }
          });
        }



 5. `media.onMuteRequest`으로 Mute 요청 이벤트 수신

        gigagenie.media.onMuteRequest=function(extra){
          if(extra) console.log("Mute!");
          else console.log("unMute!");
		};








































































