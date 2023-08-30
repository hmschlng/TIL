# 2023. 08. 30

|분류|✏️ 할 일|💭 설명|✅ 완료 |
|-|-|-|-|
| Algo | BOJ - 안전 영역 | `Silver 1` / `BFS` |<ul><li>- [x] </li></ul>|
| SQL | Programmers - 조건별로 분류하여 주문상태 출력하기 | `Lv3` / `JOIN` / `GROUP BY` | <ul><li>- [x] </li></ul> |
| SQL | Programmers - 조건에 맞는 사용자와 총 거래금액 조회하기 | `Lv3` / `JOIN` / `GROUP BY` | <ul><li>- [x] </li></ul> |
| CS | Wrapper class | 개념 정리 | <ul><li>- [x] </li></ul> |

## 인증 📸

### BOJ Silver1. 안전 영역
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/9qdZd2W.jpg">
  <p>

  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 조건별로 분류하여 주문상태 출력하기
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/oD4OowM.jpg">
  <p>

  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 조건에 맞는 사용자와 총 거래금액 조회하기
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/DqP4Fb0.jpg">
  <p>

  </p>
</details>
<br/>

### Loose coupling
<details open>
  <summary> 내용 보기 </summary>
  <blockquote>
  <p>

`[Java의 int와 Integer의 차이]`

`기본적인 차이`

`int`
- primitive type
- 기본값이 0이다.
- null을 허용하지 않는다.
- JVM stack area에 저장된다.
- 함수에 인자로 전달 시 call by value로 동작한다.

`Integer`
- reference type
- 기본값이 null이다.
- null을 허용한다.
- JVM heap area에 저장된다.
- 함수에 인자로 전달 시 call by reference 처럼 주소값을 참조한다. 하지만 Wrapper class의 내부 값은 호출되는 쪽에 영향을 주는 수정은 불가능하다. 따라서 call by value 처럼 동작한다.


`Wrapper class에 대한 추가적인 정보`

`[Auto Boxing]`
- JDK 1.5 이후부터 Integer같은 Wrapper class와 int 같은 primitive type는 연산 시에 자동 변환을 지원한다.
- primitive -> Wrapped class 로의 자동 변환을 Auto Boxing, Wrapped class -> primitive 로의 자동 변환을 Auto Unboxing이라고 한다.
- 이 오토 박싱/언박싱 연산은 내부 작업이 필요로 하기 때문에, 같은 타입끼리의 연산(int <-> int, Integer <-> Integer)보다 수행 시간이 느리다(1000000 연산 기준 약 5배 차이).


`[Wrapper class의 캐싱]`

Integer는 내부에 IntegerCache라는 private class를 가지고 있다. 
IntegerCache는 오토박싱을 서포팅하는 캐시를 가지고 있다(static final Integer cache[]).

이 캐시에 클래스 로드 시에 특정 범위의 값을 가지는 여러 인스턴스를 미리 생성해놓고, Auto Boxing 연산 시에 이 범위 안의 값을 가진 Integer 인스턴스끼리는 주소를 공유한다.

cache의 범위는 low와 high라는 필드의 값으로 결정되는데, low는 -127, high는 127이다.
  -> 이때 high는 jvm 튜닝에 따라서는 더 커질 수 있다.(-XX:AutoBoxCacheMax=<size>)

Integer.valueOf() 를 통한 인스턴스화에서도 IntegerCache가 사용된다.

``` java
@Test
public void test1() throws Exception {
    Integer n1 = 1;
    Integer n2 = 1;
  ​
    assertTrue(n1 == n2);
}
  ​
@Test
public void test2() throws Exception {
    Integer n1 = 300;
    Integer n2 = 300;
  ​
    assertTrue(n1 == n2);
}

@Test
public void Test3() throws Exception {
    Integer n1 = Integer.valueOf(1);
    Integer n2 = Integer.valueOf(1);
  ​
    assertTrue(n1 == n2);
}
  ​
@Test
public void test4() throws Exception {
    Integer n1 = Integer.valueOf(300);
    Integer n2 = Integer.valueOf(300);
  ​
    assertTrue(n1 == n2);
}
```

따라서 위의 4개의 테스트 메서드 중 test2, test4는 실패한다. test1, test2에서는 오토 박싱 연산이 있어 IntegerCache가 사용되고, test3, test4에서는 valueOf()를 통한 IntegerCache의 사용이 있다. 

즉, 캐싱 범위에 속하는 1에 대해서는 미리 생성된 같은 인스턴스를 가지게 되는 것이고, 캐싱 범위 밖인 300에 대해서는 각각 새로운 인스턴스를 받게 되어 == 연산이 false 가 된다.

``` java
@Test
public void test5() throws Exception {
    Integer n1 = new Integer(1);
    Integer n2 = new Integer(1);
  ​  ​
    assertTrue(n1 == n2);
}
```

생성자에 의한 인스턴스화는 IntegerCache가 사용되지 않는다. 따라서 test5는 실패한다.

ByteCache, LongCache 등등도 마찬가지 기능이다.
CharacterCache는 근본은 정수 타입이지만 문자 표현을 위해 음수값을 캐싱하지 않는다.

<br/>
</p>
  </blockquote>
</details>