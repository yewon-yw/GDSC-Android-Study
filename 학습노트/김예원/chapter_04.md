# Chapter 04
### 뷰(View) 클래스
- '위젯'이라고도 부름
- 레이아웃
  - 다른 위젯을 담을 수 있는 위젯
  - ViewGroup 클래스 아래 존재
- 뷰 컨테이너(view container)
  - 레이아웃이라 부르진 않지만 다른 뷰를 포함
  - ListView, GridView, TabHost, Gallery 등
  - ViewGroup 클래스에서 상속

<br>

### View 클래스 계층도
![image](https://user-images.githubusercontent.com/101886039/202501014-b485552c-93c5-4013-8bf4-9ec77f22e64c.png)

<br>

### View 클래스의 XML 속성
- id 속성
  - 모든 위젯의 id 나타냄
  - `@+id/` 형식
  - Kotlin 코드에서 위젯에 접근할 때 id 사용
- layout_width, layout_height 속성
  - 모든 위젯에 필수
  - `match_parent`, `wrap_content`
  - `px`, `dp` 로도 지정 가능
- background 속성
  - #RRGGBB 값으로 지정
  - 16진수(00 ~ FF)로 표현
- padding, layout_margin 속성
  - padding은 레이아웃의 경계선과 위젯 사이의 여백
  - margin은 위젯과 위젯 사이의 여백
- visibility 속성
  - visible: default 설정, 보이는 상태
  - invisible: 안보이는 상태지만 자리는 유지
  - gone: 안보이는 상태+자리도 사라짐
- enabled, clickable 속성
  - enabled: 위젯 동작 여부 true/false로 설정
  - clickable: 클릭, 터치 동작 여부를 true/false로 설정
- rotation 속성
  - 값은 각도로 지정

<br>

### TextView
- text 속성
  - 텍스트뷰에 나타나는 문자열
- textColor 속성
  - 글자 색상 지정
  - #RRGGBB, #AARRGGBB 형식
- textSize 속성
  - 글자 크기를 dp, px, in, mm, sp 단위로 지정
- typeface 속성
  - 글자 글꼴 지정
  - sans, serif, monospace 설정 가능, default는 normal 설정
- textStyle 속성
  - 글자 스타일 지정
  - bold, italic, bold|italic 설정 가능, default는 normal
- singleLine 속성
  - 글이 길어 한줄이 넘어갈 경우 문자열의 맨 뒤에 '...' 표시
  - true/false 설정 가능, default는 false
- 자주 사용하는 View, TextView 클래스의 XML 속성과 메소드
  <br>
  ![image](https://user-images.githubusercontent.com/101886039/202501189-eb680553-8170-478e-ba85-ca9012eeb956.png)

<br>

### 직접 풀어보기 4-3
![image](https://user-images.githubusercontent.com/101886039/202501241-e2ff1180-ec89-4607-8798-05f8a5b1b3f8.png)

<br>

### CompoundButton
- 버튼 클래스의 하위 클래스
- CheckBox
  - 여러개를 동시에 체크 가능
- Switch, ToggleButton
- RadioButton, RadioGroup
  - Group으로 묶인 RadioButton 중 하나만 선택 가능
  - 각 RadioButton의 id 속성이 필요
  - clearCheck() 메소드를 통해 해당 그룹 안의 RadioButton 체크 해제 가능

<br>

### ImageView
- 그림 출력 위젯
- src 속성: 이미지 경로
- maxHeight, maxWidth: 이미지 크기 지정
- scaleType: 이미지 확대/축소 방식 지정
  - matrix, fitXY, fitStart, fitEnd, center 등
  - [Android developers 참고](https://gdbagooni.tistory.com/15)
  - [Blog 참고](https://gdbagooni.tistory.com/15)
- 이미지 해상도: mdpi(48x48), hdpi(72x72), xhdpi(96x96), xxhdpi(144x144), xxxhdpi(192x192)
  
<br>

### 실습 4-2
![image](https://user-images.githubusercontent.com/101886039/202501371-e920d828-dff6-4c4d-ba26-eb6d16399d4a.png)

<br>

### 직접 풀어보기 4-4
![실습 화면](https://im.ezgif.com/tmp/ezgif-1-1d78a97ec7.gif)
