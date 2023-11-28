# 1조 무선네트워크 프로젝트
**팀원 : 김민규(MMMMins/조장), 한용준(HANYONUJUN), 서예령(yeryeong0519@), 신건호(geonhooo), 이정우(wjddn8038), 김건우(inhatckgw)**

--- 
### 프로젝트 아이디어 의견제시
> 23.10.31 ~ 23.11.06

1. **CCTV (*카메라, ~~적외선 센서~~*)**
   1. ~~보안용 CCTV: 사람의 움직임 감지시 동영상 녹화 또는 실시간 확인 시스템~~
   2. ~~기능 추가 고려사항: 실내용 CCTV가 아닌 다방면의 방향성 모색~~
   3. 공사장같은 장소의 모니터링 시스템, AI모델을 통한 작업자들의 사고 감지시 후 감독관에게 전송 및 신고시스템
      >참고자료   
      > https://eehoeskrap.tistory.com/348   
      > https://hackmd.io/@NrN0buuTTp6lMAQ5lPMhNw/ry5D6WFnc   
      >관련논문   
      > https://scienceon.kisti.re.kr/commons/util/originalView.do?cn=JAKO201761242144589&oCn=JAKO201761242144589&dbt=JAKO&journal=NJOU00567471<br>
      >cctv 모션감지에 대한 참고자료<br>
      >https://return-value.tistory.com/106<br>
      >https://scribblinganything.tistory.com/544
      
      
2. ~~글자 인식 카메라 (*카메라*)~~
   1. ~~글자 번역 제공 카메라~~
   2. ~~사진 및 책, 문서 스캐너~~   
3. ~~시각장애인 보조 지팡이 (*GPS, RFID, UWB모듈 중 한가지 사용*)~~
   1. ~~횡단보도, 차도 등에 도착시 시각장애인에게 도로의 정보를 제공~~   
   2. ~~기능 추가 고려사항: 도착시 시각장애인 신호 알림 받을 수 있는 방향 모색~~   
4. ~~차량 전화번호 태그기기 (*NFC, RFID 등 태그관련 모듈 사용*)~~
   1. ~~핸드폰으로 태그시 시스템을 통한 차주인에 대한 정보제공(안심번호, 문자전송, 로그기록)~~   

---
### 프로젝트 아이디어 수립 및 기능제시
> 23.11.07 ~ 23.11.13

1. 산업현장 안전관리 모니터링 카메라
2. 목적
   - 산업현장 같은 곳에서 이런 cctv 장치의 배치가 적게 되어 사고가 발생해도 다음날 발견되는 경우가 많아 그런 부분을 감소시키기 위해서이다.
   - <img width="1103" alt="스크린샷 2023-11-14 오전 10 05 42" src="https://github.com/inhatc-wn/inhatc/assets/113413158/c2fec221-dd9a-4221-a858-8dc4ff407a4b">
   - <img width="767" alt="스크린샷 2023-11-14 오전 10 07 56" src="https://github.com/inhatc-wn/inhatc/assets/113413158/2d0e5109-c4d5-4184-b695-3008c8674145">
   - <img width="1103" alt="스크린샷 2023-11-14 오전 10 05 42" src="https://github.com/inhatc-wn/inhatc/assets/113413158/7eb2a5dd-bf55-457a-bbc9-7d909cb7756d">
   
3. 기능 : 쓰러짐 감지, 특정 행동 감지, 실시간 모니터링 및 로그 누적
   - 쓰러짐 감지 : 근로자가 쓰러짐을 감지하면, 관리자에게 알림을 전송
   - 특정 행동 감지 : 근로자의 특정행동을 감지하여 그에 맞는 알림을 전송한다. (사고 신고 모션인식 등)
   - 로그 누적 : 사소한 감지상태도 로그 누적을 통한 관리
   - 실시간 모니터링 : 감독관이 실시간으로 현장을 사고를 파악
     
4. 구조
   1. 라즈베리파이 + 카메라
   2. 실시간 모니터링 웹페이지 및 앱
   3. API서버(AWS) (알림전송, 모델적용, 기타 기능구현 서버)
   4. vue.js를 통해해 관리(아직 구현 안됨)
   4. vue.js를 통해 cctv내용들의 대한 ui를 구현<br>

---
### 웹 소켓통신 서버 구축 및 실시간 영상데이터 전달 기능 구현
> 23.11.14 ~ 23.11.19   
> **역할**   
> 백엔드 서버 구축 : 김민규, 서예령   
> 프론트 UI 및 기능 구현 : 한용준, 신건호   
> 모션감지 모델 구현 : 이정우   
> 라즈베리파이와 백엔드 간 통신 구현 : 김건우   
**완성된 서버 구현도**
<img src="https://github.com/inhatc-wn/inhatc/assets/113413158/0e421f91-e04c-48c4-a06a-b662cea0507a">

