# Chapter 3 - 안드로이드를 위한 Kotlin 문법

## Kotlin의 특징
---
1. Java와 100% 상호 호환됨 
2. **Java보다 문법이 간결함** 
3. 프로그램의 안정성을 높여줌 (왜?)
4. `var` OR `val` 예약어를 통해 데이터 형식을 선언하지 않고 변수 선언 가능.

Kotlin으로 Hello world 출력
~~~Kotlin
fun main(){
    println("안드로이드를 위한 Kotlin 연습")
    // 세미콜론 없음 python 처럼.
}
~~~

### 변수와 데이터 형식
---
정수형, 실수형, 문자형, 문자열 변수 선언하기.

~~~Kotlin
fun main(){
    var var1 : Int = 10
    var var2 : Float = 10.1f  // Float 타입은 f 붙어야함. (자바도 그랬던것 같기도,,,)
    var var3 : Double = 10.2
    var var4 : Char = '안'
    var var5 : String = '안드로이드'

    // var 변수명 : 타입 = 초기값
    // var 변수명 : 타입
    // 각 타입 이름 첫 글자는 항상 대문자!

}
~~~

### Kotlin의 변수 선언 방식
---
1. 암시적 선언 : 변수의 데이터 형식을 지정하지 않고, 대입되는 값에 따라 자동으로 변수의 데이터에 형식이 지정 ex) `var va1 = 10.1f` Float 타입 의미  
    \* **단, 초기화 하지 않은 경우에는 데이터 형식을 반드시 명시 해야함.**

~~~Kotlin
fun main(){
    var va1 : Int // 초기화 하지 않는 경우 타입 명시
    var va1 : Int = 10 // 정석
    var va1 = 10 // 암시적 선언
}
~~~

2. 데이터 형식 변환(타입 캐스팅) : 캐스팅 연산자 사용 (`toInt()`, `toDouble()`) 즉, 정적 Method 사용  
    \* **코틀린은 b = (float)a 이런 문법 지원 x ** (즉, 묵시적 타입 캐스팅 안됨)**

~~~Kotlin
fun main(){
    var a : Int : "100".toInt() // 문자열 -> 정수
    var b : Double : "100.123".toDouble() // 문자열 -> 실수
}
~~~

3. Null 사용 : 코틀린은 기본적으로 변수에 Null 넣을 수 없음.  
    \* **변수 선언시 데이터 형식 뒤 ? 를 붙여야됨**

~~~Kotlin
fun main(){
    var noNull : Int = null // 오류
    var okNull : Int? = null // 정상
    
    var ary = ArrayList<Int>(1) // 1개짜리 배열 리스트 생성
    ary!!.add(100) // 값 100을 추가
    ary!!.add(null) // 오류
}
~~~

### Kotlin 조건문 if, when
---
1. if(이중 분기)

~~~Kotlin
fun main(){
    if(조건식){
        // true 실행문
    }
    else{
        false 실행문
    }
}
~~~

**2. when** : 스위치랑 유사함.(다중 분기)

~~~Kotlin
fun main(){
    when(식){
        값1 -> 실행문 // 값1이면 이 부분 실행
        값2 -> 실행문 // 값2이면 이 부분 실행
        else -> //어디에도 해당 없으면 이 부분 실행 (스위치의 default랑 유사)
    }
}
~~~

[종합적인 예시]
~~~Kotlin
fun main(){
    var count : Int = 85
    if(count >= 90){
        println("합격")
    }
    else if(count >= 60){
        println("합격인데 좀 에매")
    }else{
        println("fail")
    }

    var jumsu : Int = (count/10) * 10
    when(jumsu){
        100 -> println(100점)
        90 -> printlnt(90점)
        80,70,60 -> println("합격") //여러개 쌉가능
        else -> println("fail")
    }
}
~~~
 
[when 심화]  
범위로 처리하기 `in`이라는 키워드 있어야 사용 가능  
`in min .. max ` -> **min 부터 max까지**
~~~Kotlin
fun main(){
    var jumsu : Int = (count/10) * 10
    when(jumsu){
        in 90 .. 100 -> println("장학생")
        in 60 .. 89 -> println("합격")
        else -> println("fail")
    }
}
~~~

### Kotlin 배열
----

1. 일차원 배열 선언 형식
  
~~~Kotlin
fun main(){
    var array = Array<데이터 타입>(개수, {초기값})
    var array = Array<데이터 타입>(개수) {초기값}
    // 단 타입이 명시되어있으면 초기값은 의무 아님
    // 변수 선언이랑 비슷한 맥락
}
~~~

[실사용 예시]
~~~Kotlin
fun main(){
    var one = Array<Int>(4, {0}) // 크기 4짜리 1차원 배열 생성 초기값은 0
    one[0] = 10 // 0번 index에 data 10 넣기
    one[3] = 20 // 3번 index에 data 20 넣기
}
~~~

