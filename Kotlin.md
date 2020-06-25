# 2020. 06. 10

### 1. sort()

주어진 콜렉션을 오름차순으로 정렬해준다. 기존 배열을 변경하는 메소드이기 때문에 **Mutable 콜렉션에만 적용 가능.**

```
val sortedValues = mutableListOf(1,2,7,6,5,6)
sortedValues.sort()
println(sortedValues)
```

내림차순 정렬을 하려면 **sortDescending()** 을 하거나 **reverse()** 메소드를 사용
기존 배열을 유지하고 싶다면 **sorted()** 사용

### 2. sortBy()

주어진 객체의 특정 속성을 기준으로 정렬한다. sort() 와 마찬가지 이유로 Mutable 콜렉션에만 적용 가능

```
val sortedValues = mutableListOf(1 to "a", 2 to "b", 7 to "c", 6 to "d", 5 to "c", 6 to "e")
sortedValues.sortBy { it.second }
println(sortedValues)
```

내림차순을 위해서는 **sortByDescending** 이나 **reverse** 메소드 사용
기존 배열을 유지하고 싶다면 **sortedBy()** 사용

### 3. sortWith()

고급 정렬을 위해서 인수로 Comparator를 전달할 수 있다.

```
val sortedValues = mutableListOf(1 to "a", 2 to "b", 7 to "c", 6 to "d", 5 to "c", 6 to "e")
sortedValues.sortWith(compareBy({it.second}, {it.first}))
println(sortedValues)
```

기존 배열 유지 : **sortedWith**


# 2020.06.12

### 1.  equals , ' == '

- JAVA

  - equals는 Call by Value 즉, 값을 참조해서 비교

  - '' == ' 은 Call by Reference 주소를 참조 

    > 문자열의 값을 비교 시 equals 를 하는것이 맞다
    >
    > 

- Kotlin

  - 코틀린은 == 사용시 equals 를 내부적으로 호출한다.  굿

  - 코틀린에서 주소값을 참조할 때는 ===를 사용하면 된다.
  
  



# 2020.06.24

## - String 

- split - *문자열을 delimiters 를 기준, List형태로 나눠주고 반환한다.*

```kotlin
fun [CharSequence]().split(
  vararg **delimiters**: String,
  **ignoreCase**: Boolean = false,
  **limit**: Int = 0
): [List]
```



- replace - *문자열 내에 oldValue를 newValue로 바꾼 String을 반환한다.*

```kotlin
fun [CharSequence]().replace(
  oldValue: Char, newValue: Char
): String
```



- contains - *문자열에서 other을 포함하고 있는지를 리턴해준다.*

```kotlin
operator fun CharSequence.contains(
    other: CharSequence,
    ignoreCase: Boolean = false
): Boolean
```



- reserved - *문자열을 거꾸로한 문자열을 반환한다.*

```kotlin
fun CharSequence.reversed(): CharSequence
```



- substring - *문자열에서  range에 해당하는 문자 반환 (배열처럼 0부터)* 

```kotlin
fun String.substring(range: IntRange): String
```



- last - *문자열에서 가장 마지막 문자를 반환한다.*

```kotlin
fun CharSequence.last(): Char
```

# 2020. 06. 25

## - 코틀린 Type 표현방식

- `Int` : `123`으로 표현
- `Long` : `123L`으로 표현
- `Double` : `123.5`로 표현
- `Float` : `123.0F` 또는 `123.0f`으로 표현



##  - Math

- sqrt - *x 의 가장 가깝거나 해당하는 제곱근을 구해준다.* 

```kotlin
fun sqrt(x: Double): Double
fun sqrt(x: Float): Float
```

`몰라서 개고생 했다.`



- abs - x의 절대값을 반환해준다.

```kotlin
fun abs(x: Double): Double
fun abs(x: Float): Float
```






