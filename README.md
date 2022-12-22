# 자바 프로젝트: 코딩 타자연습 프로그램
**실행방법** : 해당 파일을 다운 받은 후 압축해제 > eclipse 왼쪽에 오른쪽 마우스 > Import > Projects from Folder or Archive > Directory > 압축해제한 kakaoTyping 폴더를 선택 > Finish > com.cglee079.kakaotp.view 패키지에 있는 MainFrame에 들어가서 실행(Ctrl+F11)<br/>
## 기획의도
  프로그래밍을 배우면서 복습의 중요성을 깨닫게 됨. 따라서 복습을 하기 위해 배운 키워드와 프로그래밍 언어를 자유롭게 추가하고, 그 추가한 내용으로 타자연습 게임을 하면서 코딩의 기본 소양인 타자실력도 키우고 내용도 다질 수 있는 프로그램을 만들고 싶었음. 또한, 그러한 자유로운 추가를 DB연동으로 구현하고 싶었다(아쉽게도 시간 부족으로 DB연동은 하지 못했다). 클론 코딩할 소스를 찾던 도중, '카카오타이핑'이라는 좋은 프로그램 소스를 찾게 되었고, 본 프로그램의 코드 분석과 기능 추가를 목표로 하게 되었다.

[클론코딩출처] : https://www.podo-dev.com/blogs/1
<br/><br/>
## 게임 설명
![20221222_095818](https://user-images.githubusercontent.com/117807082/209032767-843c1a1d-2c82-4a79-81c2-204474d6bba0.png)
  
  
**카카오 타이핑** : 자바 스윙을 기반으로 작성. 코딩 복습용 프로그램으로서, "산성비"게임에 기반을 두고 있다. 코딩 타자 연습 뿐 아니라, 본인이 추가한 복습 내용을 다질 수 있는 프로그램이다.
 <br/><br/>
 **게임 개요:** 
 + 사용자별 ID 생성
 + 사용자별 커스텀 단어 추가
 + 성공 횟수에 따른 단어 등장 변동
 + 떨어지는 단어를 정확히 타이핑 했을 때, 키워드 -> 코드 -> 삭제 순으로 변경
 + 아이템 사용 (F1, F2, F3, F4 키 이용)
   1. 모두 지우기 : 단어가 모두 지워지며, 점수상승
   2. 잠깐 멈추기 : 떨어지는 단어가 멈춥니다. 일정 시간 후 다시 떨어집니다.
   3. 천천히 : 떨어지는 단어 속도가 늦춰집니다. 일정 시간 후 제 속도로 돌아옵니다.
   4. 회복 : 체력이 회복됩니다.
 + 사용자별 랭킹
 <br/><br/><br/> 
## 해당 파일의 동작 원리
Lang : Java 11.0.2 version  
IDE : Eclipse  
Java-Swing : GUI 구현  
Java-Audio : 배경음, 효과음 컨트롤  
Thread : 산성비 구현.  
File : 랭킹, 단어 읽기 및 쓰기  
Strcuture : View, Logic 분리 구현.  

### 클래스간의 연결고리
![크기변환 20221222_175342](https://user-images.githubusercontent.com/117807082/209096886-d2e03007-52f9-4241-9725-5fca84a3bbd7.png)
<br/><br/>
위 그림과 같이 여러 View 클래스들이 각각 생성자를 생성함으로서 버튼이나 key를 누르는 action을 통해 연결고리를 형성하고, 매개변수를 전달한다.(상속관계 아님)<br/> 나머지 클래스들은 그 View들의 재료(멤버변수, 상수, 메서드, 객체)가 되는 Logic class들이다.

### 게임 동작 원리 : 3가지 스레드의 run  
PlayPanel에서 Play클래스의 3가지 thread를 run 시키면서 게임이 이루어진다. 일정 시간마다 speed만큼 y축 좌표를 아래로 내리고 일정 높이 아래로 떨어지면 목숨을 깎는  **FwAni스레드**, 그리고 일정시간마다 랜덤생성된 단어들을 그 FwAni 스레드 배열에 각각 실어서 작동시키는  **wordMaker스레드**, 그리고 그 단어들의 속도를 일정 시간마다 높이는  **SpeedUpper스레드**가 동작하면서 게임이 이루어지는 것이다. 이처럼 '일정시간마다'를 가능하게 하는 메서드는 각각의 스레드 안에 있는 sleep(time) 메서드로, 반복적으로 실행되는 스레드의 sleep 시간을 설정함으로서, 반복의 간격을 형성한다. 그리고 이러한 스레드에 변화를 줌으로서 아이템이 구현이 된다.

### 단어 및 유저 추가 및 읽기 기능 : txt파일과 프로그램 내의 JTextArea의 공백(\t) 및 줄바꿈(\n)을 기준으로 읽고 등록함으로서 가능<br/><br/>
그 외 코드에 대해 자세한 분석은 엑셀파일(CHC코드분석.xlsx)로 첨부하였다.
<br/><br/><br/>

## 이슈 및 해결책
1. 여러 클래스들의 연결고리를 찾기 위해 파일을 백업한 후 디버깅을 돌려보았는데 메인 클래스에 있는 내용의 과정만 볼 수 있었음(갑자기 화면이 형성되더니 모든 기능이 다 실행됨) 또한 starUML을 통해 봐도 상속관계가 아니라서 그 연결고리를 파악하기 어려웠음<br/>
: 엑셀파일에서 볼 수 있듯이 하나하나 꼼꼼한 코드분석을 하였고 결국 위에서 제시했던 클래스간의 연결고리를 파악할 수 있었음. 
2. 사운드 문제) 집에서는 사운드가 잘 실행이 되었으나, 학원 컴퓨터로는 사운드로 인해 게임 동작에 오류가 발생 <br/>
: wav를 다 찾아서 주석처리 하니 동작 오류가 사라짐
3. 필요한 코드가 다 작성돼있음에도 여러가지 프레임과 메뉴바가 보이지 않고 흰화면으로만 보임 <br/>
: 프레임 구성요소들을 넣는(add) 메서드 바로 직후에 각각 revalidate() 메서드를 넣어줬더니 바로 해결됨.<br/><br/><br/>


## 추가 구현한 기능
1. 코딩 복습을 하고 코딩 타자연습을 할 수 있는 프로그램을 만드는 것이 목적이었기 때문에, 여러 복습 키워드에 대한 코드내용을 내용으로 추가하고, 긴 코드를 입력할 수 있도록 JTextarea의 길이를 늘렸다.
2. 점수프레임(ScoreFrame)에 원래 메인메뉴나 게임을 끌 수 있는 버튼이 없었는데, 버튼을 생성해줬다. 이 과정에서 메인메뉴로 돌아가기 위해서 생성자에 mainFrame.this 매개변수를 여러 클래스를 거쳐서 끌고와서 사용하였다.<br/><br/><br/>

## 아쉬운점 및 추가하고 싶은 기능
: 늦게 시작하고 꼼꼼한 코드 분석에 치중하는 바람에 기능 구현을 거의 하지 못하고, 그러한 기능 구현을 통한 학습의 계기가 되지 못한점이 아쉬움.

### 추가하고 싶은 기능
+ 단어 추가, 유저 추가에 대한 DB연동
+ 유저와 단어의 삭제 및 수정 기능 추가(역시 DB연동)
+ 게임 스킬 하나 추가(4가지 스킬을 바탕으로 내가 만들고자 하는 스킬을 추가하고 싶음)
+ 인터페이스를 기반으로 한 리펙터링

## 작업후기
처음 자바 프로젝트를 하는거라 코딩 분석에 시간이 많이 들었지만, 수업 때 배운 내용을 바탕으로 코딩 분석을 끝까지 다 해낼 수 있었고, 이를 통해 수업을 열심히 듣고 복습을 철저히 할 필요성을 느낄 수 있었다. 또한 전체적인 코드 분석을 하면서 연결고리를 찾는 과정이 마치 추리를 하는 느낌이라 재밌었고, 코딩이 실제적으로 어떻게 응용될 수 있는지 알 수 있었으며, 코딩의 무한한 잠재성에 대해서 느낄 수 있었다. 