2. 이차원 배열 선언 형식  

~~~Kotlin
fun main(){
    var array = Array<배열 데이터 형식>(행 개수, {배열 데이터 형식(열 개수)})
}
~~~

[실사용 예시]  
~~~Kotlin
fun main(){
    var two = Array<IntArray>(3 {IntArray(4)}) 
    var two = Array<IntArray>(3) {IntArray(4)} // 3행 4열 배열 생성
    // IntArray => 정수형 배열 키워드
    // 약간 파이썬 같은 느낌인데..? 리스트안에 리스트 중첩 
}
~~~

[주의사항]  
**행의 데이터 타입 == 열의 데이터 타입**  
**무조건 IntArray 같은 타입사용해야함**

3. 배열 선언하면서 바로 값을 넣기(초기화 값이 아님)
~~~Kotlin
fun main(){
    var three : IntArray = intArrayOf(1,2,3) // intArrayOf 이용 (넣은 값 만큼 크기 할당)
}
~~~

4. `ArrayList` : 연결리스트 같은 느낌이다.
~~~Kotlin
fun main(){
    var one = ArrayList<Int>(4)
    one.add(10)
    one.add(20)
    var hap = one.get(0) + one.get(1)
    // 첫 번째 값 + 두 번째 값
}
~~~

### 반복문 : for, while

여기서 `for`문이 조금 다르다
~~~Kotlin
fun main(){
    var three : IntArray = intArrayOf(1,2,3)
    for (i in three.indices){
        println(one[i])
    }
    //indices -> 파이썬 range()같은 느낌
}
~~~

~~~Kotlin
fun main(){
    for(변수 in 시작..끝 step 증가량){ // 약간 python range() 풀어서 쓴 느낌
        // for(i in 0..99 step 1) 이때 0 <= i  >= 99 임
        // 실행문
    }

    for(변수 in 배열 명.indices){
        // 배열의 개수만큼 변수에 대입해서 사용하는 방법임
        // 실행문
    }
    for(변수 in 배열 명){
        // 실행문
    }

    // 실사용
    var three : IntArray = intArrayOf(1,2,3)
    for(t in three){ // 파이썬 처럼 쓰면됨
        println(t)
    }
}
~~~

**`while`은 그냥 동일함.**


### 메소드와 전역변수, 지역변수
---
1. 메소드 : 기본 메서드인 `main()`함수 외에 사용자가 메소드를 추가로 생성할 수 있음
2. 전역, 지역변수 : 알잖아...
3. 함수에 리턴타입 지정 가능
~~~Kotlin
fun add(x:Int, y:Int) : Int {
    // add()의 리턴 타입은 Int임.
    // 반드시 return 할 경우 타입 명시해야함.
}
~~~
\* **리턴 타입 명시 하지않을 경우 해당 메서드는 Void타입이다.**
\* **main() 안에 메서드 정의 가능**

### 예외처리
---
`try-catch` 문을 통해서 가능.
~~~Kotlin
fun main(){
    var num1 : Int = 100
    var num2 : Int = 0
    try{
        println(num1/num2)
    }catch(e : ArithmerticException){
        println("계산에 문제가 있습니다.")
    }
}
~~~

### 클래스 정의와 인스턴스 생성
----
클래스 : 필드변수와 메소드로 구성
~~~Kotlin
Class Car{
    var color : String = ""
    var speed : Int = 0

    fun upSpeed(value : Int){
        if((speed + value) >= 200)
            speed = 200
        else
            speed = speed + value
    }

    fun downSpeed(value : Int){
        if(speed-value <= 0 )
            speed = 0
        else
            speed = speed - value
    }
}

fun main(){
    var myCar1 : Car = Car() // 이때 컴파일러가 알아서 기본 생성자 만들어 둔다.
}
~~~

[사용자 생성자 만들기]  
`constructor`키워드 사용
~~~Kotlin
constructor(color:String, speed:Int){
    this.speed = speed
    this.color = color
}
~~~

### 메소드 오버로딩(overloading) And 메소드 오버라이드(override)
---
**Method overloading** : 리턴타입에는 영향없고 매개변수만 상관있음
> 한 클래스 내에서 메소드의 이름이 같아도 **파라미터의 개수나 데이터 형식만 다르면 여러 개를 선언할 수 있음**

**Method override** : 이름, 매개변수 같은데 실행문만 다름.

### 정적 필드, 정적 메소드, 상수 필드
----
1. 정적필드(Static field) : 인스턴스 생성 없이 클래스 자체적으로 사용됨.
    **`companion object{}` 안에 작성하여 정적 필드 만듦**

2. 정적메소드(Static method) : `companion object{}` 안에 작성 하면 됨

