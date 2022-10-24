# Chpater 4 - 기본 위젯 익히기

## 뷰(View) 클래스
----
- **안드로이드 화면에서 실제로 사용되는 것들은 모두 View 클래스의 상속을 받음**
    - 따라서 View 클래스의 속성과 메서드를 상속받는다.

- 위젯이라고 부름
- 레이아웃
    - 다른 위젯을 담을 수 있는 위제을 특별히 레이아웃이라고 함
    - 레이아웃도 크게 보면 위젯에 포함됨
 
## 뷰와 뷰그룹
---
- 안드로이드에서의 위젯
    - 다른 프로그램 언어에서 컨트롤이라고 부르는 것들
        > 버튼, 텍스트뷰, 에디트텍스트, 라디오버튼, 이미지뷰 등

\* **껍데기는 XML에 작성, 실제 구현은 kt파일**  
----  

## 뷰 클래스 계층도 
---
- **안드로이드 화면에 나타나는 모든 위젯은 `View` 하위에 존재함**(최상위 클래스는 Object)

## View클래스의 XML속성
--- 
1. 버튼의 속성
    - xml 속성이 거의 없고 대개 상위 클래스인 `TextView` Or `View`에서 상속받는다.  
        - **크기 관련 속성 layout_width, layout_height 필수 요소임**
        - id의 경우 필수는 아니지만 작성하지 않으면 이벤트 사용 불가

2. id 속성
    - **코틀린 코드에서 버튼 등의 위젯에 접근할 때 id 속성에 지정한 아이디를 사용**(findViewById(R.id.xml의 id))
    
xml에서 `android:id = '@+id/~~~'` 형식으로 쓰인다.  
이를 코틀린에서 `위젯 변수 = findViewById<위젯>(R.id.위젯id)` 
>  btn1 = findViewById\<Button>(R.id.Btn1) 이런 형식이다.

\* **터치했을 때 어떤 동작이 필요한 경우 id 지정**
--

3. `layout_width`, `layout_height` 속성 : 모든 위젯에 필수로 들어감
    - `match_parent` : 부모의 너비에 꽉차는 크기
    - `warp_content`: 위젯 내부의 컨텐츠에 크기를 맞춤 ( ex. Button에 text속성이 버튼입니다. 경우 크기는 버튼입니다. 글자에 맞춤)  
<p>

4. 값을 숫자로 직접 지정하는 경우 : **단위에 주의할 것** (단위 : px)
    - AVD는 해상도가 1080 x 1920인 경우 너비(width)를 1080px, 높이를 1920px로 지정하면 match_parent처럼 보임.
<p>

5. `background` 속성 : 레이아웃 색상 지정

6. `padding` 및 `layout_margin` 속성
    - padding : **레이아웃의 경계선과 위젯 사이에** 여백을 둘 수 있다.
    - margin : **위젯과 위젯 사이에** 여백을 둘 수 있다.  
<p>

7. `visibility`속성 : 위젯을 보일 것인지 여부 결정(뭐 특정 버튼 누르면 보이도록 하는 방법에 쓰임)
    - `visible` : 디폴트로 설정되어 있으며, **보이는 상태**
    - `invisible` : 안보이는 상태이지만, **자신의 자리 유지함.**
    - `gone` : 안 보이는 상태, **원래 자신의 자리도 사라짐.**

<p>

8. `enabled`, `clickable` 속성 : Boolean타입의 값을 가지고 디폴트 값은 true임.
    - `enabled` : 위젯의 동작 여부
    - `clickable` : 클릭이나 터치가 동작 여부

9. `rotation` : 위젯을 회전시켜 출력 (값은 각도)

## TextView 
-----

- `text` 속성 : 문자열 형식으로 값을 직접 입력하거나 `@string/변수명` 형식으로 지정 후 string.xml파일에 지정 가능
- `textColor` 속성 : 글자 색상
- `textSize` 속성 : 글자 크기(단위 : dp, px, in, mm, sp)
- `typeface` 속성 : 글자의 글꼴 지정
- `textStyle` 속성 : 글자 스타일 지정(글꼴이랑 착각 금지)
- `singleLine` 속성 : **글이 길어 줄이 넘어갈 경우 강제로 한 줄까지만 출력 그뒤에 ...처리


