# Computer-concept-term-review
## 목표 
* 무의식에서 아는 줄 알았던 모르는 개념들을 확실히 정리하기 위한 레포
* 각각 제목만 보고 링크의 내용을 요약해서 말할 수 있도록 정확히 개념 공부
* 각 개념 필요성과 연관 관계 이해 -> 프로세스 이해 & 개인 블로그 정리 -> 복습(암기)  
## 프로그래머 기본기
* [읽어볼 것](http://www.fastcampus.co.kr/dev_school_gds_blog_feature_1/)
    - 코딩은 결국 데이터를 원하는 방향으로 바꾸는 것
* [이펙티브 프로그래밍 후기](https://brunch.co.kr/@imagineer/81)
    - 회사에서 개발자는 기획자가 만든 계획에 따라 디자이너의 디자인을 현실로 옮기는 일, 이게 싫으면 프리랜서로 
* 실수할 여지를 줄이자

## 기본기 공부할 곳
* [tutorialspoint - 언어를 비롯 구조와 개념등 많은 분야에 대한 튜토리얼을 제공](https://www.tutorialspoint.com/)
* [geeksforgeeks - 컴퓨터과학에 대한 거의 모든 걸 제공, 인터뷰 문제와 코딩 문제도 제공](https://www.geeksforgeeks.org/)
    *[인터뷰, 코딩 문제 관련](https://practice.geeksforgeeks.org/)
    
## 컴퓨터가 데이터를 저장하는 방식
[엔디안](http://www.joinc.co.kr/w/Site/Network_Programing/Documents/endian)
* 네트워크에서 stream을 받을 때 주의
[구조체 패딩](http://pangate.com/19) cf) Socket으로 데이터 보낼 때 주의 


## 자료구조, 알고리즘
- [알고리즘 강의 - 나동빈 블로그](https://blog.naver.com/ndb796/221226794899)
- [kks227 블로그](http://blog.naver.com/PostView.nhn?blogId=kks227&logNo=220820773477) & [kks227 코드](https://github.com/kks227/BOJ) : 알고리즘 공부(Intermediate) 
- [갓발자 isku의 자바 boj 풀이](https://github.com/ISKU/Algorithm)

## 프로그래밍 구조 
- 객체 지향
   - 철학 : 실제 생활과 비슷하게 코딩을 하자 
- 의존성 주입
    - dagger2 라이브러리
- 비동기 처리 
    - 네트워킹
    - RxJava
    - 코루틴

## 자바 
[Effective 자바 정리](https://brunch.co.kr/@oemilk/168)



## 선형대수 
공간 
## 인공지능 
### 기반 수학
* [Likelihood]()
    - 성공한 횟수(m)와 시행한 횟수(n)가 모수(parameter)로 주어지고 성공할 확률이 Random Variable일 때, 사건이 일어날 가능성 L(P|n,m)
* [Proability]()
    - 시행할 횟수(n)과 성공확률 (p)가 모수(parameter)로 주어지고 성공 횟수가 
### 자연어 처리 
[언어학 관련](https://blog.naver.com/bcj1210/)
[NLG](http://blog.ncsoft.com/?p=37832)
### 컴퓨터 비전 

### 딥러닝 


### 참고 사이트 
* [aidev 개발자 모임](http://aidev.co.kr/) light 한 사이트

<hr>

## 서버 
### REST API 
* [설계 가이드](https://hackernoon.com/restful-api-design-step-by-step-guide-2f2c9f9fcdbf)

### 네트워크

### *Docker*
- [Docker 처음 할 때 햇갈리는 점 pop it](https://www.popit.kr/kafka-%EC%9A%B4%EC%98%81%EC%9E%90%EA%B0%80-%EB%A7%90%ED%95%98%EB%8A%94-%EC%B2%98%EC%9D%8C-%EC%A0%91%ED%95%98%EB%8A%94-kafka/?utm_source=dable])
- [Docker 한국어 정리](https://github.com/remotty/documents.docker.co.kr)

### Docker Kubernetes (오케스트레이션 도구)
- 설명 [1](https://www.popit.kr/kubernetes-introduction/?utm_source=dable)

### 카프카 
- 설명 [첫걸음](https://www.popit.kr/kafka-%EC%9A%B4%EC%98%81%EC%9E%90%EA%B0%80-%EB%A7%90%ED%95%98%EB%8A%94-%EC%B2%98%EC%9D%8C-%EC%A0%91%ED%95%98%EB%8A%94-kafka/?utm_source=dable)

<hr/>

## 클라이언트 
### 안드로이드
- [안드로이드 개발자가 알아야할 것들](https://medium.com/mindorks/how-to-become-a-complete-android-developer-110d7ef91f2a)
    - 요약
    - Build ! 
    - 유용한 개발 툴 
    - 어떻게 3th party library가 돌까?
- [안드로이드 가이드](https://guides.codepath.com/android)
- [구글 샘플](https://github.com/googlesamples) : 사실상 여기가 끝판왕
    - [연습 - 해바라기 프로젝트](https://github.com/googlesamples/android-sunflower)
- [Architecture](https://github.com/googlesamples/android-architecture)  
- [비동기 처리 Handler, Looper](https://academy.realm.io/kr/posts/android-thread-looper-handler/)
- [MVC->MVP->MVVM](https://thdev.tech/androiddev/2017/08/09/Android-MVC_MVP_MVVM-Intro.html) 
- 애니메이션 
    - [예제](https://android.jlelse.eu/make-your-app-shine-how-to-make-a-button-morph-into-a-loading-spinner-9efee6e39711)
    - [아이콘](https://www.androiddesignpatterns.com/2016/11/introduction-to-icon-animation-techniques.html)
### 코틀린
* [Reference](https://kotlinlang.org/docs/reference/typecasts.html#safe-nullable-cast-operator)
* [MVP](https://github.com/googlesamples/android-architecture/tree/todo-mvp-kotlin/)
* [추가된 함수 apply, let, run, with](https://www.androidhuman.com/lecture/kotlin/2016/07/06/kotlin_let_apply_run_with/)

## 웹
* [django 시작 문서](https://django-doc-test-kor.readthedocs.io/en/old_master/topics/templates.html) 
### CSS 
* [Udemy 웹 디자인 강좌 : Web Design for Web Developers: Build Beautiful Websites!](https://www.udemy.com/web-design-secrets/)
* [Button 디자인](https://freefrontend.com/css-buttons/)

### 애니메이션 
* [애니메이션 라이브러리](https://hackernoon.com/10-javascript-animation-libraries-to-follow-in-2018-50ff1d905f43)

## 성능 
- [안드로이드 메모리 누수 패턴](https://m.blog.naver.com/eyeballss/221127939604)
- [가비지 컬렉터](http://imcreator.tistory.com/120?category=629872)
- [프론트엔드 성능 체크리스트](https://github.com/ParkSB/Front-End-Performance-Checklist/blob/master/README.md)
[Recyclerview precomputedText](https://developers-kr.googleblog.com/2018/08/prefetch-text-layout-in-recyclerview.html)
- [자바스크립트 성능 저하 코드스타일](http://12bme.tistory.com/134) 

## 기타 
- [Readme 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601) 
- 공부 링크 
    - [포프 Tv](https://www.youtube.com/channel/UC63J0Q5huHSlbNT3KxvAaHQ)
    - [Pop it](https://www.popit.kr/) : 데브옵스와 아키텍처 설계등의 양질의 칼럼
    - [Medium 안드로이드](https://android.jlelse.eu/) : 영어로 된 칼럼
    - [Medium Pro 안드로이드](https://proandroiddev.com/) : 영어로 된 칼럼
    - [Medium freecamp](https://medium.freecodecamp.org/)
    - [tutorialspoint](https://www.tutorialspoint.com/index.htm) : 새로운 개념 시작에 좋음, 영어
    - [Sktechx Youtube](https://www.youtube.com/channel/UCtV98yyffjUORQRGTuLHomw)
: 양질의 최신 세미나를 들을 수 있음, 한글 
    - [zerocho](https://www.zerocho.com/) : 웹 프론트 전반적으로 잘 설명되어있음 

## 개인적으로 명확하지 않은 것들 질문 
- Enum 을 쓰면 코드가 빨라지나 ?
- Kotlin에서 nullable 이 필요 없을때? 
- Dagger, 의존성 주입은 parameter로 외부에서 객체를 넘겨주는 방식인데 Dagger 는 안 써봐서 어떤 식으로 의존성 주입인지 햇갈림
- Android 
    - SharedPreference 
    - [Video](https://github.com/googlesamples/android-VideoPlayer)
- oauth 
- proguard : 코드 난독화?
- Firebase 
- [Notification](https://github.com/googlesamples/android-architecture-components/tree/master/PagingWithNetworkSample)
## 기여자 목록입니다. 감사합니다!
