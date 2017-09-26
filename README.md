# gigagenie-ninenine
GiGA Genie 서비스 SDK를 이용한 구구단 게임입니다.

### 사용한 API

 1. `init`으로 API를 초기화

        function init(){
          var options={};
          options.appid='';
          options.apikey="";
          options.keytype="";
          gigagenie.init(options,function(result_cd,result_msg,extra){
            if(result_cd===200){
              status='IS';
              appid=extra.appid;
              console.log('Initialize Success, appid:'+extra.appid);
              startNineNine();
            };
          });
        }
    


 2. Voice API `voice.getVoiceText`으로 음성인식을 요청
  * getVoiceText의 매개변수인 callback을 통해 음성 이벤트를 수신합니다.
  * extra.voicetext: 음성인식 된 text (string)


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














































"# gigagenie-ninenine" 
"# gigagenie-ninenine" 
