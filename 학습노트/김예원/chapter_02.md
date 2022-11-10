# Chapter 02
## <실습 2-4>
<br>

### 기초 정리
- xmlns(xml name space): XML 요소의 이름 충돌을 피할 수 있는 방법을 제공함
  - 즉, XML에서 접두사를 사용해 이름 충돌을 피하고자 할 때 접두어에 대한 name space 정의
- 안드로이드 프로그래밍에서의 xmlns
  - xmlns:android: 안드로이드 SDK에 있는 기본 속성 사용
  - xmlns:app : 프로젝트에서 사용하는 외부 라이브러리에 포함되어있는 속성 사용
  - xmlns:tools : 안드로이드 스튜디오의 디자이너 도구 등에서 화면을 보여줄 때 사용
    - 이 속성은 앱이 실행될 때는 적용되지 않고, 안드로이드 스튜디오에서만 적용됨
- [출처](https://velog.io/@younsle/XML-%EC%86%8D%EC%84%B1-%EC%A0%95%EB%A6%AC-o7k11q4fx9)

<br>

### View Binding
- findViewById 문제점
  - Null 안정성: 개발자가 유효하지 않은 id를 사용하면 null 오류 발생 가능
  - Type 안정성: View type 잘못 작성해 casting 하면cast exception 발생 가능
  - 속도가 상대적으로 느림
- gradle 설정
  ```
  android{
    viewBinding {
        enabled true
    }
  }
  ```
- Activity
  ```kotlin
  private lateinit var binding: ActivityMainBinding
  binding = ActivityMainBinding.inflate(layoutInflater)
  setContentView(binding.root)
  ```
- [참고](https://developer.android.com/topic/libraries/view-binding?hl=ko)

<br>

### 실행 코드 
- MainActivity.kt
  ```kotlin
    class MainActivity : AppCompatActivity() {
        private lateinit var binding: ActivityMainBinding
        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            binding = ActivityMainBinding.inflate(layoutInflater)
            setContentView(binding.root)

            binding.button.setOnClickListener {
                Toast.makeText(applicationContext,"버튼 선택", Toast.LENGTH_SHORT).show()
            }
        }
    }
- activity_main.xml
    ```xml
    <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <Button
            android:id="@+id/button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/button_name"
            android:backgroundTint="@color/gray"
            android:layout_marginStart="10dp"
            android:layout_marginEnd="10dp"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintBottom_toBottomOf="parent"/>

    </androidx.constraintlayout.widget.ConstraintLayout>
    ```
<br>

### 실행 결과
![실행 결과](https://user-images.githubusercontent.com/101886039/201102198-ce1a5968-9111-4492-955a-98a28812fe0d.png)

<br>

### res 폴더
- drawable: 이미지 파일 등
- mipmap: 디자인 화면, 런처 아이콘
    - xxxhdpi, xxhdpi, xhdpi: 초고해상도 런처 아이콘 파일
    - hdpi: 고해상도 런처 아이콘 파일
    - mdpi: 중해상도 런처 아이콘 파일
- layout: XML 파일
- values
    - strings.xml: 문자열 저장
    - colors.xml: 색상표 저장
    - styles.xml: 스타일 저장
- menu: 메뉴 XML 파일 저장, 필요시 생성해서 사용
- anim: 애니메이션 저장

<br>

### Style, Theme 차이
- 둘 다 속성을 resource에 mapping하는 key-value 쌍이라는 동일한 기본 구조를 가짐
1. style
    - 특정 뷰 유형 지정<br>예) 특정한 하나의 스타일을 사용해 버튼 속성 지정 가능
    - style에서 지정하는 모든 속성은 layout 파일에서 설정할 수 있음
    - 모든 속성을 style로 추출하면 여러 위젯에서 손쉽게 속성 사용 및 관리 가능
2. theme
    - style, layout, widget 등으로 참조할 수 있는 명명된 resource 모음을 정의
    - theme는 colorPrimary와 같은 symentic 이름을 Android resource에 할당
- [참고](https://medium.com/androiddevelopers/android-styling-themes-vs-styles-ebe05f917578)

<br>

### Gradle Scripts 폴더
- Gradle Build System과 관련된 파일 들어있음
    - build.gradle(Module:app): 빌드 스크립트 핵심 파일로 compile version, minimum sdk, compile library 등을 등록
    - local.properties: 컴파일되는 SDK의 경로가 들어있음
    - gradle.properties: JVM 관련 메모리 설정

