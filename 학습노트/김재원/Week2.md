# Chapter3. 안드로이드를 위한 Kotlin 문법
## Kotlin의 개요
### Kotlin의 특징
-----
1. Java와 100% 상호 호환되므로 Java 코드를 완전히 대체 가능
2. Java보다 문법이 간결함
3. 프로그램의 안정성을 높여줌
4. var 또는 val 예약어를 통해 데이터 형식을 선언하지 않고 변수를 선언할 수 있음

### 예제 3-1 빈 화면에 간단한 입력해보기
-----
![예제3-1](https://user-images.githubusercontent.com/111935711/198816314-be248f8c-2f49-4f75-bd9a-e309825d4dec.jpg)

### 예제 3-2 데이터 타입별 번수 선언, 대입, 출력
-----
![예제3-2](https://user-images.githubusercontent.com/111935711/198816442-05d06b04-5366-4b31-b78c-e76b640198df.jpg)

## Kotlin의 기본 문법
### 변수와 데이터 형식 
-----
- 문자형
  1. Char - 2byte를 사용하며 한글 또는 영문 1개만 입력
  2. String - 여러 글자의 문자열을 입력
- 정수형
  1. Byte - 1byte를 사용하며 -128 ~ +127까지 입력
  2. Short - 2byte를 사용하며 -32768 ~ +32767까지 입력
  3. Int - 4byte를 사용하며 약 -21억 ~ +21억까지 입력
  4. Long - 8byte를 사용하며 상당히 큰 정수까지 입력 가능
- 실수형
  1. Float - 4byte를 사용하며 실수를 입력
  2. Double - 8byte를 사용하며 실수를 입력, Float보다 정밀도가 높음
- 불리언형
  1. Boolean - true 또는 false를 입력

### 변수 선언 방식
-----
- 암시적 선언
  - 변수의 데이터 형식을 지정하지 않고, 대입되는 값에 따라 자동으로 변수의 데이터 형식이 지정
    - 단, 초기화하지 않는 경우에는 데이터 형식을 반드시 명시해야 함. 
    ```
    var var1 = 10
    var var2 = 10.1f
    var var3 = 10.2
    var var4 = '안'
    var var5 = "안드로이드"
    ```
- var(variable)
  - 일반 변수를 선언할 때 사용
  - 필요할 때마다 계속 다른 값을 대입 가능
  ```
  var myVar : Int = 100
  myVar = 200 // 정상
  ```
- val(value)
  - 변수 선언과 동시에 값을 대입하거나, 초기화 없이 선언한 후에 한 번만 값을 대입 가능
  - 한 번 값을 대입하고 나면 값을 변경 할 수 없음
  ```
  val myVal : Int = 100
  myVal = 200 // 오류
  ```

### 데이터 형식 변환
-----
- 캐스팅 연산자 사용
- Kotlin에서 제공하는 toInt()나 toDouble() 등의 정적 메소드 사용
  ```
  var a : Int = "100".toInt()
  var b : Double = "100.123".toDouble()
  ```

### null 사용
-----
- Kotlin은 기본적으로 변수에 null 값을 넣지 못함
  - 변수를 선언할 때 데이터 형식 뒤에 ?를 붙여야 null 대입 가능
  ```
  var notNull : Int = null // 오류
  var okNull : Int? = null // 정상
  ```

- 변수가 null 값이 아니라고 표시해야 하는 경우에는 !!로 나타냄
  - 이 경우 null 값이 들어가면 오류 발생
  ```
  var ary = ArrayList<Int>(1) // 1개짜리 배열 리스트
  ary!!.add(100) // 값 100을 추가
  ```

## 반복문, 배열, 조건문
### 조건문 if, when
-----
- if 문
  - 조건이 true인지 false인지에 따라서 어떤 작업을 할 것인지를 결정
  - 이중 분기라고도 부름
  - if 문의 형식
    ```
    if(조건식) {
      // 조건식이 true 일 때 이 부분 실행
    }
    ```
  - if-else 문의 형식
    ```
    if(조건식) {
      // 조건식이 true 일 때 이 부분 실행
    } else {
      // 조건식이 false 일 때 이 부분 실행
    }
    ```
- when 문
  - 여러 가지 경우에 따라서 어떤 작업을 할 것인지를 결정
  - 다중 분기라고도 부름
  - when 문의 형식
    ```
    when(식){
        값1 -> // 값1이면 이 부분 실행
        값2 -> // 값2이면 이 부분 실행
        .
        .
        .
        else -> 어디에도 해당하지 않으면 이 부분 실행
    }
    ```
- 실습
![조건문예제](https://user-images.githubusercontent.com/111935711/198817978-8f8aa409-21ee-477f-9ae9-8c529a397fcf.jpg)

- when 문의 처리 방법
  - 각각의 값에 따라 처리
  - 범위로 처리 : in 키워드 사용
    ```
    var jumsu : Int = count
    when(jumsu) {
        in 90 .. 100 -> println("when문 합격(장학생)")
        in 60 .. 89 -> println("when문 합격")
        else -> println("when문 불합격")
    }
    ```

### 배열
-----
- 배열 - 여러 개의 데이터를 하나의 변수에 저장하기 위해 사용
![배열의개념](https://user-images.githubusercontent.com/111935711/198818232-aae22261-de0b-4a13-b760-8eb3384acc8f.jpg)

- 일차원 배열 선언 형식
  ```
  var 배열명 = Array<데이터 형식>(개수, {초깃값})
  var 배열명 = Array<데이터 형식>(개수) {초깃값}
  ```
  - 일차원 배열(one[4])를 선언하고 값을 대입하는 방법
    ```
    var one = Array<Int>(4, {0})
    one[0] = 10
    one[3] = 20
    ```
- 이차원 배열 선언 형식
  ```
  var 배열명 = Array<배열 데이터 형식>(행 개수, {배열 데이터 형식(열 개수)})
  ```
  - 3×4 이차원 배열(two[3][4])을 선언하고 값을 대입하는 방법
    ```
    var two = Array<IntArray>(3, {IntArray(4)})
    two[0][0] = 100
    two[2][3] = 200
    ```
- 배열을 선언하면서 값을 바로 대입하는 것도 가능
  ```
  var three : IntArray = intArrayOf(1, 2, 3)
  ```
- ArrayList
  ```
  var one = ArrayList<Int>(4)
  one.add(10)
  one.add(20)
  var hap = one.get(0) + one.get(1) // 첫 번째 값 + 두 번째 값
  ```
### 반복문 for, while
-----
- for 문
  ```
  for (변수 in 시작..끝 step 증가량){
    // 이 부분을 반복 실행
  }
  ```
  - 배열의 개수만큼 변수에 대입하여 반복하는 방법
    ```
    for (변수 in 배열명.indices) {
        // 이 부분을 반복 실행
    }
    ```
  - 배열의 모든 값을 출력하는 방법
    ```
    var one : IntArray = intArrayOf(10, 20, 30, 40)
    for (i in one.indices){
        println(one[i])
    }
    ```
  - 첨자(i) 없이 바로 배열의 값을 하나씩 처리하는 방법
    ```
    for (변수 in 배열명){
        // 이 부분에서 변수 사용
    }
    ```
    - 배열의 내용이 하나씩 변수에 대입된 후 for 문 내부 실행 (배열의 개수만큼 for 문이 반복됨)
- while 문
  ```
  while (조건식) {
    // 조건식이 true인 동안 이 부분을 실행
  }
  ```

- break 문
  - 반복문을 빠져나올 때 사용

- countinue 문
  - 반복문의 조건식으로 건너뛸 때 사용
  
- 실습
![반복문예제](https://user-images.githubusercontent.com/111935711/198819018-0432006b-69d9-4619-885d-33e4b9087bec.jpg)

## 메소드와 전역변수 지역변수
### 메소드
-----
- 기본 메스드인 main()함수 외에 사용자가 메소드를 추가로 생성할 수 있음
- 메소드를 호출할 때 파라미터를 넘길 수 있음
- 메소드에서 사용된 결과를 return 문으로 돌려줄 수 도 있음.

### 변수
-----
- 전역변수(global variable)
  - 전역변수는 모든 메소드에서 사용됨
- 지역변수(local variable)
  - 메소드 내부에서만 사용됨
- 실습
![메소드와전역변수실습](https://user-images.githubusercontent.com/111935711/198819831-644fbc5f-3447-4ccf-b812-0738c97dbe04.jpg)

## 예외처리 try-catch
### 예외
-----
- Kotlin 프로그램 실행 중에 발생하는 오류
  - try-catch 문을 통해 이 오류를 처리
  ![예외처리실습](https://user-images.githubusercontent.com/111935711/198819962-8e11441b-075b-414e-9809-666ba8a3bf83.jpg)

## 연산자
### 주로 사용되는 Kotlin 연산자
-----
|**연산자**|**설명**|
|:--:|:------:|
|+, -, *, /, %|사칙 연산자|
|+, -|부호연산자로 변수, 수, 식 앞에 붙임|
|=|대입 연산자로 오른쪽을 왼쪽에 대입|
|++, --|1식 증가 또는 감소|
|==, ===, !=, !==, <, >, <=, >=|비교연산자로 true 또는 false를 반환|
|&&, \|\|, !|논리 연산자로 and, or, not을 의미|
|and, or, xor, inv()|비트 연산자로 비트 단위로 and, or, exclusive or, not 연산|
|shr, shl|시프트 연산자로, 비트 단위로 왼쪽 또는 오른쪽으로 이동|
|+=, -=, *=, /=|복합 대입 연산자|
|toByte(), toShort(), toInt(), toLong(), toFloat(), toDouble(), toChar()|데이터 형식을 강제로 변환하는 함수|

## 클래스 정의와 인스턴스 생성
### 클래스
- 변수(필드)와 메소드로 구성
- 객체지향 관점에서의 클래스
  - 실세계의 객체들이 가질 수 있는 상대와 행동
![클래스와인스턴스](https://user-images.githubusercontent.com/111935711/198862274-8961bc3a-c238-49e2-af47-0b47162e5f8a.jpg)
- 자동차 클래스를 구현
```
class Car {
  var color : String = ""
  var speed : Int = 0

  fun upSpeed(value : Int) {
    if (speed + value >= 200){
      speed = 200
    } else {
      speed = speed + value
    }
  }
  fun downSpeed(value : Int) {
    if (speed - value <= 0) {
      speed = 0
    } else {
      speed = speed - value
    }
  }
}
```
- Car 클래스를 인스턴스로 생성
```
fun main() {
  var myCar1 : Car = Car()
  myCar1.color = "빨강"
  myCar1.speed = 0

  var myCar2 : Car = Car()
  myCar2.color = "파랑"
  myCar2.speed = 0

  var myCar3 : Car = Car()
  myCar3.color = "초록"
  myCar3.speed = 0

  myCar1.upSpeed(50)
  println("자동차1의 색상은 " + myCar1.color + "이며, 속도는 " + myCar1.speed+ "km 입니다.")

  myCar2.upSpeed(20)
  println("자동차1의 색상은 " + myCar2.color + "이며, 속도는 " + myCar2.speed+ "km 입니다.")

  myCar3.upSpeed(50)
  println("자동차1의 색상은 " + myCar3.color + "이며, 속도는 " + myCar3.speed+ "km 입니다.")
}
```
## 생성자
- Car.kt에 생성자 코드 추가
```
class Car {
  var color : String = ""
  var speed : Int = 0

  constructor(color : String, speed : Int){
    this.color = color
    this.speed = speed
  }

  ~~~ 생략
}
```
- Car 클래스를 사용한 myCar1, myCar2, myCar3의 내용 변경
```
fun main() {
  var myCar1 : Car = Car("빨강", 0)
  var myCar2 : Car = Car("파랑", 0)
  var myCar3 : Car = Car("초록", 0)

  ~~~ 생략
}
```
## 메소드 오버로딩
- 한 클래스 내에서 메소드의 이름이 같아도 파라미터의 개수나 데이터 형식만다르면여러 개를 선언할 수 있음
- Car.kt에 메소드 오버로딩 추가
```
class Car {
  var color : String = ""
  var speed : Int = 0

  constructor(color : String, speed : Int) {
    this.color = color
    this.speed = speed
  }

  constructor(speed : Int){
    this.speed = speed
  }
  constructor() {
  }

  ~~~ 생략
}
```
## 정적 필드, 정적 메소드, 상수 필드
### 정적 필드(static field)
-----
- 인스턴스를 생성하지 않고 클래스 자체에서 사용되는 변수
- companion object {} 안에 작성하여 정적 필드를 만듦

### 정적 메소드(static method)
-----
- 메소드 또한 companion object {} 안에 작성하면 됨
- 인스턴스를 생성하지 않고도 '클래스명.메소드명()'으로 호출하여 사용 가능

### 상수 필드
-----
- 정적 필드에 초깃값을 입력하고 const val로 선언
- 선언한 후에는 값을 변경할 수 없음
- 상수 필드는 대문자로 구성하는 것이 일반적임
- 클래스 안에 상수를 정의할 때 사용
- Car.kt에 정적 구성 요소 추가
```
class Car {
  var color : String = ""
  var speed : Int = 0
  companion object {
    var carCount : Int = 0
    const val MAXSPEED : Int = 200
    const val MINSPEED : Int = 0
    fun currentCarCount() : Int {
      return carCount
    }
  }

  constructor(color : String, speed : Int) {
    this.color = color
    this.speed = speed
    carCount ++
  }

  ~~~ 생략
}
```
```
fun main() {
  var myCar1 : Car = Car("빨강", 0)
  var myCar2 : Car = Car("파랑", 0)
  var myCar3 : Car = Car("초록", 0)

  println("생산된 차의 대수(정적 필드) ==> " + Car.carCount)
  println("생산된 차의 대수(정적 메소드) ==> " + Car.currentCarCount())
  println("차의 최고 제한 속도 ==> " + Car.MAXSPEED)
  //생산된 차의 대수(정적 필드) ==> 3
  //생산된 차의 대수(정적 메소드) ==> 3
  //차의 최고 제한 속도 ==> 200

  println("PI의 값 ==> " + Math.PI)
  println("3의 5제곱 ==> " + Math.pow(3.0, 5.0))
  //PI의 값 ==> 3.141592653589793
  //3의 5제곱 ==> 243.0
}
```

## 클래스 상속과 메소드 오버라이딩
### 클래스 상속(inheritance)
-----
- 기존의 클래스가 가지고 있는 것을 그대로 물려받으면서 필요한 필드나 메소드를 추가로 정의하는 것을 의미
- 클래스와 상속의 개념
![클래스와상속의개념](https://user-images.githubusercontent.com/111935711/198863071-a6ea1d4f-9f24-4c5c-90b2-3a8b8267398c.jpg)

### 슈퍼클래스(superclass 또는 부모클래스)
-----
- 그림에서의 자동차 클래스를 의미

### 서브클래스(subclass 또는 자식클래스)
-----
- 그림에서의 승용차 클래스나 트럭 클래스를 의미
- 서브클래스는 슈퍼클래스의 모든 필드와 메소드를 상속받음
  - 별도의 선언이나 정의 없이도 슈퍼클래스의 필드와 메소드 사용 가능

### 메소드 오버라이딩(overriding)
- 슈퍼클래스의 메소드를 무시하고 새로 정의하는 것을 의미
  - 승용차 클래스의 '속도 올리기()' 메소드는 슈퍼클래스의 메소드를 재정의
- 승용차 클래스
```
open class Car {
  ~~~ 생략
  open fun upSpeed(value : Int){
    if (speed + value >= 200)
    ~~~ 생략
  }
}

class Automobile : Car {
  var seatNum : Int = 0

  constructor() {
  }
  fun countSeatNum() : Int {
    return seatNum
  }

  override fun upSpeed(value : Int) {
    if (speed + value >= 300){
      speed = 300
    } else {
      speed = speed + value
    }
  }
}
```
- 서브클래스 사용
```
fun main() {
  var auto : Automobile = Automobile()
  auto.upSpeed(250)
  println("승용차의 속도는 " + auto.speed + "km 입니다.")
  //승용차의 속도는 250km 입니다.
}
```

## 추상 클래스와 추상 메소드
### 추상(abstract) 클래스
-----
- 인스턴스화를 금지하는 클래스
- 추상 클래스는 클래스 앞에 abstract 키워드를 붙여서 지성
- 인스턴스화란 서브클래스 사용 예제의 2행과 같이 클래스로 인스턴스를 생성하는 것을 의미

### 추상 메소드
-----
- 본체가 없는 메소드
- 메소드 앞에 abstract 키워드르 붙여서 지정
  - 추상 메소드를 포함하는 클래스는 추상 클래스로 지정해야 함

### 추상 클래스와 추상 메소드를 사용하는 목적
-----
- 공통적으로 사용되는 기능을 추상 메소드로 선언 해놓고, 추상 클래스를 상속받은 후에 추상 메소드를 오버라이딩해서 사용하기 위함
- "구현한다" → 추상 메소드를 오버라이딩하는 것을 의미
- 동물 클래스를 추상 클래스로 만들고 추상 메소드인 '이동한다()'를 포함하는 예제
![추상클래스와추상메소드](https://user-images.githubusercontent.com/111935711/198863615-6d5f21e0-2264-4ac2-a78d-b16fd6a0c3bb.jpg)
- 그림을 구현한 예제
```
abstract class Animal {
  var name : String = ""
  abstract fun move()
}

class Tiger : Animal() {
  var age : Int = 0
  override fun move() {
    println("네 발로 이동한다.")
  }
}

class Eagle : Animal() {
  var home : String = ""
  override fun move() {
    println("날개로 날아간다.")
  }
}

fun main() {
  var tiger1 = Tiger()
  var eagle1 = Eagle()

  tiger1.move()
  eagle1.move()
  //네 발로 이동한다.
  //날개로 날아간다.
}
```

## 클래스 변수의 다형성
### 다형성(polymorphism)
-----
- 서브클래스에서 생성한 인스턴스를 자신의 클래스 변수에 대입할 수 있는 것을 의미
- 하나의 변수에 여러 종류의 인스턴스를 대입할 수 있음
```
fun main() {
  var animal : Animal

  animal = Tiger()
  animal.move()
  //네 발로 이동한다.

  animal = Eagle()
  animal.move()
  //날개로 날아간다.
}
```

## 인터페이스와 다중 상속
### 인터페이스(interface)
-----
- 추상 클래스와 성격이 비슷함
- interface 키워드를 사용하여 정의하고 내부에는 추상 메소드를 선언함
- 클래스에서 인터페이스를 받아 완성할 때 상속과 마찬가지로 ' : 인터페이스 이름' 형식을 사용
- 인터페이스는 '상속받는다'고 하지 않고 '구현한다'고 함
- Kotlin은 다중 상속을 지원하지 않음
  - 대신 인터페이스를 사용하여 다중 상속과 비슷하게 작성할 수 있음
```
abstract class Animal {
  var name : String = ""
  abstract fun move()
}

interface iAnimal {
  abstract fun eat()
}

class iCat : iAnimal {
  override fun eat() {
    println("생선을 좋아한다.")
  }
}

class iTiger : Animal(), iAnimal {
  override fun move() {
    println("네 발로 이동한다.")
  }
  override fun eat() {
    println("멧돼지를 잡아먹는다.")
  }
  
class Eagle : Animal() {
  var home : String = ""
  override fun move() {
    println("날개로 날아간다.")
  }
}

fun main() {
  var cat = iCat()
  cat.eat()
  //생선을 좋아한다.

  var tiger = iTiger()
  tiger.move()
  tiger.eat()
  //네 발로 이동한다.
  //멧돼지를 잡아먹는다.
}
}
```

## 람다식
### 람다식(lambda expression)
-----
- 함수를 익명 함수(anonymous function) 형태로 간단히 표현 한 것
- 코드가 간결해져서 가독성이 좋아짐
- 람다는 {} 안에 매개변수와 메소드의 모든 내용을 선언
- 파라미터 2개를 받아서 합계를 출력하는 일반적인 메소드 형식
```
fun addNumber(n1 : Int, n2 : Int) : Int {
  return n1 + n2
}
```
- 이것을 람다식으로 간단히 표현 가능
```
val addNumber = {n1 : Int, n2 : Int -> n1 + n2}
```

### 람다식의 특징
-----
1. 람다식은 {}로 감싸며 fun 예약어를 사용하지 않음
2. {} 안 ->의 왼쪽은 파라미터, 오른쪽은 함수의 내용
3. -> 오른쪽 문장이 여러개라면 세미콜론(;)으로 구분
4. 내용 중 마지막 문장은 반환값(return)임

## 패키지
- 클래스와 인터페이스가 많아지면 관리하기가 어렵기 때문에 패키지 단위로 묶어서 관리
  - 사용자가 생성한 클래스가 포함될 패키지는 *.kt 파일 첫 행에 아래와 같이 지정
  ```
  package 패키지명
  ```
- 안드로이드에서 제공하는 패키지 목록 확인 [링크](https://developer.android.com/reference/kotlin/packages)


## 제네릭스(Generics)
- 데이터 형식의 안전성을 보장하는데 사용
  - 제네릭스를 사용하여 strList에 문자열만 들어가도록 설정할 수 있음
    - 다음 코드의 마지막 행은 오류가 발생
    ```
    var strList = ArrayList<String>(4)
    strList.add("첫 번째")
    strList.add("두 번째")
    strList.add(3)
    ```
- 제네릭스는 \<String>뿐 아니라 \<Int>, \<Double> 등을 사용할 수 있음
- 사용자가 정의한 클래스 형에도 사용 가능

## 문자열 비교, 날짜 형식
### 문자열 비교
-----
- String 클래스의 equals() 메소드 사용
```
var str : String = "안녕하세요"
if(str.equals("안녕하세요")){
  //문자열이 같으면 이 곳을 수행
}
```
### 날짜 형식
-----
- DateFormat 클래스를 상속받은 SimpleDate Format 사용
- '연월일'이나 '시분초'와 같은 일반적인 표현이 가능
```
import java.text.DateFormat
import java.text.SimpleDateFormat
import java.util.*

fum main() {
  var now = Date()
  var sFormat : SimpleDateFormat

  sFormat = SimpleDateFormat("yyyyMMdd")
  sFormat = SimpleDateFormat("HH:mm:ss")
  println(sFormat.format(now))
  //23:15:21 형식으로 출력
}
```
# Kotlin 람다함수 추가 설명
## 람다 함수 구조
### 함수 타입 선언
-----
- 함수 타입이란 함수를 선언 할 때 나타내는 매개변수와 반환 타입을 의미
  - 일반 함수 선언
  ```
  fun some(no1 : Int, no2 : Int) : Int {
    return no1 + no2
  }
  ```
  - 함수 타입을 이용해 함수를 변수에 대입
  ```
  val some : (Int, Int)A -> Int = { no1 : Int, no2 : Int -> no1 + no2 }
  ```

## 람다식의 구성
### 변수에 지정된 람다식
-----
![람다식의구성](https://user-images.githubusercontent.com/111935711/198864683-c450012f-b692-4eff-b3eb-fae978450e07.jpg)

### 표현식이 2줄 이상일 때
-----
```
val multi2 : (Int, Int) -> Int = {
  x : Int, y : Int ->
  println("x * y")
  x * y // 마지막 표현식이 반환
}
```

### 자료형의 생략
-----
```
val multi : (Int, Int) -> Int = { x : Int, y : Int -> x * y} // 생략되지 않은 전체 표현
val multi = { x : Int, y : Int -> x * y} // 선언 자료형 생략
val multi : (Int, Int) -> Int = { x, y -> x * y} // 매개변수 자료형 생략
```

### 반환 자료형이 없거나 매개변주가 하나 있을 때
- 반환 자료형이 없으면 화살표 표기법도 사라짐(반환 타입이 없는 경우 Unit으로 표기)
-----
```
val greet : () -> Unit = { println("Hello, World!") }
val square : (Int) -> Int = { x -> x * x }
```

### 람다식 안에 람다식이 있는 경우
-----
- 작성은 가능하지만 자주 사용하지 않음
```
val nestedLambda : () -> () -> Unit = { { println("nested") } }
```

### 선언부의 자료형 생략
-----
```
val greet = { println("Hello, World!") } // 추론 가능
val square = { x : Int -> x * x } // 선언 부분을 생략하려면 x의 자료형을 명시
val nestedLambda = { { println("nested") } } // 추론 가능
```

## 람다 함수와 고차 함수
### 매개변수가 1개인 람다 함수
-----
- 람다 함수의 매개변수가 1개일 때는 매개변수를 선언하지 않아도 it 키워드로 매개 변수를 이용할 수 있음
- 매개변수가 1개인 람다 함수
```
fun main() {
  val some = {no : Int -> println(no)}
  some(10)
  // 10
}
```
- 매개변수가 1개인 람다함수에 it키워드 사용
```
fun main() {
  val some : (Int) -> Unit = {println(it)}
  some(10)
  // 10
}
```

### 람다 함수의 반환
-----
- 람다 함수에서는 return문 사용 불가능
- 람다 함수의 반환값은 본문에서 마지막 줄의 실행 결과
- 람다 함수에서 return문 사용 오류
```
val some = { no1 : Int, no2 : Int -> return no1 * no2} // 오류
```
- 람다 함수의 반환문
```
fun main() {
  val some = {no1 : Int, no2 : Int ->
    println("In Lambda function")
    no1 * no2
  }
  println("result : ${some(10, 20)}")
  // In Lambda function
  // result : 200
}
```
### 고차함수
-----
- 함수를 매개변수로 전달받거나 반환하는 함수를 의미
- 일반적으로는 람다식을 매개변수로 받거나 결과로 리턴하는 함수를 의미
- 코드 조각을 람다로 만들면 코드 중복 제거(고차함수의 목적)
```
fun calculator(a : Int, b : Int, operation : (Int, Int) -> Int = operation(a, b))

fun main(args : Array<String>?) {
  val sum = {x : Int, y : Int -> x + y}
  println(calculator(1, 2, sum))
  println(calculator(4, 3, {a : Int, b : Int -> a - b}))
}
```
- 고차함수 : 매개변수 및 리턴 모두 사용하는 고차함수 예제
![고차함수](https://user-images.githubusercontent.com/111935711/198865485-82980dcd-7696-436f-a742-4b4552de4450.jpg)
- 매개변수에 람다식이 있는 경우 : 고차함수 호출 방법 예제
```
fun main() {
  var result : Int // 람다식을 매개변수의 인자로 사용한 함수
  result = highOrder({x, y -> x + y}, 10, 20)
  println(result)
}

fun highOrder(sum : (Int, Int) -> Int, a : Int, b : Int) : Int {
  return sum(a, b)
}
```

### Call by Value
-----
```
fun main() {
  val result = callByValue(lambda()) // 람다식 함수를 호출
  println(result)
}
fun callByValue(b : Boolean) : Boolean { // 일반 변수 자료형으로 선언된 매개변수
  println("callByValue function)
  return b
}
val lambda: () -> Boolean = { // 람다 표현식이 두 줄
  println("lambda function")
  true // 마지막 표현식 문장의 결과가 반환
}
```

### Call by Name
-----
```
fun main() {
  val result = callByName(otherLambda) // 람다식 이름으로 호출
  println(result)
}
fun callByName(b : () -> Boolean) : Boolean { // 람다식 함수 자료형으로 선언된 매개변수
  println("callByName function)
  return b()
}
val otherLambda: () -> Boolean = {
  println("otherLambda function")
  true
}
```

### 다른 함수의 참조에 의한 호출
-----
```
fun sum(x : Int, y : Int) = x + y
funcParam(3, 2, sum) // 오류(sum은 람다식이 아님)

fun funcparam(a : Int, b : Int, c:(Int, Int) -> Int) : Int {
  return c(a, b)
}

funcparam(3, 2, ::sum)
```