3. 상수 필드 : `Static field`에 초기값 입력 후 `const val`로 선언 (val도 상수 변수 의미 단, **정적 필드의 상수화는 const키워드 필요**)

~~~Kotlin
Class Car{
    var color : String = ""
    var speed : Int = 0

    companion object{ // 정적 필드, 정적 메서드 
        var carCount : Int = 0
        fun upSpeed(value : Int){
            if((speed + value) >= 200)
                speed = 200
            else
                speed = speed + value
        }

        fun downSpeed(value : Int){
            if(speed-value <= 0 )
                speed = 0
            else
                speed = speed - value
        }
    }
}

fun main(){
    var myCar1 : Car = Car() // 이때 컴파일러가 알아서 기본 생성자 만들어 둔다.
}
~~~

### 클래스 상속(inheritance)
----
클래스 상속 : 기존 클래스를 그대로 물려받으면서 필요한 메서드를 추가로 정의하는 것.

- 슈퍼클래스 : 부모 클래스라고 부름
- 서브클래스 : 슈퍼클래스의 모든 필드, 메서드를 상속받음

`open`이라는 키워드가 있어야 **오버라이딩 가능**
오버라이딩 할땐, `override`라고 명시해야함 (Java의 어노테이션과 유사)

**서브 클래스 선언시에 타입 지정 필요함**

~~~Kotlin
open class Car{
    // 슈퍼클래스 누군가 상속 받을 예정이라 open 키워드 사용
    var color : String = ""
    var speed : Int = 0

    open fun upSpeed(value : Int){
        if((speed + value) >= 200)
            speed = 200
        else
            speed = speed + value
    }

    open fun downSpeed(value : Int){
        if(speed-value <= 0 )
            speed = 0
        else
            speed = speed - value
    }
}
class Automobile : Car() {
    //Car() 이렇게 하면 부모 생성자 까지 호출하면서 가져오는 것.
}
class Automoblie : Car {
    constructor() {
        // 요렇게 하면 Car() 안해도 됨.
    }
}
~~~

### 추상 클래스와 추상 메서드
---
- 추상(abstract) 클래스
    - 인스턴스화를 금지하는 클래스 -> `var animal : Animal()` 이런거 못함 `var animal : Animal` 이래야함
    - Class 앞에 abstract 키워드 붙여서 사용(Java랑 동일)

- 추상 메소드(abstract method)
    - **본체가 없는 메소드**
    - abstract 키워드 붙여서 사용  
    **추상 메서드를 포함하는 클래스는 추상 클래스 밖에없음.** 

추상 클래스와 추상 메서드를 사용하는 목적 : 공통적으로 사용되는 기능을 추상 메드로 선언하고 상속 후 구체화함.

**즉, 구현한다(implement)** 는 의미..?


### 인터페이스(interface)와 다중 상속
----
인터페이스(interface) : 추상 클래스와 성격이 비슷.   
- > 인터페이스는 상속 보단 구현한다는 표현을 함.

~~~Kotlin
abstract class Animal { // 추상 클래스
    var name : String = ""
    abstract fun move() // 추상 메서드
}

interface iAnimal { // 인터페이스
    abstract fun eat() // 추상 메서드
}

class iCat : iAnimal { // iAnimal 구현
    override fun eat() { // 오버라이드
        println("생선을 좋아한다.")
    }
}

class iTiger : Animal(), iAnimal { // 다중 상속 흉내 (Animal은 상속, iAnimal은 구현)
    override fun move() {
        println("네 발로 이동한다.")
    }
    override fun eat() {
        println("멧돼지를 잡아 먹는다.")
    }
}

class Eagle : Animal() {
    var home : String = ""
    override fun move() {
        println("날개로 날아간다.")
    }
}

fun main() {
    var cat = iCat() // 인터페이스는 인스턴스화 가능
    cat.eat()
    
    var tiger = iTiger()
    tiger.move()
    tiger.eat()    
}
~~~

### 람다식(Lambda expression)
----
익명함수 형태로 간단히 표현 한 것

[파라미터 2개를 받아서 합계를 출력하는 일반적인 메소드 형식]
~~~Kotlin
fun addNumber(n1:Int, n2:Int) : Int{
    return n1 * n2
}
~~~

[람다식 표현]
~~~Kotlin
val addNumber = {n1:Int, n2:Int -> n1 + n2} // var을 사용해서 선언도 가능하지만 추천 x
                   // 매개변수 -> 실행문
~~~

**람다식 특징**
1. 람다식은 {}로 감싸며 fun 예약어 사용안함
2. {}안쪽 -> 왼쪽은 매개변수, 오른쪽은 함수의 실행문
3. -> 오른쪽 문잔이 여러 Line이면 세미콜론으로 구분 (**한줄로 작성하는 경우 적용됨**)
4. 내용 중 마지막 문장은 반환 값(return)

**추후 Event Listener 사용시 많이 적용됨**