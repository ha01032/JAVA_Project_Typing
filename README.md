# 자바 프로젝트: 코딩 타자연습 프로그램
**실행방법** : 해당 파일을 다운 받은 후 압축해제> eclipse 왼쪽에 오른쪽 마우스 > Import > Projects from Folder or Archive > Directory > 압축해제한 kakaoTyping 폴더를 선택 > Finish > com.cglee079.kakaotp.view 패키지에 있는 MainFrame에 들어가서 실행(Ctrl+F11)<br/>
## 기획의도
프로그래밍을 배우면서 복습의 중요성을 깨닫게 됨. 따라서 복습을 하기 위해 배운 키워드와 프로그래밍 언어를 자유롭게 추가하고, 그 추가한 내용으로 타자연습 게임을 하면서 코딩의 기본 소양인 타자실력도 키우고 내용도 다질 수 있는 프로그램을 만들고 싶었다. 또한, 그러한 자유로운 추가를 DB연동으로 구현하고 싶었다(아쉽게도 시간 부족으로 DB연동은 하지 못했다). 클론 코딩할 소스를 찾던 도중, '카카오타이핑'이라는 괜찮은 프로그램 소스를 찾게 되었고, 본 프로그램의 코드 분석과 기능 추가를 목표로 하게 되었다.

[클론코딩출처] : https://www.podo-dev.com/blogs/1
<br/><br/><br/><br/>
## 게임 설명
![20221222_095818](https://user-images.githubusercontent.com/117807082/209032767-843c1a1d-2c82-4a79-81c2-204474d6bba0.png)
  
  
**카카오 타이핑** : 자바 스윙을 기반으로 작성. 코딩 복습용 프로그램으로서, "산성비"게임에 기반을 두고 있다. 코딩 타자 연습 뿐 아니라, 본인이 추가한 복습 내용을 다질 수도 있는 프로그램이다.
 <br/><br/>
 **게임 개요:** 
 + 사용자별 ID 생성
 + 사용자별 커스텀 단어 추가
 + 성공 횟수에 따른 단어 등장 변동
 + 떨어지는 단어 성공 시, 키워드 -> 코드 -> 삭제 순 변경
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
위 그림과 같이 여러 View 클래스들이 각각 생성자를 생성함으로서 버튼이나 key를 누르는 action으로 연결고리를 형성하고, 매개변수를 전달한다.<br/> 나머지 클래스들은 그 View들의 재료가 되는 Logic class들이다.

### 게임 동작 원리  
PlayPanel에서 play클래스의 3가지 thread를 run 시키면서 게임이 이루어진다. 일정 시간마다 speed만큼 y축 좌표를 아래로 내리고 일정 높이 아래로 떨어지면 목숨을 깎는  **FWAni스레드**, 그리고 일정시간마다 랜덤생성된 단어들을 그 FWAni 스레드 배열에 각각 실어서 작동시키는  **wordMaker스레드**, 그리고 그 단어들의 속도를 일정 시간마다 높이는  **SpeedUpper** 스레드가 동작하면서 게임이 이루어지는 것이다. 이처럼 '일정시간마다'를 가능하게 하는 메서드는 각각의 스레드 안에 있는 sleep(time) 메서드로, 반복적으로 실행되는 스레드의 sleep 시간을 설정함으로서, 반복의 간격을 형성한다. 그리고 이러한 스레드에 변화를 줌으로서 4가지 아이템이 구현이 된다.<br/><br/>
그외 코드에 대해 자세한 분석은 해당 repository에 엑셀파일(CHC코드분석.xlsx)로 첨부하였다.<br/><br/><br/>

## 이슈 및 해결책




