# chpater 5 - 레이아웃 익히기

## 레이아웃의 기본 개념
----
**레이아웃은 ViewGroup 클래스로부터 상속받으며 내부에 무엇을 담는 용도**로 쓰임(위젯, 레이아웃)  
`View` : 컨테이너 역할하는 애들 집합임

### 레이아웃의 대표적인 속성
----
1. `orientation` : 수평, 수직 여부 결정(`vertical` : 수직, `horizontal` : 수평)
2. `gravity` : 위젯의 정렬 방향을 좌픅, 우측, 중앙 등으로 설정
   - 레이아웃 기준 위젯을 정렬함 (**해당 레이아웃에 있는 위젯을 어디에 배치할지 정해지는 것임**)
3. `layout_gravity` : 위젯 자신의 위치를 부모의 어느곳에 위치할지 결정함.(**위젯을 레아아웃 어느 방향에 배치할지 설정**) 
4. `padding` : 레이아웃 안에 배치할 위젯의 여백을 설정
5. `layout_weight` : 차지하는 공간의 가중값을 설정 (위젯들이 동일한 비율로 화면에 배치되도록)
6. `baselineAligned` : 위젯을 보기 좋게 정렬함(이때 위젯 테두리 맞춤이 아니라 위젯 내부 컨텐츠에 맞춰 정렬함)  
   <p>
   <div align = center>
    <img src="https://miro.medium.com/max/1080/1*GuOA2t0j_GsZe3XhmB-Czg.png"  width="300" height="500"/>
    </div>

[`gravity` VS `layout_gravity`]  
~~~XML
<Button
    android:layout_gravity = "center"
    android:gravity = "bottom|right"
    android:background = "#ff0000"
    android:text = "Hello World"
    android:textcolor = "#000000"/>
~~~  
<div align = center>

