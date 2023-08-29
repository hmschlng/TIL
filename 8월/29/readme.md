# 2023. 08. 29

|분류|✏️ 할 일|💭 설명|✅ 완료 |
|-|-|-|-|
| Algo | Programmers - 단속 카메라 | `Lv3` / `Greedy` |<ul><li>- [x] </li></ul>|
| Algo | Programmers - 숫자 게임 | `Lv3` / `Greedy` |<ul><li>- [x] </li></ul>|
| SQL | Programmers - 카테고리 별 도서 판매량 집계하기 | `Lv3` / `JOIN` / `GROUP BY` | <ul><li>- [x] </li></ul> |
| CS | Loose coupling | 개념 정리 | <ul><li>- [x] </li></ul> |

## 인증 📸

### Programmers Lv3. 단속 카메라
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/MBoFr5t.jpg">
  <p>

  </p>
</details>
<br/>

### Programmers Lv3. 숫자 게임
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/dCteC1r.jpg">
  <p>

  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 카테고리 별 도서 판매량 집계하기
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/7jT2h1w.jpg">
  <p>

  </p>
</details>
<br/>

### Loose coupling
<details open>
  <summary> 내용 보기 </summary>
  <blockquote>
  <p>

`Loose Coupling`

애플리케이션에서의 Loose coupling은, 애플리케이션 컴포넌트끼리의 상호 연결이 실행 가능한 최소 수준으로 서로 의존하도록 하는 design principle이다. 결합은 각 컴포넌트가 다른 컴포넌트에 대해 갖고 있는 직접적인 관여 정도를 나타낸다.

`Loose Coupling 적용의 이점`

- 컴포넌트의 변경이 다른 부분에서 예상하지 못한 않은 "변경"이 발생할 리스크를 줄여 시스템의 안정성을 높인다.
 -> 변경 : 모듈 추가/제거, 리팩토링, 재설계 등

- 높은 유연성과 재사용성으로 유지 관리 차원의 이득이 있다.


`Spring Framework의 DI와 Loose coupling`

Spring은 DI(의존성 주입)을 통해 loose coupling을 구현한다. 

Bean 객체로 지정된 POJO/POJI들을 애플리케이션 실행 시점에 ApplicationContext에 미리 생성하고, 런타임 내에 Bean들 사이의 의존성이 결정되게 함으로써 객체와 객체 간의 결합도를 낮춘다.

이는 한 컴포넌트가 다른 컴포넌트에 대해 필요한 지식의 양을 낮추어준다. 

런타임시 객체 내부에서 다른 객체를 직접 생성할 때(new), 다른 객체에 대한 지식(생성하는 데 필요한 여러 정보들 - 구현체인지, 상속 관계는 어떠한지, 인스턴스화 되었는지, 추상 클래스인지 구체화된 클래스인지 등등)이 생성의 주체가 되는 클래스에게 요구된다. 

하지만 @Autowired 등으로 의존관계가 정의한다면, singleton으로 미리 생성되어 있다가 Bean이 사용될 때 의존 관계가 정해지고, 해당 Bean을 그대로 사용한다. 이 관점에서도 loose coupling이라 할 수 있다.

<br/>
</p>
  </blockquote>
</details>