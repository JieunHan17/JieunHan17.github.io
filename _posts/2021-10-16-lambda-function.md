---
title: Lambda Funtion vs High Order Function
layout: post
post-image: "https://developer.android.com/images/cluster-illustrations/kotlin-hero.svg?hl=ko"
description: Kotlin에서 지원하는 함수형 프로그래밍
tags:
  - Kotlin
  - Function
---

# High Order Function(고차함수)

- 함수를 인수로 취하거나 함수를 결과로 반환할 수 있는 함수
- e.g. Call-Back Method -> Android Studio에서 자주 사용

---

# Lambda Expression(람다 표현식)

- 고차함수에서 매개변수로 주어지는 식
- Java 7까지는 람다 표현식을 지원하지 않았지만, Java 8부터는 지원

## 예시

<font style="color: #1E3D6B">[Java 코드]</font>

```java
FloatingActionButton fab = findViewById(R.id.fab);
fab.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // Something
    }
});
```

<br>

<font style="color: #1E3D6B">[Kotlin 람다 표현식]</font>

```kotlin
fab.setOnClickListener { /* Something */ }
```

- Kotlin에서 제공하는 SAM(Single Abstract Method) 정의에 의해 동작
- SAM은 Interface에 1개의 Method가 있을 경우에만 동작

## 문법

<font style="color: #1E3D6B">[최댓값 구하는 코드]</font>

```kotlin
private fun findMax(list: ArrayList<Int>) =
        list.maxBy({it})
```

<br>

그러나 Kotlin에서는 메소드에 정의한 Higher-Order Function의 마지막 {}은 () 밖에다가 값을 정의할 수 있다.<br>
()를 생략하면 아래와 같이 된다.<br>

```kotlin
private fun findMax(list: ArrayList<Int>) =
        list.maxBy { it }
```

- 변수가 1개만 존재하는 경우 it 키워드로 대체 가능

<br>

<font style="color: #1E3D6B">[합을 구하는 코드]</font>

```kotlin
fun sum(a: Int, b: Int): Int {
  return a + b
}
```

<br>

람다식 표현을 통해 아래와 같이 간단하게 표현이 가능하다.<br>

```kotlin
val sum = { a: Int, b: Int -> a + b}
```

<br>

---
