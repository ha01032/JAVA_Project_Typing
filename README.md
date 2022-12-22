# 자바 프로젝트: 코딩 타자연습 프로그램
**실행방법** : 해당 파일을 다운 받은 후 압축해제> eclipse 왼쪽에 오른쪽 마우스 > Import > Projects from Folder or Archive > Directory > 압축해제한 kakaoTyping 폴더를 선택 > Finish > com.cglee079.kakaotp.view 패키지에 있는 MainFrame에 들어가서 실행(Ctrl+F11)
## 기획의도
프로그래밍을 배우면서 복습의 중요성을 깨닫게 됨. 따라서 복습을 하기 위해 배운 키워드와 프로그래밍 언어를 자유롭게 추가하고, 그 추가한 내용으로 타자연습 게임을 하면서 코딩의 기본 소양인 타자실력도 키우고 내용도 다질 수 있는 프로그램을 만들고 싶었다. 또한, 그러한 자유로운 추가를 DB연동으로 구현하고 싶었다(아쉽게도 시간 부족으로 DB연동은 하지 못했다). 클론 코딩할 소스를 찾던 도중, '카카오타이핑'이라는 괜찮은 프로그램 소스를 찾게 되었고, 본 프로그램의 코드 분석과 기능 추가를 목표로 하게 되었다.

[클론코딩출처] : https://www.podo-dev.com/blogs/1



## 게임 설명
![20221222_095818](https://user-images.githubusercontent.com/117807082/209032767-843c1a1d-2c82-4a79-81c2-204474d6bba0.png)


**카카오 타이핑** : 자바 스윙을 기반으로 작성. 코딩 복습용 프로그램으로서, "산성비"게임에 기반을 두고 있다. 코딩 타자 연습 뿐 아니라, 본인이 추가한 복습 내용을 다질 수도 있는 프로그램이다.

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



## 해당 파일의 동작 원리


