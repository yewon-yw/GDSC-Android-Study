# Chapter1. 안드로이드 개요와 개발 환경 설치
##  안드로이드의 개요
### 스마트폰
-----
-  통화기능 + 컴퓨터 + 다양한 기능 내장(MP3, 카메라, DMB, GPS 등)

### 스마트폰 개발 환경 비교
-----
|**구분**|**안드로이트**|**아이폰**|**윈도폰**|
|:--:|:------:|:------:|:------:|
|**개발언어**|Java, Kotlin, C++|Objdect C|C#, VB.NET|
|**개발 운영체제**|Windows, Linux, Mac OS|Mac OS|Windows 8/8.1/10|
|**개발 툴**|Eclipse, Android Studio|Xcode|Visual Studio 2013 이상|
|**지원 장치**|안드로이드폰, 안드로이드 태블릿, 안드로이드 스마트워치, 안드로이드 TV|아이폰, 아이팟(iPod), 아이패드(iPad), 애플워치|윈도폰|
|**대표 제품**|삼성 갤럭시 S/노트 시리즈, LG G/G Pro/V 시리즈, 구글 넥서스/픽셀 시리즈|아이폰 시리즈, 아이패드 시리즈|노키아 루미아(Lumia) 시리즈|
|**최신 개발 버전**|Android 10.0(Q)|iOS 13|윈도폰 10|
|**앱스토어**|구글 플레이, 삼성 Apps, T스토어, 네이버 스토어 등|애플 앱스토어|Windows 스토어|

### 안드로이드
-----
- 구글(Google)이 2007년 안드로이드사를 인수하면서 시작

- 주요 버전별 특징
  1. 롤리팝(5.0) : 다양한 안드로이드 기기를 통합 지원
  2. 마시멜로(6.0) : 앱 권한 설정, 지문 인식 지원
  3. 누가(7.0) : 가상현실 지원 및 3D 게임, 알림 기 향상, 다중 창 열기 지원
  4. 오레오(8.0) : PIP, 알림, 자동 채우기, 멀티카메라, 인공지능확장 등을 지원
  5. Android 10.0(Q) : 라이브 캡션, 스마트 재생, 청각 보조, 동작 네비게이션, 어두운 테마, 개인 정보 제어 등을 지원

- 안드로이드의 특징
  1. 안드로이드의 핵심 커널(Kernel) : 리눅스(Linux)로 구성
  2. 안드로이드 애플리케이션 개발 언어 : Java or Kotlin
  3. 안드로이드 SDK에서 많은 라이브러리를 포함하고 있어 개발이 용이
  4. 오픈 소스를 지향 → 운영체제부터 관련 문서, 개발 도구 등 거의 모든 것을 무료로 사용 가능
  5. 지속적인 업그레이드 제공

- 안드로이드의 구조
  1. 응용프로그램(Applications)
     - 안드로이드 스마트폰에서 샤용할 수 있는 일반적인 응용 프로그램
     - 웹 브라우저, 달력, 구글맵, 연락처, 게임 등 사요자 입장에서 가장 많이 사용
     - Java 또는 Kotlin으로 제작됨
  2. 응용 프로그램 프레임워크(Application Framework)
     - 안드로이드 API가 존재하는 곳
     - 안드로이드폰 하드웨어에 접근할 때 API를 통해서만 가능
  3. 안드로이드 런타임(Android Runtime)
     - Java 코어 라이브러리와 달빅 가상 머신 또는 아트 런타임으로 구성됨
     - 안드로이드는 Java 또는 Kotlin 문법으로 프로그래밍하지만 Java 가상 머신을 사용하지 않고 이곳의 달빅 가상 머신이나 아트 런타임을 사용함
  4. 라이브러리(Libraries)
     - 안드로이드에서 사용되는 여러 시스템 라이브러리는 시스템 접근 때문에 Java 또는 Kotlin이 아닌 C로 작성 → 성능이 뛰어나며 세밀한 조작 가능
  5. 리눅스 커널(Linux Kernel)
     - 하드웨어의 운영과 관련된 저수준의 관리 기능
     - 메모리 관리, 디바이스 드라이버, 보안 등

