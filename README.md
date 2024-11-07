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

✅ 컬렉션 선택
- 계획 및 상황
	- 친구를 추가하는 순서대로 리스트에 출력되게 계획
	- Service 클래스에서 로직을 구성하고, 코드를 최소화 하기 위해 중복 저장 안하는 set컬렉션 사용
- 문제 발생
	- set 컬렉션 특징이 순서 없이 저장하기 때문에 랜덤으로 출력되는 점을 파악
 	- 회원가입 순서대로 친구목록에 출력되며, 유저들이 회원가입 순서를 유추할 수 있을 문제점 발견
- 해결 과정
	- set 컬렉션을 list로 변환 후 정렬 하도록 로직 변경
	- user의 id를 통해 정렬하는 결과가 나타남
	- 계획 한 방향으로(친구 추가순으로 목록 보이기) 구현하기 위해 list 컬렉션으로 변경
	- Controller 클래스에서 URL 매핑을 통해 친구 목록 불러오도록 로직을 변경
   	- DB와 연결해야하는 기능은 Service 클래스로 분리하여 로직 변경

✅ 직관적인 UI를 고려하여 해결
- list 컬렉션은 중복이 허용 되기 때문에 컨트롤러에서 중복제거 또는 JavaScript를 이용한 알림창 제공을 고민
- 유저에게 조금 더 직관적으로 보게 하기 위해 이미 친구가 등록된 유저의 닉네임을 클릭 시 친구 추가버튼이 노출되지 않도록 thymeleaf로 처리<br>


