# Chapter 2 - 처음 만드는 안드로이드 애플리케이션

안드로이드 프로젝트 개발 단계 

|1번|안드로이드 프로젝트 생성|
|:--:|:-------:
|2번|화면 디자인 및 편집(.XML)|
|3번|Kotlin 코드 작성(.kt)|
|4번|프로젝트 실행 및 결과 확인(AVD)|
|5번|안드로이드 애플리케이션 개발 완료|

2. XML 파일에는 각 위젯의 **ID, 크기 등 속성 값이 들어있다.**
3. Kotlin 코드를 통해서 변수를 만들고 **위젯과 맵핑 및 이벤트를 호출한다.**


## 사소한 표준 룰
----
xml에서 위젯 다루기
~~~XML
<Button
    android:layout_width = "match_parent"
    android:layout_height = "wrap_content"
    android:id = "@+id/button1"
    android:text = "@string/strBtn1"> 
    <!-- text = @string/strBtn1 요놈의 의미는 -->
    <!-- [app] -> [res] -> [values] -> [strings.xml]에 저장돼있는 strBtn1 변수가 가지는 text를 이용하겠다는 의미임. -->
    <!-- 그냥 android:text = "버튼입니다" 이렇게 하면 직접적으로 위젯의 이름을 설정한다는 의미 -->
    <Button>
~~~


`activity_main.xml`에 작성된 `Button`에 대해 접근해야하므로 버튼에 대한 멤버변수를 하나 만들어야함.
~~~cpp
lateinit var button1 : Button // Button 객체를 가질 변수 선언.
//lateinit이라는 것은 필요할 때(이벤트 발생시 초기화 하겠다는 의미 즉, 동적 바인딩이다.)
// 이때 val(상수) 선언으로 되어있는지 check 필요함. (상수 선언시, 이벤트로 인한 값 변경 불가)
button = findViewById<Button>(R.id.xml에 작성한 버튼 id)
// 이때 Button 위젯에 관련된 클래스가 import되어 있어야함.
~~~

`Button`이벤트 생성하기
~~~cpp
button1.setOnClickListener {
    // 버튼 클릭시 작동할 내용 작성
    // setOnClickListener는 람다식으로 작성됨.
}
~~~
[정리]
1. 위젯 변수 선언. -> `lateinit var button1 : Button`
2. xml 위젯과 맵핑 -> `button1 = findViewById\<Button>(R.id.xml의 버튼 id)`
3. 이벤트 생성 -> `button1.setOnClickListener {}`

## 프로젝트에서 사용되는 폴더와 파일의 용도
----

[Java 폴더]  
하위에 **패키지명의 폴더가 있는데, 이는 안드로이드 프로젝트를 생성할 때 입력한 패키지 이름과 동일.**  
**이곳에 `MainActivity.kt` 있음**

[java (generated) 폴더]  
Android Studio 3.2 부터 제공됨.  **시스템 내부적으로 사용되므로 딱히 신경쓸게 없다.**

[res 폴더]  
앱 개발에 사용되는 **이미지(image), 레이아웃(layout), 문자열(String)** 등이 들어감.

- [drawable 폴더]  
    이미지 파일을 넣음

- [mipmap 폴더]
    디자인 화면이나 앱이 설치된 후에 보이는 런처 아이콘을 넣음

- [layout 폴더]
    액티비티(화면)을 구성하는 XML파일 들어있음 기본적으로 `activity_main.xml`이 초기화면임.

- [values 폴더]   
    문자열 저장하는 `string.xml` 색상표 저장하는 `colors.xml` 스타일 저장하는 `styles.xml`등이 들어 있음.

[res (generated) 폴더]  
Android Studio 3.5 제공됨 **내부적으로 사용되므로 신경쓸 필요없음**

[manifests 폴더]  
`AndroidManifest.xml`파일이 들어 있음
**앱의 여러가지 정보를 담고 있는 중요한 파일임**

[Gradle Scripts 폴더]  
`Gradle` 빌드 시스템과 관련된 파일 있음  
`build.gradle (Module: app)` : 빌드 스크립트 핵심 파일  
`local.properties` : 컴파일되는 SDK의 경로가 들어 있음  
`gradle.properties` : JVM 관련 메모리가 설정되어 있음

> Gradle : 그루비(Groovy)를 기반으로 한 빌드 도구이다. 
