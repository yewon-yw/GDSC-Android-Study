# CallBack 함수 참고 
[callback 함수]
--
1. **다른 함수의 인자로써 이용되는 함수(고차함수)**
2. 어떤 이벤트에 의해 호출되어지는 함수.(이벤트 리스너)

OS -> 이벤트 인식 -> 콜백 호출
> `setOnCableConnected`로 설정한 함수가 케이블을 연결할 때 마다 호출되므로 -> `onCableConnected`는 어떤 이벤트에 의해 호출되어지는 함수 즉, 콜백 함수 라고 할 수 있다.

## 안드로이드에서 콜백 의미

1. 정의 : 함수의 파라미터로 들어온 함수를 콜백함수라고 함. 이는 특별한 문법이 있는게 아니고 **호출하는 방식의 측면으로 봐야함**
2. 용도 : **어떤 함수가 호출되고 순차적으로 다음 작업을 실행해야 할 때 사용됨.**
~~~Kotlin
fun main(){
    first(::Second) // call by name
}
fun first(second : () -> Unit) : Unit{ // 콜백 함수 리턴 타입 = Unit, first함수 리턴 타입 = Unit
    print("first on\n")
    second() // 콜백 함수 실행.
}
fun second():Unit{ //반환 타입 void
    print("second on")
}
// 실행 순서 main -> first -> second
// 리턴 순서 second -> first -> main
~~~