**웹소켓을 통한 영상 데이터 전달**   
<img src="https://github.com/inhatc-wn/inhatc/assets/113413158/0c8a0111-474a-4724-99ad-ae5a10fbb828">

---
### UI작업 및 API설계, 모델 최적화
> 23.11.21 ~ 23.11.27

**실시간 영상을 불러오는 fast api의 ip주소를 localhost 주소에 등록 후 녹화 시킬 수 있도록 구현**
![ui 수정](https://github.com/inhatc-wn/inhatc/assets/104452243/209152db-5875-4f7e-9761-95ed19b75e7c)
> ui 구조
> 1. 실시간 이미지 출력화면
> 2. 실시간 이미지 녹화 시작버튼
> 3. cctv 관리자 정보 등록 (아직 기능 구현 안됨)
> 4. 최근 활동 모션이 감지된 이미지 캡처 후 화면의 띄워주기(아직 기능 구현 안됨)
> 5. 감지상태를 로그를 통해 관리(아직 기능 구현 안됨)

<br>

**백엔드 API설계 및 문자 발송 구현**
> 이번주 문제점 : 기존 SMS 전송 플랫폼을 네이버 클라우드 플랫폼을 사용하려 했으나 최근 플랫폼에 악성 사용자 가입 증가로 인해 신규가입을 차단시켜놓은 상황, 다른 대안을 찾아야만 했음   
>   
> 해결안 : 해외 SMS 전송 플랫폼인 twilio 사용하여 SMS전송 구현

*API문서*   
<img width="1000" alt="스크린샷 2023-11-28 오전 1 01 47" src="https://github.com/inhatc-wn/inhatc/assets/113413158/e8bfb3e8-5dbc-485c-80a0-372260189df1">

*감지 로그 API*   
<img width="1000" alt="스크린샷 2023-11-28 오전 1 01 21" src="https://github.com/inhatc-wn/inhatc/assets/113413158/d40cd8c8-7cf1-4b31-a52b-0312248f1177">

*문자 전송 API*   
<img width="1000" alt="스크린샷 2023-11-28 오전 1 01 32" src="https://github.com/inhatc-wn/inhatc/assets/113413158/25fa1e02-e677-42c7-92d8-0113aeb95eba">

*실제 문자 전송 화면*   
<img width="500" alt="문자전송" src="https://github.com/inhatc-wn/inhatc/assets/113413158/4de7a461-30d9-48fb-bfec-c81f7397a9c0">

<br>

**모델최적화**   

> 모델최적화   
> 테스트 정확도: 0.9059560894966125   
> 테스트 손실: 0.2978125512599945   

*비감지: 사고 발생X*   
<img width="500" alt="문자전송" src="https://github.com/inhatc-wn/inhatc/assets/113413158/258bf61a-9756-49ec-96b9-f956f9e9c750">

*감지: 사고 발생O*   
<img width="500" alt="문자전송" src="https://github.com/inhatc-wn/inhatc/assets/113413158/5b6db61b-2686-4d2c-804b-8272570e34b5">

---
### 남은 한주간 방향성
> 현재 모션인식을 제외한 모든 기능은 전부 구현이 완료되어, 각 기능끼리 붙이는 작업만 남아있다.

- [x] 라즈베리파이
   - [x] 라즈베리파이 → 백엔드간 소켓통신 구현
   - [x] 카메라 데이터 전달 구현 
- [ ] 프론트
   - [x] UI설계
   - [x] 버튼을 통한 백엔드 서버와 웹 소켓 통신 구현
   - [ ] 관리자 정보( 전화번호, 이름 및 아이디 ) 백엔드 서버로 전달하는 기능
   - [ ] 지난 로그, 현재 로그 표시 구현
   - [x] 실시간 이미지 데이터 화면 표시 (현재 프로토타이핑으로 구현)
- [ ] 백엔드
   - [x] 서버 구현도 작성
   - [x] Database 작성
   - [x] API 작성
      - [x] SMS 문자 전송 기능 구현
      - [x] 로그 기록 전송 기능 구현
      - [ ] 로그 정보 데이터베이스에 기록하는 기능 구현
   - [x] 웹 소켓 통신 구현
      - [x] 라즈베리파이 → 백엔드 소켓 통신 구현
      - [x] 백엔드 → 프론트 소켓통신 구현
- [ ] AI모델
   - [x] 사람 쓰러짐 모델 구현
      - [x] 모델 정확도 향상
      - [x] 라즈베리파이 → 백엔드 카메라 데이터를 포매팅하여 모델에 적용시키고, 감지 여부 확인후 기존 값의 형태로 리턴
   - [ ] 행동을 통한 감지 신고
      - <img width="100" alt="image" src="https://github.com/inhatc-wn/inhatc/assets/113413158/40ff59a0-21ee-4c42-b119-5a791e481039">

      