# Chapter 03
### kotlin 특징
1. Java와 100% 상호 호환되므로 Java 코드를 완전히 대체 가능
2. Java보다 문법이 간결
3. 프로그램의 안정성을 높여줌
4. var, val 예약어를 통해 데이터 형식을 선언하지 않고 변수 선언 가능

<br>

### Kotlin 변수 선언 방식
1. 암시적 선언
   - 변수의 데이터 형식을 지정하지 않고, 대입되는 값에 따라 자동으로 변수의 데이터 형식이 지정됨
   - 단, 초기화하지 않은 경우엔 데이터 형식 반드시 명시해야함
2. var(variable)
    - 일반 변수 선언할 때 사용
    - 필요할 때마다 계속 다른 값 대입 가능
3. val(value)
   - 변수 선언과 동시에 값을 대입하거나 초기화 없이 선언한 후에 한 번만 값을 대입 가능
   - 한 번 값을 대입하고 나면 값 변경 불가

  <br>

  ### 데이터 형식 변환
  - 캐스팅 연산자 사용
    - toInt(), toDouble(), ...
  
  <br>

  ### null 사용
  - Kotlin은 기본적으로 변수에 null 값 불가능
  - null로 초기화 방법
    ```kotlin
    var a: Int? = null
    ```
   - null값이 들어가면 안되는 경우
     ```kotlin
     var arr = ArrayList<Int>(1)
     arr!!.add(100)
     ```
<br>

### 조건문
1. if 문
2. when 문(다중 분기)
   ```kotlin
   when(score){
    10 -> Log.d(TAG,"A+")
    9 -> Log.d(TAG,"A")
    7,8 -> Log.d(TAG,"B+")
    6..3 -> Log.d(TAG,"B")
    else -> Log.d(TAG,"C")
   }
   ```

<br>

### 배열
1. 1차원 배열
   ```kotlin
   var arr = Array<Int>(4,{0}) // length:4
   arr[0] = 10
   arr[3] = 20
   ```
2. 2차원 배열
   ```kotlin
   var arr = Array<IntArray>(3,{IntArray(4)}) // size:3*4
   arr[0][1] = 100
   arr[2][3] = 200
   ```

- ArrayList
  ```kotlin
  var arr = ArrayList<String>(4)
  arr.add("first")
  arr.add("second")
  println(arr.get(1)) // second 출력
  ```
<br>

### 반복문
1. for 문
   ```kotlin
   for(index in 0..5 step 1){
    println(index)
   }
   // 0 <= index <= 5 범위
   ```
   ```kotlin
   for(index in arr.indices){
    println(arr[index])
   }
   // 배열 크기만큼 실행
   // 아래 코드와 동일하게 실행
   for(item in arr){
    println(item)
   }
   ```
2. while 문

<br>

### 메소드, 전역변수, 지역변수
- 메소드
- 변수
  - 전역변수(global variable)
  - 지역변수(local variable)
  
<br>

### 예외 처리
- try-catch 문
  ```kotlin
  fun main(){
    var num1: Int = 100
    var num2: Int = 0
    try{
        println(num1/num2)
    } catch (e: ArithmeticException){
        println("계산에 문제가 있습니다")
    }
  }
  ```

<br>

### 클래스
- class
  - 변수(필드)와 메소드로 구성
  - 생성자는 `constructor` 사용
  - 메소드 오버로딩(overloading)
    - 한 클래스 내에서 메소드의 이름이 같아도 파라미터의 개수나 데이터 형식만 다르면 여러개를 선언할 수 있음
  - cf) 오버라이딩(overriding): 파라미터 개수는 동일, 내부 구현이 달라짐, 보통 상속관계에서 주로 발생

<br>

### 필드, 메소드
- 정적 필드(static field)
  - 인스턴스를 생성하지 않고 클래스 자체에서 사용
  - `companion object {}` 안에 작성
- 정적 메소드(static method)
  - `companion object {}` 안에 작성
  - 인스턴스 생성 없이 `클래스명.메소드명()`으로 호출해 사용 가능
- 상수 필드
  - 클래스 안에 상수를 정의할 때 사용
  - 정적 필드에 초깃값을 입력, `const val`로 선언
  - 선언 후에는 값 변경 불가
```kotlin
  class Car{
    var color: String = ""
    var speed: Int = 0
    companion object {
        var carCount: Int = 0 // 정적 필드
        const val MAXSPEED: Int = 200 // 상수 필드
        const val MINSPEED: Int = 0 // 상수 필드
        fun currentCarCount(): Int { // 정적 메소드
            return carCount
        }
    }

    // 생성자
    constructor(color: String, speed: Int){
        this.color = color
        this.speed = speed
        carCount++
    }
  }
  ```

<br>

### 클래스 상속(inheritance)
- 기존의 클래스가 가지고 있는 것을 그대로 물려받으면서 필요한 필드나 메소드를 추가로 정의
- superclass(부모클래스)
- subclass(자식클래스)
  - 별도의 선언이나 정의 없이도 부모클래스의 필드와 메소드 사용 가능
