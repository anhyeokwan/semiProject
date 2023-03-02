# Near By Doctor

## 개요
비대면진료와 약국처방이 가능한 쉽고 편리한 병원약국 서비스

## 계획의도
- 어디서든지 쉽고 빠르게 비대면 진료를 받을 수 있는 병원, 약국 진료서비스를 구축
- 전국 어디서든 내가 있는 곳에서 약처방을 받을 수 있고 평소에도 건강을 챙길 수 있도록 의사, 약사와 함께 소통할 수 있는 웹사이트를 제공

## 유사사이트
![image](https://user-images.githubusercontent.com/77394673/222446372-48bb99b1-3c91-4a7d-8a00-9280c1f4002d.png)


## 개발목표
1. 기존에 없던 PC 비대면 진료시스템
- 기존의 다른 비대면 진료 시스템은 대부분 모바일 어플리케이션으로 구성되어있기에 PC환경으로 이용가능하도록 구현

2. 누구나 이용 가능하게 보기쉬운 UI와 사용법
- 인터넷 이용이 낯설 수 있는 어르신도 편한 사용법과 모든 메뉴가 한눈에 들어올 수 있는 깔끔한 UI디자인

3. 즉각적인 피드백과 진료해줄 담당의를 선택할 수 있는 권리
- 언제든 이용가능한 신고페이지를 통해 불쾌한 의사, 약사, 회원을 신고하면 신고받은 횟수를 표시하는 등 즉각적인 피드백을 수용
  그 시간에 진료중인 의사한테 어쩔 수 없이 받아하는 대면진료와 달리 진료가능한 의사들과 의사의 담당분야를 보고 선택할 수 있는 기능 구현
  
  4. 누구나 이용가능한 건강상담에 대한 커뮤니티 게시판
  - 모든 회원이 자신의 건강꿀팁이 있다면 공유가능한 게시판
  - 추천을 많이 받고 의사들이 인정하는 건강꿀팁이라면 모두가 공유할 수 있도록 사용
  
  ## 개발환경
  - 운영체제 : window 10
  - 개발도구 : Eclipse
  - DBMS : Oracle DB-SQL Developer
  - Server : Apache Tomcat v9.59
  - Language : Java, HTML5, CSS3, JavaScript
  - 디자인툴 : Bootstrap, W3c
  - Framework : Jquery, ajax
  - API : 메일API, 네이버지도API
  
  ## 상세기능
 ![image](https://user-images.githubusercontent.com/77394673/222452736-83e4470d-416a-432b-a20e-6725b29b3dec.png)
 ![image](https://user-images.githubusercontent.com/77394673/222452908-5d8ebec5-c7ff-41d8-9c71-c8aa02e08962.png)

## 일정
2022.09.13 ~ 2022.09.26
'
## 내 구현기능
1. 회원가입
2. 병원예약

## 1. 회원가입
![image](https://user-images.githubusercontent.com/77394673/222460227-dfdbbeee-faa6-4d78-bb1a-33fae5445814.png)
![image](https://user-images.githubusercontent.com/77394673/222460257-3110d4c6-fc0e-4823-ac3e-ef96a0404d60.png)

#### 구현기능설명
- 메인페이지의 회원가입을 누르면 다음과 같은 약관 동의 페이지가 나옵니다. 
  약관동의 페이지는 모든 체크박스에 체크가 되면 넘어가고 모두 되어있지 않으면 메시지가 나오면서 넘어가지 않게 되어있습니다. 
  취소를 누르면 메인페이지로 넘어가고 다음을 누르면 회원 정보를 입력하는 창이 나옵니다.

- 회원정보 입력창은 각 입력값에 유효성검사를 걸어두었습니다. 
  유효성 검사에 맞지 않으면 빨간색으로 어떻게 입력하라고 각 부분에 표시가 됩니다. 
  그리고 이메일인증을 할 수 있으며 모든 값이 알맞게 입력이 되면 회원가입이 가능하게 됩니다.
  - 메일 api
  ```java
  boolean result = false;
		
		Random r = new Random();
		StringBuilder sb = new StringBuilder(); // String 배열
		
		// 0~3
		// 0: 숫자  1: 영어대문자  2: 영어소문자
		for(int i = 0; i < 8; i++) {
			int flag = r.nextInt(3);
			
			if(flag == 0) {
				// 랜덤숫자
				int ranNum = r.nextInt(10);
				sb.append(ranNum);
			} else if(flag == 1) {
				// 영어 소문자
				char ranSmall = (char)(r.nextInt(26) + 65);
				sb.append(ranSmall);
			} else if(flag == 2) {
				// 영어 대문자
				char ranBig = (char)(r.nextInt(26) + 97);
				sb.append(ranBig);
			}
		}
		
		Properties prop = System.getProperties();
		prop.put("mail.smtp.host","smtp.gmail.com");
	    prop.put("mail.smtp.port", 465); //포트설정
	    prop.put("mail.smtp.auth", "true");
	    prop.put("mail.smtp.ssl.enable", "true");
	    prop.put("mail.smtp.ssl.trust","smtp.gmail.com");
	    prop.put("mail.smtp.starttls.required", "true");
	    prop.put("mail.smtp.ssl.protocols", "TLSv1.2");
	    prop.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
		
	  //인증정보설정(로그인) javax.mail-Session
	      Session session =Session.getDefaultInstance(prop, 
	            new Authenticator() {
	               protected PasswordAuthentication getPasswordAuthentication() { //구글 아이디 패스워드
	                  PasswordAuthentication pa = new PasswordAuthentication("bomkh123","oplntjofdzxwuvaf");
	                  return pa;//여기까지가 구글에서 로그인 한 시점
	            }
	         }   
	      );
	      
	      // 메세지를 전송하는 객체
	      MimeMessage msg = new MimeMessage(session);
	      try {
	    	// 이메일 작성
			msg.setSentDate(new Date());
			// 보내는 사람 정보
			msg.setFrom(new InternetAddress("bomkh123@gmail.com", "nearByDoctor를 방문해주셔서 감사합니다."));
			// 받는 사람 정보 객체(email)
			InternetAddress to = new InternetAddress(email);
			msg.setRecipient(Message.RecipientType.TO, to);
			
			// 이메일 제목 설정
			msg.setSubject("nearByDoctor 인증메일 입니다.", "UTF-8");
			
			// 이메일 문구
			msg.setContent("<h1>안녕하세요. nearByDoctor입니다.</h1>"
	        		 + "<h3>인증번호는 [<span style='color:red'>" + sb.toString() + "</span>] 입니다.","text/html;charset=utf-8");
			
			// 이메일 전송
			Transport.send(msg);
			result = true;
			
	      } catch (MessagingException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (UnsupportedEncodingException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	      
	      if(result) {
	    	  return sb.toString();
	      }else {
	    	  return null;
	      }
		
	}
  ```
  - 메일 자바스크립트
  ```javascript
  let mailCode;
    	let auMail;
    	function sendMail(){
    		
    		const email = $("#email").val();
    		if(email != ""){
    			$.ajax({
        			url : "/sendmail.do",
        			type : "post",
        			data : {email : email},
        			success : function(data){
        				mailCode = data;
        				console.log(mailCode);
        				authTime();
        			}
        		});
    		}else{
    			alert("이메일을 입력하세요!");
    		}
    		
    		
    	}
    	
    	let intervalId;
    	function authTime(){
    		$("#timeZone").html("<span id='min'>3</span> : <span id='sec'>00</span>")
    		intervalId = window.setInterval(function(){
    			timeCount();
    		}, 1000);
    	}
    	
    	function timeCount(){
    		const min = Number($("#min").text());
    		const sec = $("#sec").text();
    		
    		if(sec == "00"){
    			if(min == 0){
    				mailCode = null;
    				clearInterval(intervalId);
    			}else{
    				$("#min").text(min-1);
    				$("#sec").text(59);
    			}
    		}else{
    			const newSec = Number(sec)-1
    			if(newSec < 10){
    				$("#sec").text("0" + newSec);
    			}else{
    				$("#sec").text(newSec);
    			}
    		}
    	}
    	
    	$("#authGo").on("click", function(){
    		const emailAu = $("#emailAu").val();
    		
    		if(mailCode != null){
    			if(emailAu == mailCode){
        			$("#timeZone").css("display", "none");
        			$("#authMsg").text("인증완료");
        			$("#authMsg").css("color", "blue");
        			clearInterval(intervalId);
        			auMail = true;
        		}else{
        			$("#authMsg").text("인증실패");
        			$("#authMsg").css("color", "red");
        			auMail = false;
        		}
    		}else{
    			$("#authMsg").text("인증시간 만료");
    			$("#authMsg").css("color", "red");
    		}
    	})
  ``
  
  - 입력값 유효성검사
  ```javascript
  let idStatus;
        let pwStatus;
        let pwchkStatus;
        let nameStatus;
        let phoneStatus;
        let emailStatus;
        let postStatus;
        
        
        const postReg = $("#postReg");
        $("#post").on("keyup", function(){
        	const postReg1 = /^[0-9]{6}$/;
        	
        	const postVal1 = $("#post").val();
        	
        	if(postReg1.test(postVal1)){
        		postReg.text("알맞은 생년월일입니다.");
        		postReg.css("color", "blue");
        		postStatus = true;
        	}else{
        		postReg.text("알맞지 않은 생년월일입니다.");
        		postReg.css("color", "red");
        		postStatus = false;
        	}
        })

        const emailReg = $(".emailReg");
        $("#email").on("keyup", function(){
            const emailChkReg = /^[a-zA-Z0-9]{8,12}@/;
            const emailVal = $("#email").val();

            if(emailChkReg.test(emailVal)){
                emailReg.text("");
                emailStatus = true;
            }else{
                emailReg.text("알맞지 않은 이메일형식입니다.");
                emailReg.css("color", "red");
                emailStatus = false;
            }
        })

        const phoneReg = $(".phoneReg");
        $("#phone").on("keyup", function(){
            const phoneRegChk = /^[0-9]{10,11}$/;
            const phoneVal = $("#phone").val();

            if(phoneRegChk.test(phoneVal)){
                phoneReg.text("")
                phoneStatus = true;
            }else{
                phoneReg.text("알맞지 않은 전화번호입니다.");
                phoneReg.css("color", "red");
                phoneStatus = false;
            }
        })

        const nameReg = $(".nameReg");
        $("#name").on("keyup", function(){
            const nameRegChk = /^[가-힣]{2,5}$/;
            const nameVal = $("#name").val();

            if(!nameRegChk.test(nameVal)){
                nameReg.text("알맞지 않은 이름입니다.");
                nameReg.css("color", "red");
                nameStatus = false;
            } else{
                nameReg.text("");
                nameStatus = true;
            }
        })

        const pwreChk = $(".passwordChkReg");
        $("#pwre").on("keyup", function(){
            const pwreVal = $("#pwre").val();
            const pwVal = $("#pw").val();

            if(pwreVal == pwVal){
                pwreChk.text("비밀번호가 일치합니다.");
                pwreChk.css("color", "blue");
                pwchkStatus = true;
            }else{
                pwreChk.text("비밀번호가 일치하지않습니다.");
                pwreChk.css("color", "red");
                pwchkStatus = false;
            }
        })

        const pwChk = $(".passwordReg");
        $("#pw").on("keyup", function(){
            const pwReg = /^(?=.*[a-zA-Z])(?=.*[0-9])(?=.*[~!@#$%^&*]).{8,20}$/;
            const pwVal = $("#pw").val();
            const pwreVal = $("#pwre").val();

            if(pwReg.test(pwVal)){
                pwChk.text("알맞은 비밀번호입니다.");
                pwChk.css("color", "blue");
                pwStatus = true;
            }else{
                pwChk.text("알맞지 않은 비밀번호입니다.");
                pwChk.css("color", "red");
                pwStatus = false;
            }
            
            if(pwreVal == pwVal){
                pwreChk.text("비밀번호가 일치합니다.");
                pwreChk.css("color", "blue");
                
            }else{
                pwreChk.text("비밀번호가 일치하지않습니다.");
                pwreChk.css("color", "red");
                
            }
        })

        const possibleId = $(".possibleId");
        $("#id").on("keyup", function(){
            const idReg = /^(?=.*[a-zA-Z])(?=.*[0-9]).{5,10}$/;
            const idVal = $("#id").val();

            if(idReg.test(idVal)){
                possibleId.text("알맞은 아이디입니다.");
                possibleId.css("color", "blue");
                idStatus = true;
                
            }else{
                possibleId.text("영어 대/소문자와 숫자를 포함하십시오.");
                possibleId.css("color", "red");
                idStatus = false;
            }
        });
  ```
  
  ## 2. 병원예약
  ![image](https://user-images.githubusercontent.com/77394673/222467212-ea3027a0-023a-4e0b-a212-4aef7ab5b4e8.png)
  ![image](https://user-images.githubusercontent.com/77394673/222467320-b9bff275-bc06-4249-81eb-d03416f49ee6.png)
- 날짜는 금일과 명일 중 하나를 선택할 수 있습니다. 
- 시간은 오전 오후 나누어져 있으며 라디어버튼으로 되어있어 하나면 선택할 수 있습니다.
- 증상설명은 자신의 증상을 간략하게 설명하는 박스입니다.
- 로그인이 되어있지 않으면 예약버튼이 나오지 않고 로그인 후 사용할 수 있다는 구문이 나오고 로그인 페이지로 이동할 수 있게 되어있습니다.
- 하나라도 체크되지 않거나 증상설명에 설명이 없으면 메시지가 나와 예약이 되지 않습니다.

* 아쉬운 점
- 예약테이블에 정규화가 되지 않아 예약구현 시 어려움이 있었습니다.
- 만약 다시 테이블을 구성한다면 예약테이블, 시간테이블로 쪼개서 조회를 할때는 조인을 쓰고 예약할때는 merge문을 써 더 효율적으로 구현했을거같습니다.