## Kotlin코드로 XML속성 설정
---
~~~Kotlin
 override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // 변수 선언
        var tv1 : TextView
        var tv2 : TextView
        var tv3 : TextView

        // XML <-> kt 맵핑
        tv1 = findViewById<TextView>(R.id.textView1)
        tv2 = findViewById<TextView>(R.id.textView2)
        tv3 = findViewById<TextView>(R.id.textView3)

        tv1.setText("안녕하세요?") // android:text
        tv1.setTextColor(Color.RED) // android:textColor
        tv2.setTextSize(30.0f) // android:textsize
        tv2.setTypeface(android.graphics.Typeface.SERIF, android.graphics.Typeface.BOLD_ITALIC) // android:typeface
        tv3.setText("가나다라마바사아자차카타파하가나다라마바사아자차카타파하갸냐댜랴먀뱌샤")
        tv3.setSingleLine() // android:singleLing
    }
~~~

## Button과 EditText
---
[클래스 계층도]
- Object
    - View
        - TextView
            - Button, EditText, RadioButton, CheckBox, ToggleButton 등.

[버튼 이벤트 생성]  
`변수.setOnClickListener{}` 콜백 함수라고 부름(람다식 형태)  
`변수.setOnTouchListener{view, motionEvent}`  
\* **두 콜백함수의 차이점 : `setOnClickListener`의 경우 단순 터치시 동작함(터치만 인식함) 반면, `setOnTouchListener`는 터치, 드래그, 손가락 방향 등 다양한 액션을 인식 할 수 있다.**
--

[EditText 값 가져오기]   
`String 변수 = EditText객체.getText().toString()` == `String 변수 = EditText객체.text.toString()` 
**차이점은 kotlin 메서드(getText()) 이냐 XML 속성(text)이냐??** -> just 뇌피셜


[onCreate 메서드] : 이놈 호출시 Main_activity 페이지 생성됨 (lateinit)

## CompoundButton 클래스
---
[클래스 계층도]
- Object
    - View
        - TextView
            - Button  
                - CompoundButton
                    - Check Box, RadioButton, Switch, ToggleButton

특징 : **공통적으로 체크 또는 언체크 상태를 가질 수 있음**

1. 체크박스 : **독립 컨포넌트**
    - 여러 개의 체크박스가 있어도 서로 독립적으로 동작한다는 특징이 있어 여러 개를 동시에 체크할 수 있음.

[이벤트 구성] : `setOnCheckedChangeListener`
~~~Kotlin
// 체크박스가 변경될 때 동작하는 람다식
변수명.setOnCheckedChangeListener{compoundButton, b ->
    // 이때 b는 boolean 타입을 말함 (체크 됨/안됨)
    // 이벤트 실행 부
    if(변수.isChecked == true){
        // 체크 된 상태
    }else{
        // 체크 안된 상태
    }
}
~~~

2. 스위치와 토글버튼 : 주 용도는 온/오프 상태 표시
    - 똑같이 이벤트는 `setOnCheckedChangeListener` 사용함.

3. 라디오버튼과 라디오그룹 
    - **여러 개 중 하나만 선택해야 하는 경우에 사용**됨 (즉, 중복 x 단, **라디오 그룹과 같이 사용해야함**), **각 라디오 버튼마다 id가 있어야함**(없으면 선택된 것으로 fix되어버림)
    - **라디오그룹은 TextView 하위의 위젯들과는 성격이 조금 다르다**
        > `clearCheck()` 해당 라디오 그룹 내부의 체크된 것을 모두 해제함

~~~XML
<!-- 아래는 일부 속성이 생략된 코드임 -->
<RadioGroup
    android:id="@+id/rGroup1:"
    <RadioButton
        android1:id="@+id/radio1"
        android:text = "남성"/>
    <RadioButton
        android1:id="@+id/radio2"
        android:text = "여성"/>
    <!-- 라디오 그룹 내부에 2개의 라디오 버튼이 있음 -->
</RadioGroup>
<!-- 그룹 내부에 2개의 버튼이 있어서 둘 중 하나만 선택 가능함. -->
<!-- 그룹 밖에 2개 나열 하면 중복 선택 가능함 -->
~~~

## 이미지뷰와 이미지버튼
----
[클래스 계층도]
- Object
    - View
        - ImageView
            - ImageButton

**특징 : 이미지뷰에 보여줄 그림 파일은 일반적으로 프로젝트의 [res] -> [drawable] 폴더에 있어야 함.**

[이미지 불러오기]  
`android:src = "@drawable/그림 아이디(그림 파일 이름)`   

[관련 속성]
1. src : 이미지의 경로
2. maxHeight/maxWidth : 이미지의 크기 지정
3. scaleType : 이미지의 확대/축소 방식 지정
 
[mipmap 폴더] : 여기 있는 앱 아이콘 그림을 화면에 출력하면 **OS가 알아서 현재 안드로이드 폰의 해상도에 적잘한 이미지를 알아서 선택함**