<details>
 <summary>수정 전 코드</summary>


 ![스크린샷(19)](https://github.com/user-attachments/assets/2c41acef-0fe2-43bc-8aa9-72b304362fe1)

 
</details>


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

✅ 도전적
- 1:1 실시간 채팅으로 계획
- WebSocket 및 STOMP 이해: 처음 다뤄보는 개념이기 때문에 실시간 메세지 처리에 대한 이해 필요
- STOMP에서 '주제(Topic)'와 '구독(Subscribe)' 개념이 생소했음, 실시간 메시징 구현을 위해 WebSocket 연결과 STOMP 프로토콜을 통해 메시지를 송수신하는 흐름을 학습하기 위해 기존 구현된 자료들을 분석
- 기존 구현된 WebSocket 및 STOMP 코드를 동일하게 구현해보며 이해 ⬇️
	
<details>
 <summary>WebSocketConfig</summary>

	@Configuration
	@EnableWebSocketMessageBroker
	public class WebsocketConfig implements WebSocketMessageBrokerConfigurer{
	@Override
	public void registerStompEndpoints(StompEndpointRegistry registry) {
		
		//stomp 접속 url -> /ws/chat
		registry.addEndpoint("/ws/chat")   //연결될 엔드 포인트
		.setAllowedOriginPatterns("*")
		.withSockJS();   //SocketJS 를 연결한다는 설정
	}
	@Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {

		//메세지를 구독하는 요청 url -> 메세지 받을 때
	registry.enableSimpleBroker("/queue", "/topic");

	//메세지를 발행하는 요청 url -> 메세지를 보낼 때
	registry.setApplicationDestinationPrefixes("/app");
	}

	} 
</details>

  <details>

<summary> DTO </summary>

 ChatRoom

	@Getter
	@Setter
	@NoArgsConstructor
	@Entity
	public class ChatRoom {

	@Id
	private String roomId; //방 번호
	private String roomName; //방 이름
	
	//채팅 방 생성
	public static ChatRoom create(String name) {
		ChatRoom room = new ChatRoom();
		room.roomId = UUID.randomUUID().toString();  //랜덤으로 받을 번호
		room.roomName = name;
		return room;
	}
	}

ChatMessage

	@Getter
	@Setter
	@NoArgsConstructor
	@AllArgsConstructor
	public class ChatMessage {
	//메세지 타입 : 입장, 채팅
	public enum MessageType{
		ENTER, TALK
	}
	private MessageType type; //메세지 타입
	private String roomId;  // 방번호
	private String sender;  // 메세지 보낸 사람
	private String message;  // 메세지
	}



 
</details>

<details>
 <summary> Controller </summary>
	

ChatController

	@RequiredArgsConstructor
	@Controller
	@RequestMapping("/chat")
	public class ChatController {	
 	private final ChatService chatService;

	//채팅 리스트 화면
	@GetMapping("/room")
	public String rooms(Model model) {
		return "/chat/room";
	}
	
	//채팅방 생성
	@PostMapping("/room")
	@ResponseBody
	public ChatRoom createRoom(@RequestParam(value = "name") String name) {
		return chatService.createRoom(name);
	}

	//모든 채팅방 목록 반환
	@GetMapping("/rooms")
	@ResponseBody
	public List<ChatRoom> room(){
		return chatService.findAllRoom();
	}
	
	//채팅방 입장 화면
	@GetMapping("/room/enter/{roomId}")
	public String roomDetail(Model model, @PathVariable("roomId") String roomId){
		model.addAttribute("roomId", roomId);
		return "/chat/roomdetail";
	}
	
	//특정 채팅방 조회
	@GetMapping("/room/{roomId}")
	@ResponseBody
	public ChatRoom roomInfo(@PathVariable("roomId") String roomId) {
		return chatService.findById(roomId);
	}
	
	}

MessageController

	@RestController
	@RequiredArgsConstructor
	public class MessageController {
	private final ChatService chatService;
	private final SimpMessageSendingOperations sendingOperations;
	
	@MessageMapping("/chat/message")
	public void enter(ChatMessage message) {
		if(ChatMessage.MessageType.ENTER.equals(message.getType())) {
			message.setMessage(message.getSender() + "님이 입장하였습니다");
		}
		sendingOperations.convertAndSend("/topic/chat/room/"+message.getRoomId(),message);
	}
	
	}


</details>
<details>
<summary> ChatService </summary>
		
	@Slf4j
	@RequiredArgsConstructor
	@Service
	public class ChatService {
	private Map<String, ChatRoom> chatRooms;
	@PostConstruct   //해당 어노테이션은 의존성 주입이 이루어진 후 초기화 작업이 필요한 메소드에 사용됨
	private void init() {
		chatRooms = new LinkedHashMap<>();
	}
	
	//채팅방 불러오기
	public List<ChatRoom> findAllRoom(){
		
		//채팅방 최근 생성 순으로 반환
		List<ChatRoom> result = new ArrayList<>(chatRooms.values());
		Collections.reverse(result);
		return result;	
	}
	//채팅방 하나 불러오기
	public ChatRoom findById(String roomId) {
		return chatRooms.get(roomId);
	}
	
	
	
	//채팅방 생성
	public ChatRoom createRoom(String name) {
		ChatRoom chatRoom = ChatRoom.create(name);
		chatRooms.put(chatRoom.getRoomId(), chatRoom);
		return chatRoom ;
	}	
	} 
</details>




✅ DB 연결의 필요성
- 문제 발생 : 서버 재시작 시 기존 주고 받았던 메세지가 사라지지 않도록 데이터베이스에 채팅 기록을 저장해야 함을 파악
- 해결 과정
	- 채팅 기록 저장: 채팅 메시지를 데이터베이스에 저장하기 위해 JPA와 Hibernate를 활용하여 MySQL 데이터베이스와 연동
	- 메세지 테이블과 채팅방 테이블을 분리하여 정규화 작업
	- 채팅방 ID ,메세지 ID를 사용하여 유저ID 와 관계 설정
  
- 결과: 채팅 기록 저장 및 조회 가능 : 채팅 메세지가 DB에 저장되어 해당 닉네임을 가진 유저와 이전에 나눈 대화를 확인 가능하게 함 

  	

✅ UI 개선
- JavaScript를 사용하여 1:1 채팅의 대표적인 UI로 디자인하여 유저가 채팅시 직관적이게 확인가능하도록 로직을 구성

✅ 최종 결과 및 배운점 
- 실시간 1:1 채팅 구현
- WebSocket을 사용하여 실시간 양방향 메세지 송수신과 STOMP 프로토콜을 사용하여 보다 쉽게 관리
- DB와 실시간 채팅의 통합 : 실시간으로 메세지를 처리하고, 데이터 저장과 조회를 고려하고 고민하면서 실시간 처리와 DB의 트랜잭션을 결하는 방법을 배움
- 

✅ 개선 사항
- 알림 시스템을 추가 : 메세지 마지막 확인 이후 채팅 메세지가 도착하면 뱃지등을 통해 알림을 받을 수 있도록 개선할 예정
- 채팅 기능 확장 : 프로젝트 내의 '같이 먹기' 신청시에만 노출 되는 부분을 다양한 페이지에서도 사용가능하도록 확장할 예정
- 파일 전송 기능 : 현재 텍스트만 전송 가능하므로 파일첨부나 이미지 전송도 가능하도록 할 예정
- 일대다 채팅 기능 추가 할 예정



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

