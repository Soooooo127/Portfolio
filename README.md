<h1>김지수 포트폴리오</h1>
안녕하세요, JAVA 풀스택 개발자 김지수입니다.

# 🚨팀 프로젝트 명
[모두 모이자, MOMO](http://momo2gather.com/member/welcome)

# 🚨팀 프로젝트 일정 및 인원
프로젝트 일정<br>
2024년 7월 15일 ~ 2024년 9월 12일 <br>
9주 소요 <br>
![momo 프젝 일정](https://github.com/user-attachments/assets/15151a42-95b9-4c11-b051-6695cd882b7c)

팀 구성 : 지원자 외 5명<br>
 

# 🚨사용기술
- 백엔드
자바, 스프링부트, 스프링 시큐리티, 롬복, jpa hibnate, MySQL<br>

- 프론트엔드
html , css, js<br>
타임리프<br>
부트스트랩<br>
j 쿼리 <br>

# 🚨ERD
![MomoERD ver1 1 1](https://github.com/user-attachments/assets/1f4de842-c053-4456-a8a7-f211ca36a0b4)



# 🚨핵심 기능
프로젝트의 핵심 기능 설명 <br>

같이먹기
oauth
친구
채팅 
이미지


# 🚨기여한 점
공지사항 게시판<br>
친구추가 / 삭제 <br>
1:1 채팅 <br>



# 🚨문제 해결 경험
친구 등록 하는 데 
- 친구 등록하는데 있어서 set 컬렉션 or list 컬렉션 사용 고민<br>
- 친구를 추가하는 순서대로 리스트에 출력되게 계획했습니다.
- 코드를 최소화 하기 위해 중복 저장 안하는 set컬렉션 사용했습니다.
- set 컬렉션 특징이 순서 없이 저장하기 때문에 랜덤으로 출력되는 점을 알았습니다.
- set 컬렉션을 list로 변환 후 정렬 하도록 로직을 구성했습니다.
- 결과로 user의 id를 통해 정렬해서 회원가입 순서대로 친구목록에 출력되며, 유저들이 회원가입 순서를 유추할 수 있을 문제점도 발겼했습니다.

<details>
 <summary>수정 전 코드</summary>


 ![스크린샷(19)](https://github.com/user-attachments/assets/2c41acef-0fe2-43bc-8aa9-72b304362fe1)

 
</details>

- 그래서 list 컬렉션으로 변경하여 구현 계획대로 진행하고자 했습니다.
- list 컬렉션은 중복이 허용 되기 때문에 컨트롤러에서 중복제거 로직을 생각했으나, 유저가 조금 더 직관적으로 보기 쉽게 친구등록이 이미 된 사람은 친구 추가시 추가버튼을 가렸습니다.
<details>
 <summary>수정 후 코드</summary>

 ## FriendService 클래스 수정 
 
 
    public void createFriend(String myid, Member friendMemeber) {		
      	Optional<Member> me = this.memberRepository.findBymemberid(myid); //내 아이디 저장
	 Member mymember = me.get(); //내 정보 가져와서 member 타입으로 객체 생성 
         mymember.getFriend().add(friendMemeber); //친구객체를 list 컬렉션에 저장 
	 this.memberRepository.save(mymember);
		 }
## Friend.html 


![freePosting_list](https://github.com/user-attachments/assets/b421ef86-d737-4254-83cc-4a6dd59ad2db)


</details>



- 채팅에 대한 트러블 슈팅
채팅 했더니 @jsonignore 어노테이션 붙였더니 가능

<details>
 <summary>접기/펼치기</summary>

 ## 접은 내용
 접은 내용
</details>

