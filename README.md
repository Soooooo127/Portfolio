# 김지수 포트폴리오
> 안녕하세요, <br>
**책임감**있는 자세로 **협업**하며, **협조적인 태도**로 회사와 함께 성장하고 싶은 풀스택 개발자 **김지수**입니다.
<br><br>

## 📁 팀 프로젝트 명

> 모두모이자, MOMO <br>
 1인 가구를 위한 맛집정보와 함께 타인과 상호작용 할 수 있는 커뮤니티 서비스를 제공하는 웹사이트 입니다.


[MOMO 웹사이트](http://momo2gather.com/member/welcome) <br><br><br>



## 📁 팀 프로젝트 인원 및 일정
   팀 프로젝트 인원  :  김지수 외 5명 <br>

  프로젝트 일정  :  2024년 7월 15일 ~ 2024년 9월 12일 (총 9주 소요) <br><br>
	 ![momo 프젝 일정](https://github.com/user-attachments/assets/15151a42-95b9-4c11-b051-6695cd882b7c) <br><br><br>


 

## 📁 사용기술

### 백엔드
- Java
- Spring Boot
- Spring Security
- JPA Hibernate
- MySQL

### 프론트엔드
- HTML
- CSS
- JS
- Thymeleaf
- Bootstrap
- JQuery  <br><br>

## 📁 ERD
![MomoERD ver1 1 1](https://github.com/user-attachments/assets/1f4de842-c053-4456-a8a7-f211ca36a0b4) <br><br><br>



## 📁 핵심 기능

- 같이먹기 신청기능  :  맛집 정보를 선택하여 오프라인을 통해 같이 먹을 사람들을 찾는 기능
- 소셜을 통한 로그인 (구글, 네이버) 
- CRUD 기반의 다양한 게시판들 (자유, 질문과 답변, 출석체크, 문의하기, FAQ, 공지사항으로 구성)
  <br><br><br>


## 📁 기여한 점

- CRUD 기반 게시판 구현 (공지사항 게시판) <br>
- 친구추가 / 삭제 기능 구현 <br>
- 1:1 채팅 기능 구현 <br><br><br>



## 📁 문제 해결 경험
### 친구기능에서 문제 해결 경험

- 친구를 추가하는 순서대로 리스트에 출력되게 계획
- Service 클래스에서 로직을 구성하고, 코드를 최소화 하기 위해 중복 저장 안하는 set컬렉션 사용
- set 컬렉션 특징이 순서 없이 저장하기 때문에 랜덤으로 출력되는 점을 파악
- set 컬렉션을 list로 변환 후 정렬 하도록 로직 변경
- user의 id를 통해 정렬하는 결과가 나타남, 또한 회원가입 순서대로 친구목록에 출력되며, 유저들이 회원가입 순서를 유추할 수 있을 문제점도 발견 <br>

<details>
 <summary>수정 전 코드</summary>


 ![스크린샷(19)](https://github.com/user-attachments/assets/2c41acef-0fe2-43bc-8aa9-72b304362fe1)

 
</details>

- 계획 한 방향으로(친구 추가순으로 목록 보이기) 구현하기 위해 컬렉션을 list로 변경
- Controller 클래스에서 url 매핑을 통해 친구 목록 불러오게 로직을 변경, 데이터 베이스와 연결해야하는 기능은 Service 클래스로 분리하여 로직을 변경
- list 컬렉션은 중복이 허용 되기 때문에 컨트롤러에서 중복제거 로직을 생각했으나,
- 유저에게 조금 더 직관적으로 보게 하기 위해 이미 친구가 등록된 유저의 닉네임을 클릭 시 친구 추가버튼이 노출되지 않도록 thymeleaf로 처리<br>

<details>
 <summary>수정 후 코드</summary>

 ## FriendService 클래스 수정 
 
 
    public void createFriend(String myid, Member friendMemeber) {		
      	Optional<Member> me = this.memberRepository.findBymemberid(myid); //내 아이디 저장
	 Member mymember = me.get(); //내 정보 가져와서 member 타입으로 객체 생성 
         mymember.getFriend().add(friendMemeber); //친구객체를 list 컬렉션에 저장 
	 this.memberRepository.save(mymember);
		 }
## freePosting_list.html 

친구 추가 기능은 닉네임이 노출 되는 모든 곳에서 가능하도록 구현 <br>
대표적으로 freePosting 을 참고해주시기 바랍니다.<br>

![freePosting_list](https://github.com/user-attachments/assets/b421ef86-d737-4254-83cc-4a6dd59ad2db)

구현 페이지입니다.

친구 추가 전

![친구추가 전](https://github.com/user-attachments/assets/1c6fc5ae-768f-494e-9503-56c067356c45)

친구 추가 후
![친구 추가 후](https://github.com/user-attachments/assets/95a43033-5326-40af-9169-34bff0603739)


</details>
<br><br>

### 채팅 기능 구현 시 문제 해결 경험

💡 도전적
- 1:1 실시간 채팅으로 계획
- WebSocket 및 STOMP 이해: 처음 다뤄보는 개념이기 때문에 실시간 메세지 처리에 대한 이해가 필요했음
- STOMP에서 '주제(Topic)'와 '구독(Subscribe)' 개념이 생소했음, 실시간 메시징 구현을 위해 WebSocket 연결과 STOMP 프로토콜을 통해 메시지를 송수신하는 흐름을 학습하기 위해 기존 구현된 자료들을 분석
- 연습한 웹소켓 캡쳐


💡 DB연결의 필요성
- 서버 재시작 시 기존 주고 받았던 메세지가 사라지지 않도록 데이터베이스에 채팅 기록을 저장해야 함을 파악
- 채팅 기록 저장: 채팅 메시지를 데이터베이스에 저장하기 위해 JPA와 Hibernate를 활용하여 MySQL 데이터베이스와 연동
- 메세지 테이블과 채팅방 테이블을 분리하여 정규화 작업
- 채팅방 ID ,메세지 ID를 사용하여 유저ID 와 관계 설정
  

  	

💡UI 개선
- JavaScrip를 사용하여 1:1 채팅의 대표적인 UI로 디자인하여 유저가 채팅시 직관적이게 확인가능하도록 로직을 구성

💡 결과 
- 실시간 1:1 채팅 구현


💡 배운점 
-


## 📁 팀 프로젝트 Repository
[프로젝트 Repository](https://github.com/Soooooo127/PROJECT-MOMO.git) <br><br>


## 📁 국가기관 전략 산업 훈련(풀스택 Java 개발자)
이 과정을 수료하기 위해 하루 8시간씩 6개월 과정을 수료함<br>
#### 배운 내용<br>
- java 기초<br>
- DB (RDBMS)<br>
- MVC 패턴으로 게시판 만들기 <br>
	- spring + jsp 사용하여 게시판 만들기 <br>
	- spring boot + thymeleaf 사용하여 게시판 만들기 <br>
- 팀프로젝트



## 📁 Contact
Email : wltn125@naver.com

Github : [김지수 Github](https://github.com/Soooooo127)