# Chapter2. 처음 만드는 안드로이드 애플리케이션
## 실습1 - 첫 응용 프로그램 작성하기
### 버튼 만들어보기
-----
![첫화면구성](https://user-images.githubusercontent.com/111935711/198240889-b9faecb6-2dd7-4e60-b237-83e4b388c813.jpg)

## 실습2 - 직접 풀어보기
### 실습 내용
-----
![실습내용](https://user-images.githubusercontent.com/111935711/198240943-c683cf03-2c28-48ee-9456-60f4bd132488.jpg)

### 실습 코드(MainActivity.kt)
-----
```
package com.example.helloandroid

import android.content.Intent
import android.net.Uri
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        var linkBtn = findViewById<Button>(R.id.link)
        var callBtn = findViewById<Button>(R.id.call)
        var photoBtn = findViewById<Button>(R.id.photo)
        var exitBtn = findViewById<Button>(R.id.exit)

        linkBtn.setOnClickListener {
            var intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://wontfolio.com"))
            startActivity(intent)
        }
        callBtn.setOnClickListener {
            var intent = Intent(Intent.ACTION_DIAL, Uri.parse("tel:119"))
            startActivity(intent)
        }
        photoBtn.setOnClickListener {
            var intent = Intent(Intent.ACTION_PICK, Uri.parse("content://media/internal/images/media"))
            startActivity(intent)
        }
        exitBtn.setOnClickListener {
            finish()
        }
    }
}
```

### 실습 결과
-----
![실습화면](https://user-images.githubusercontent.com/111935711/198241322-3b138e4d-f82e-4506-9d23-5f4c1eec8761.jpg)

![실습결과1](https://user-images.githubusercontent.com/111935711/198241351-472b73ff-cf0f-4c2f-b66d-32929142d96d.jpg)

![실습결과2](https://user-images.githubusercontent.com/111935711/198241382-af8fc8bc-5a2d-4f0f-af0f-ca741b568c6c.jpg)

![실습결과3](https://user-images.githubusercontent.com/111935711/198241408-b6e49449-ddd0-4b15-b5e6-fe28db135382.jpg)

![실습결과4](https://user-images.githubusercontent.com/111935711/198241439-693bb513-f9db-46a1-b881-739031db2379.jpg)


## 프로젝트에서 사용되는 폴더와 파일의 용도
### java 폴더
-----
- 하위에 패키지명의 폴더가 있는데, 이는 안드로이드 프로젝트를 생성할 때
입력한 패키지 이름과 동일한 것
- 패키지 이름 아래에 MainActivity.kt로 메인 Kotlin 소스가 들어 있음
  - 실제로 프로그래머가 가장 많이 수정할 소스 파일이며, 주로
액티비티(화면, activity_main.xml)에서 어떤 일을 할지를
프로그래밍하게 됨

### java(generated) 폴더
-----
- Android Studio 3.2부터 제공되는 폴더이며 시스템 내부적으로 사용(특별히 신경 쓰지 않아도 됨)

### res 폴더
-----
- 앱 개발에 사용되는 이미지, 레이아웃, 문자열 등이 들어가는 폴더
- drawable 폴더
  - 이미지 파일을 넣음
- mipmap 폴더
  - 디자인 화면이나 앱이 설치된 후에 보이는 런처 아이콘을 넣음
  - xxxhdpi, xxhdpi, xhdpi : 초고해상도 런처 아이콘 파일을 넣음
  - hdpi : 고해상도 런처 아이콘 파일을 넣음
  - mdpi : 중해상도 런처 아이콘 파일을 넣음
- layout 폴더
  - 액티비티(화면)를 구성하는 XML 파일을 넣음
  - 기본적으로 activity_ main.xml이 초기화면으로 지정되어 있음. 
추가로 화면이 필요하면 이곳에 XML 형태로 생성
- values 폴더
  - strings.xml : 문자열을 저장
  - colors.xml : 색상표를 저장
  - styles.xml : 스타일을 저장
- menu 폴더
  - 메뉴 XML 파일을 저장하는데, 필요시 생성해서 사용
- anim 폴더
  - 애니메이션을 저장
- XML 폴더
  - XML 파일을 저장

### res(generated) 폴더
-----
- Android Studio 3.5부터 제공되는 폴더이며 내부적으로 사용(신경 쓰지
않아도 됨)

### manifest 폴더
-----
- AndroidManifest.xml 파일이 들어 있음
  - 앱의 여러 가지 정보를 담고 있는 중요한 파일
  - ‘매니페스트 파일’이라고 읽으며, 필요에 따라 수정하거나 변경
### Gradle Scripts 폴더
-----
- Gradle 빌드 시스템과 관련된 파일이 들어 있음
- 주요한 3개 파일
  - build.gradle (Module: app) : 빌드 스크립트 핵심 파일로 컴파일
버전, 실행되는 최하 버전, 컴파일 라이브러리 등을 등록
  - local.properties : 컴파일되는 SDK의 경로가 들어 있음
  - gradle.properties : JVM 관련 메모리가 설정되어 있음