**이렇게 배치를 한다면 예상되는 화면은 아래와 같다**  
![이미지](https://velog.velcdn.com/images/723poil/post/39176a94-6ee4-45d6-a50c-0d0ec886242e/image.png)  
[출처](https://velog.io/@723poil/LinearLayout-%EC%84%A0%ED%98%95%EB%B0%B0%EC%B9%98)
</div>

\* **레이아웃도 View 클래스의 하위 클래스이므로 View클래스의 XML속성과 메서드 모두 사용 가능함.**
--


### 레이아웃의 종류
----
1. LinearLayout : 그냥 순차적으로 쌓기
2. RelativeLayout : **어떤 대상 기준 어느 방향인지 설정 가능**(다른 위젯으로 부터 상대적인 위치 지정)
3. FrameLayout : 주로 탭 같은거 만들 때 사용
4. TalbeLayout : 테이블 처럼 가능(행 확장은 힘듬)
5. GridLayout : 테이블 처럼 만드는 것이지만 행 확장 등, 확장성 좋음

----
[한 화면에서 위젯을 **수평과 수직으로 다양하게 배치해야 하는 경우**]  
- 리니어레이아웃 내부에 리니어레이아웃 생성하는 방식을 사용함.

~~~XML
<LinearLayout>
    <LinearLayout>
        위젯...
    </LinearLayout>
    <LinearLayout>
        위젯...
    </LinearLayout>
    <LinearLayout>
        위젯...
    </LinearLayout>
    <LinearLayout>
        위젯...
    </LinearLayout>
</LinearLayout>
~~~

[잠깐!]
> `match_parent` : 자신의 상위 객체에 같은 크기가 됨  
> `wrap_content` : 내용을 담을 크기면 충분함.  
> 중복 리니어레이아웃 작성시 주의해서 속성을 부여해야함.  
> 만약 `layout_weight` 속성이 있는 경우 비율이 동일 하기 때문에 `match_parent`를 하더라도 모든 위젯이 보인다.

[응용 - 빨 노 검 파란색 레이아웃 배치하기]

~~~XML
<!--전체 레이아웃-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"><!--수직으로 설정-->

    <!--빨간색/노란색/검은색 위해 만든 곳-->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:orientation="horizontal"><!--수평-->

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:background="#FF0000"><!--빨간색-->
        </LinearLayout>

        <!--노란색/검은색 나누기 위함-->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            android:layout_weight="1"><!--수직-->

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:background="#FFFF00"><!--노란색-->
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:background="#000000"><!--검은색-->
            </LinearLayout>
        </LinearLayout>
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:background="#0000FF"><!--파란색-->
    </LinearLayout>
</LinearLayout>
~~~

레이아웃 구조 : **전체 레이아웃을 감싸는 것** 1개, **각 색상을 채워넣을 레이아웃** 4개(빨 노 검 파), **빨/노/검 구역 나눌 레이아웃** 1개, **노/검 구역 나눌 레이아웃** 1개

## Kotlin 코드로 레이아웃 만들기
----
지금까지는 `activity_main.xml`에 화면을 구성한 후 `MainActivity.kt`의 `setContentView()` 메서드로 화면을 출력했음.
> `setContentView()`메서드가 호출 되어야 Activity 생성됨 즉, lateinit 임.
---
\* XML 없이 Kotlin을 작성하기 위해서는 기존의 **`setContentView()`**를 주석처리 Or 제거해야한다.
--

~~~Kotlin
// XML없이 리니어레이아웃 생성하기

val params = LinearLayout.LayoutParams(
             LinearLayout.LayoutParmas.MATCH_PARENT,
             LinearLayout.LayoutParmas.MATCH_PARENT)

// 이때 params 변수는 상수로 선언하는 것을 추천함.   

val baseLayout = LinearLayout(this) // 리니어 레이아웃 생성
// 레이아웃 속성 정의
baseLayout.orientation = LinearLayout.VERTICAL // 수직
baseLayout.setBackgroundColor(Color.rgb(0, 255, 0))

setContentView(baseLayout, params) // R.id.activity_main 같은 의미

/*
순서를 보면
레이아웃 속성 크기 정의하고
레이아웃 속성 정의하고
setContentView() 불러온다.
*/
~~~

~~~Kotlin
//버튼 만들기
val btn = Button(this) // 버튼 객체 생성(생각해보면 클래스이름() 형태라 인스턴스 만드는 느낌임)
btn.text = "버튼입니다" // 버튼 텍스트 속성 
btn.setBackgroundColor(Color.MAGENTA) 
baseLayout.addView(btn) // 레이아웃에 해당 버튼 위젯 삽입

btn.setOnClickListener { // 이벤트 
    Toast.makeText(applicationContext, "코드로 생성한 버튼입니다", Toast.LENGTH_SHORT).show()
}
~~~
<div align = center>
    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqZiMv%2FbtrgBDJKYj1%2FBOIksacRCjsmn7NCMkMeCk%2Fimg.png"  width="300" height="500"/>
</div>

[위 그림 만들기]
~~~Kotlin
val params = LinearLayout.LayoutParams(
             LinearLayout.LayoutParmas.MATCH_PARENT,
             LinearLayout.LayoutParmas.MATCH_PARENT)

val baseLayout = LinearLayout(this) // 리니어 레이아웃 생성
// 레이아웃 속성 정의
baseLayout.orientation = LinearLayout.VERTICAL // 수직
baseLayout.setBackgroundColor(Color.rgb(0, 255, 0))

setContentView(baseLayout, params) // R.id.activity_main 같은 의미

val edittext = EditText(this) // Edit Text 객체 생성
baseLayout.addView(edittext) // 레이아웃에 edittetx 삽입 
//레이아웃 변수.addView(삽입할 객체)

val btn = Button(this) // 버튼 객체 생성
btn.text = "버튼입니다"
btn.setBackgroundColor(Color.Yellow)
baseLayout.addView(btn) // 레이아웃에 삽입

val textview = TextView(this) // 텍스트뷰 객체 생성
baseLayout.addView(textview) // 레이아웃에 삽입


btn.setOnClickListener{ //버튼 이벤트 생성
    textview.text = edittext.text.toString() // EditText의 텍스를 바로 문자열로 캐스팅하고 텍스트뷰에 저장.
~~~


## 렐러티브레이아웃
----
<div align = center>
    <img src="https://velog.velcdn.com/images/ohjs00000/post/7c3c2c43-3ffc-4fcc-8d11-ec6e70d72205/image.png"  width="500" height="234"/>
</div>

~~~XML
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:text="위쪽" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_centerVertical="true"
        android:text="좌측" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="중앙" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_centerVertical="true"
        android:text="우측" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        android:text="아래" />

</RelativeLayout>
~~~
<div align = center>
    결과 화면<p>
    <img src="https://t1.daumcdn.net/cfile/tistory/27350745597540BE06"  width="500" height="800"/>
</div>


### 다른 위젯의 상대 위치에 배치
---
렐러티브 레이아웃 안에서 다른 위젯의 특정한 곳에 배치하는 방법도 있음  
다른 위젯의 아이드를 지정하면 됨 **(@+id/기준 위젯 아이디)**
> ex. 버튼을 기준으로 alignTop 위치에 두고싶다 => `android:layout_alignTop = "@+id/basebtn"`

<div align = center>
    <img src="https://velog.velcdn.com/images/ohjs00000/post/d5f62580-edd5-4b16-a72e-3bcf1dd93f2a/image.png"  width="500" height="260"/>
    <p>
    여기서 above, toRightOf, toLeftOf, below는 기준 위젯에서 상하좌우를 의미하며, 나머지 다른 세부 속성은 상하좌우에 대한 구체적인 위치를 의미
</div>

예를 들어, 왼쪽 위치의 상단에 두고싶으면
~~~XML
<Button 
    android:layout_alignTop ="@+id/baseBtn"
    android:layout_toLeftOf = "@+id/baseBtn"/>
    <!-- 이렇게 2개 필요함 -->
~~~


[응용]

~~~XML
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <Button
        android:id="@+id/baseBtn1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:text="기준1" />

    <Button
        android:id="@+id/baseBtn2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_centerVertical="true"
        android:text="기준2" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_above="@+id/baseBtn2"
        android:layout_toRightOf="@+id/baseBtn1"
        android:text="1번" />
        <!-- 기준 1의 오른쪽, 기준 2의 상단 부분에 위치 -->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_below="@+id/baseBtn1"
        android:text="2번" />
        <!-- 레이아웃의 오른쪽, 기준1의 아래 부분에 위치 -->
</RelativeLayout>
~~~

어떤 결과를 보일지 한번 해보길 바란다.

[응용]
~~~XML
<RelativeLayout
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_height="match_parent"
    android:layout_width="match_parent"
    android:orientation="horizontal"
    android:padding="10dp">


    <TextView
        android:id="@+id/number"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="전화번호" />
    
    <EditText
        android:id="@+id/editText1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_toRightOf="@+id/number" 
        android:hint="000 - 0000 - 0000"
        android:gravity="center"/>
    <Button
        android:id="@+id/btn1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/editText1"
        android:layout_alignRight="@+id/editText1"
        android:text="취소"/>
        <!-- editText 기준으로 아래 오른쪽 -->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_toLeftOf="@+id/btn1"
        android:layout_margin="30dp"
        android:layout_alignBaseline="@+id/btn1"
        android:text="확인"/>
        <!-- 취소 버튼 기준으로 왼쪽 같은 라인 -->
</RelativeLayout>
~~~

~~~XML
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding = '10dp'
    android:orientation="vertical">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <TextView
            android:id="@+id/tv1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text = "전화번호">
        </TextView>
        <EditText
            android:id="@+id/et1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="000 - 0000 - 0000"
            android:gravity="center">
        </EditText>
    </LinearLayout>
    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_gravity="right">
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="입력"
            android:layout_margin="10dp">
        </Button>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="취소"
            android:layout_margin="10dp">
        </Button>
    </LinearLayout>
</LinearLayout>
~~~


## 테이블 레이아웃
---
`TableRow`와 함께 사용됨

행의 수 : `TableRow`의 수
열의 수 : `TableRow`안에 포함됨 위젯의 수

[관련 속성]  
1. `layout_span` : 열을 합쳐서 표시하라 의미
2. `layout_colum` : 지정된 열에 현재 위젯 표시
3. `stretchColumns` : `TableLayout`자체에 설정하는 속성임. 지정된 열의 넗이를 늘리라는 의미 값이 *인 경우 모두 같은 크기로 확장됨.

~~~XML
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/tableLayout1"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <TableRow>

        <Button
            android:layout_width="60dp"
            android:text="1" />

        <Button
            android:layout_width="60dp"
            android:layout_span="2"
            android:text="2" />

        <Button
            android:layout_width="60dp"
            android:text="3" />
    </TableRow>

    <TableRow>

        <Button
            android:layout_width="60dp"
            android:layout_column="1"
            android:text="4" />
        <!-- 1열이라고 지정을 했음 -->
        <Button
            android:layout_width="60dp"
            android:text="5" />

        <Button
            android:layout_width="60dp"
            android:text="6" />
    </TableRow>

</TableLayout>
~~~