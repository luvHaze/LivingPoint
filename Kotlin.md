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
