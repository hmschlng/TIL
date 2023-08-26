# 2023. 08. 26

|분류|✏️ 할 일|💭 설명|✅ 완료 |
|-|-|-|-|
| Algo | Programmers - 야근 지수 | `Lv3` / `Heap` |<ul><li>- [x] </li></ul>|
| Algo | Programmers - 단어 변환 | `Lv3` / `BFS` |<ul><li>- [x] </li></ul>|
| SQL | Programmers - 없어진 기록 찾기 | `Lv3` / `JOIN` | <ul><li>- [x] </li></ul> |
| SQL | Programmers - 조건에 맞는 사용자 정보 찾기 | `Lv3` / `HAVING` / 'CONCAT' | <ul><li>- [x] </li></ul> |
| CS | SSIA ch5 나머지 공부 | 책 읽고 정리 | <ul><li>- [x] </li></ul> |

## 인증 📸

### Programmers Lv3. 야근 지수
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/1enL41O.jpg">
  <p>

  </p>
</details>
<br/>

### Programmers Lv3. 단어 변환
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/5dayQMl.jpg">
  <p>

  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 없어진 기록 찾기
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/br9sTfr.jpg">
  <p>

  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 조건에 맞는 사용자 정보 조회하기
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/agpjcSa.jpg">
  <p>

  </p>
</details>
<br/>

### Spring Security In Action ch5 공부
<details open>
  <summary> 내용 보기 </summary>
  <blockquote>
  <p>

`SecurityContext`

SecurityContext는 Authentication 객체를 담는 인스턴스이다.
AuthenticationProvider가 위임받은 인증처리를 성공적으로 완료하면(authenticate()) Authentication 객체를 반환하고, AuthenticationManager는 요청이 유지되는 동안 이 Authentication 객체를 SecurityContext에 저장하고 있는다(실제로는 인증 필터로 반환한 뒤 인증 필터가 SecurityContext에 저장하는 흐름).
인증 프로세스가 끝난 후 SecurityContext에서 인증된 엔티티에 대한 세부정보(username, authority 등)에 접근할 수 있다.


`SecurityContextHolder`

SecurityContextHolder는 SecurityContext를 관리하는 관리자 객체이다. SecurityContext 자체로는 Authentication 객체를 저장하는 역할만 한다.

(Principal -> Authentication -> SecurityContext -> SecurityContextHolder의 순서로 저장된다)

Spring Security는 SecurityContextHolder가 SecurityContext를 관리하는 세가지 방식(전략)을 제공한다.
- MODE_GLOBAL
- MODE_THREADLOCAL
- MODE_INHERITABLETHREADLOCAL


`MODE_GLOBAL`

독립형 애플리케이션에 적합한 전략이다. 일반적인 WAS는 요청을 독립적으로 관리하므로 요청별로 분리하는 것이 더 합리적이기 때문에 사용되지 않는다.
모든 요청, 모든 스레드에서 SecurityContext를 공유한다. 그러나 모든 스레드의 동시 접근에 의한 race condition이 발생할 수 있다.

※ SecurityContext는 ThreadSafe를 지원하지 않으므로, 개발자가 동시 접근을 직접 해결해 주어야 한다.


`MODE_THREADLOCAL - Default`

전통적인 servlet WAS에 적용되는 기본 전략이며, 따로 명시적으로 지정하지 않아도 적용된다. 
Tomcat은 들어오는 요청 각각에 대해 스레드를 할당하면, THREADLOCAL은 해당 스레드 내부에 보안 컨텍스트를 저장한다.
때문에 한 요청은 그 요청에 대한 보안 컨텍스트만 접근 가능하고, 다른 thread에서는 보안컨텍스트를 조회할 수 없다.


`MODE_INHERITABLETHREADLOCAL`

요청 당 여러 스레드를 사용하는 리액티브 애플리케이션에 적합한 관리 전략이다. 
Asnyc가 적용된(@EnableAsync) 리액티브 애플리케이션에서는 @Async 메소드가 별도의 스레드에서 실행되는데, THREADLOCAL 전략을 사용하는 상태에서는 상위 스레드의 세부 정보가 복사되지 않는다.

INHERITABLETHREADLOCAL 전략은 비동기 메서드를 실행하는 스레드가 원래 스레드의 보안 컨텍스트를 복사하도록 한다.

예시) 아래처럼 Application에 @EnableAsync를 적용하고 SecurityContextHolder에 MODE_THREADLOCAL을 적용한 뒤, @Async 메소드에서 SecurityContext에 접근하면 NPE가 발생하는 것을 확인할 수 있다.

// 구성 설정
``` java
@Configuration
@EnableAsync
public class ProjectConfig {

    @Bean
    public InitializingBean initializingBean() {
        return () -> SecurityContextHolder.setStrategyName(SecurityContextHolder.MODE_THREADLOCAL);
    }

}
```

// 엔드포인트에서 실행되는 @Async 메소드에서 SecurityContext에 접근

```java
@GetMapping("/async")
@Async
public String test() {
    var context = SecurityContextHolder.getContext();
    return context.getAuthentication().getName();
}
```

※ 하지만 MODE_INHERITABLETHREADLOCAL 전략을 사용하더라도 프레임워크가 자체적으로 스레드를 만드는 경우가 아니라 코드로 직접 스레드를 만드는 경우에는 프레임워크가 해당 스레드에 대해 모르기 때문에, SecurityContext가 복사되지 않는다. 


`코드로 직접 생성한 스레드에 SecurityContext 전달하기 1`

스레드를 직접 생성하는 경우에는 DelegatingSecurityContextRunnable, 또는 DelegatingSecurityContextCallable로 보안컨텍스트를 직접 전달하는 방법을 사용해야 한다. 

이렇게 개발자가 직접 관리해주는 스레드를 '자체 관리 스레드'라고 불린다.

Spring Security에서는 자체 관리 스레드에 SecurityContext를 복사하도록 Runnable과 Callable<T>을 데코레이팅할 수 있는 두 인터페이스가 있다.
- DelegatingSecurityContextRunnable : 반환값 X
- DelegatingSecurityContextCallable<T> : 반환값 O

이 두 가지 인터페이스 중 원하는 타입으로 정의하여(또는 람다로 정의하여) ExecutorService에 submit해주면 보안컨텍스트를 전달할 수 있다.

예시)

``` java
Callable<String> task = () -> {
    return SecurityContextHolder.getContext()
		.getAuthentication()
		.getName();
}

var e = Executors.newCachedThreadPool();

try {
    return e.submit(new DelegatingSecurityContextCallable<>(task))
	    .get();
} finally {
    executorService.shutdown();
}
```


`코드로 직접 생성한 스레드에 SecurityContext 전달하기 2`

또 다른 방법으로는 ExecutorService를 확장하는 DelegatingSecurityContextExecutorService 구현체에 Runnable/Callable을 submit하는 것이다.

예시)

```java
Callable<String> task = () -> {
    return SecurityContextHolder.getContext()
		.getAuthentication()
		.getName();
}

var e = new DelegatingSecurityContextExecutorService(Executors.newCachedThreadPool());

try {
    return e.submit(task)
	    .get();
} finally {
    executorService.shutdown();
}
```




<br/>
</p>
  </blockquote>
</details>