# FCM (Firebase Cloud Messaging)

Firebase 클라우드 메시징(FCM)은 무료로 메시지를 안정적으로 전송할 수 있는 교차 플랫폼 메시징 솔루션입니다. <br>

FCM 을 이용하면 새 이메일이나 기타 데이터를 동기화 할 수 있다고 클라이언트에 알릴 수 있습니다. <br>

자동으로 동기화가 되므로 굳이 서버 관리가 필요없다 

<img src="https://elfinlas.github.io/2017/12/25/Adroid-FCM-Setup/img_01.png">


## 세팅
### 서버 세팅 
1. https://console.firebase.google.com/u/2/?hl=ko 로그인
2. 프로젝트 추가 
3. 
### Gradle 세팅 
```
dependencies {
     implementation 'com.google.firebase:firebase-messaging:12.0.1'
}
```
### Manifest 설정 
인터넷 권한 설정
```
<uses-permission android:name="android.permission.INTERNET"></uses-permission>
```
FCM 서비스 
MyFirebaseMessagingService : FirebaseMessagingService() 를 상속받은 클래스  <br>
MyFirebaseInstanceIDService : FirebaseInstanceIdService() 를 상속 받은 클래스 
```
 <service
            android:name=".firebase.MyFirebaseMessagingService">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT"/>
            </intent-filter>
        </service>

        <service
            android:name=".firebase.MyFirebaseInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
```
## 알림 전달 방식에 따른 처리 
* foreground 
 onMessageReceived() 메소드를 거침 
 
* background 


### 참고사항 
- [FCM 설정](http://blog.naver.com/PostView.nhn?blogId=cosmosjs&logNo=221299751382&categoryNo=0&parentCategoryNo=56&viewDate=&currentPage=4&postListTopCurrentPage=1&from=search&userTopListOpen=true&userTopListCount=10&userTopListManageOpen=false&userTopListCurrentPage=4)