- 메소드 오버라이딩(overriding)
  - 부모클래스의 메소드를 무시하고 새로 정의
  - `override` 키워드 사용
  - Kotlin에서는 default keyword가 final이라 오버라이드가 불가능하기 때문에 `open` 키워드 사용
  ```kotlin
  open class Car{
    open fun upSpeed(value: Int){}
  }
  class Automobile: Car {
    override fun upSpeed(value: Int){
        // 새로 정의
    }
  }
  ```
<br>

### 추상클래스와 추상메소드
- 추상클래스(abstract class)
  - 인스턴스화를 금지하는 클래스
  - `abstract` 키워드 사용
- 추상메소드(abstract method)
  - 본체가 없는 메소드
  - `abstract` 키워드 사용
  - 추상메소드를 포함하는 클래스는 추상클래스로 지정해야함
- 사용 목적
  - 공통적으로 사용되는 기능을 추상메소드로 선언해놓고, 추상클래스를 상속받은 후에 추상메소드를 오버라이딩해서 사용하기 위함
  - 구현한다(implement)
    - 추상메소드를 오버라이딩 하는 것
```kotlin
abstract class Animal {
    var name: String = ""
    abstract fun move()
}
class Tiger: Animal() {
    var age: Int = 0
    override fun move() {
        println("네 발로 이동")
    }
}
class Eagle: Animal() {
    var home: String = ""
    override fun move() {
        println("날아간다")
    }
}
fun main() {
    var tiger = Tiger()
    var eagle = Eagle()
    tiger.move()
    eagle.move()
}
/**
 * 출력:
 * 네 발로 이동
 * 날아간다
 */
 ```
<br>

### 다형성(polymorphism)
- subclass(자식클래스)에서 생성한 인스턴스를 자신(부모)의 클래스 변수에 대입할 수 있는 것을 의미
- 하나의 변수에 여러 종류의 인스턴스를 대입 가능
```kotlin
fun main() {
    var animal: Animal
    animal = Tiger()
    animal.move()
    animal = Eagle()
    animal.move()
}
/**
 * 출력:
 * 네 발로 이동
 * 날아간다
 */
 ````
<br>

### 인터페이스와 다중 상속
- 추상클래스와 성격 비슷
- `interface` 키워드 사용하고 내부에는 추상메소드 선언
- 구현한다(implement)
- Kotlin은 다중 상속을 지원하지 않기 때문에 interface를 사용해서 다중 상속 구현 가능
```kotlin
abstract class Animal {
    var name: String = ""
    abstract fun move()
}
interface iAnimal {
    abstract fun eat() // 추상메소드라 본체가 없음
}
class iCat: iAnimal {
    override fun eat() {
        println("like fish")
    }
}
class iTiger: Animal(), iAnimal { // Animal은 상속받고, iAnimal을 구현한다는 의미
    override fun move() {
        println("네 발로 이동")
    }
    override fun eat() {
        println("like meat")
    }
}
```
<br>

### 람다식(lambda expression = lambda function)
- 함수를 익명함수(anonymous function)형태로 간단히 표현
- 코드 간결해져서 가독성이 좋아짐
- 람다는 { } 안에 매개변수와 메소드의 모든 내용을 선언
```kotlin
fun add(num1: Int, num2: Int): Int {
    return num1 + num2
}

// 위 메소드를 람다식으로 표현
val add = { num1: Int, num2: Int -> num1 + num2 }
// 위의 람다식과 아래의 람다식은 동일함
val add: (Int, Int) -> Int = { num1, num2 -> num1 + num2 }
```

- 람다식 특징
  - fun 예약어를 사용하지 않고, { } 사용
  - 파라미터 -> 함수 body
  - 함수 body가 여러줄이라면 세미콜론(;)으로 구분
  - 내용 중 마지막 문장은 return 값, `return`문 사용 불가
  - return type이 없는 경우 Unit으로 표기
    ```kotlin
    val greet: () -> Unit = { println("hello") }
    ```
  - 매개변수가 1개인 람다식
    ```kotlin
    val some: (Int) -> Unit = { println(it) }
    // 매개변수를 따로 선언하지 않아도 it 키워드로 사용 가능
    ```
- 고차함수
  - 함수를 매개변수로 전달받거나 반환하는 함수를 의미
  - 일반적으로는 람다식을 매개변수로 받거나 결과로 리턴하는 함수를 의미
  - 코드 조각을 람다로 만들어 코드 중복을 제거하기 위함
  ```kotlin
  fun calculator(a: Int, b: Int, operation: (Int, Int)->Int) = operation(a, b)

  fun main(args: Array<String>?){
    val sum = {x: Int, y: Int -> x+y}
    println(calculator(1,2,sum))
    println(calculator(4,3,{a: Int, b: Int -> a-b}))
  }
  /* 원래는 sum 함수가 들어가는 calculator, dif 함수가 들어가는 calculator 두 개를 작성해야하지만 람다식을 사용해 코드 중복을 줄임 */
  ```
<br>

### 패키지
- 클래스와 인터페이스가 많아지면 관리하기가 어렵기 때문에 패키지 단위로 묶어서 관리
- `package 패키지명`

<br>

### Generics
- 데이터 형식의 안정성을 보장하는 데 사용
- `<>` 내에 타입을 지정
  ```kotlin
  var strList = ArrayList<String>(4)
  strList.add("first")
  strList.add(3) // 오류 발생
  ```
- 사용자가 정의한 클래스형에도 사용 가능
