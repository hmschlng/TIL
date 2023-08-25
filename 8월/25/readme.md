# 2023. 08. 25 

|분류|✏️ 할 일|💭 설명|✅ 완료 |
|-|-|-|-|
| Algo | BOJ - 내리막길 | `Gold 3` / `DFS` |<ul><li>- [x] </li></ul>|
| SQL | Programmers - 헤비 유저가 소유한 장소 | `Lv3` / `HAVING` | <ul><li>- [x] </li></ul> |
| CS | SSIA ch5 절반 공부 | 책 읽고 정리 | <ul><li>- [x] </li></ul> |

## 인증 📸

### BOJ Gold 3. 내리막길
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/dKqW5Yl.jpg">
  <p>
  dp와 dfs를 사용해 구현
  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 헤비 유저가 소유한 장소
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/dmXFIYb.jpg">
  <p>
    having, join을 사용하여 구현
  </p>
</details>
<br/>

### Spring Security In Action ch5 공부
<details open>
  <summary> 내용 보기 </summary>
  <blockquote>
  <p>

`Spring Security In Action ch5 - AuthenticationProvider`

AuthenticationProvider는 UserDetailsService와 PasswordEncoder의 사용 주체로, 인증 로직을 담당하는 계층이다. 
AuthenticationManager는 HTTP 필터 계층에서 요청을 수신하고, 인증 책임을 AuthenticationProvider에게 위임한다.

서비스의 인증 로직을 커스터마이징하려면 이것의 구현체를 정의하면 된다.

`AuthenticationProvider 구현체 정의`

다음의 두 메소드를 오버라이딩해야 한다.

Authentication authenticate(Authentication authentication);
boolean supports(Class<?> authenticationType);

authenticate 메소드는 서비스에서 적용하려는 인증 유형 요청(Authentication)이 들어오면 이를 인증 로직을 거쳐 인증한 뒤 인증 결과를 Authentication 타입(주로 구현체)로 리턴한다.

supports 메소드는 AuthenticationProvider가 지원하려는 인증 유형이 맞는지 아닌지를 정의하는 역할을 한다.


`Authentication`
Authentication은 인증 프로세스의 핵심 인터페이스로, 인증 요청 이벤트를 나타내고, 애플리케이션에 접근을 요청한 엔티티의 세부 정보를 담는다. 
id/password, JWT, OAuth 등 여러 방식으로 인증에 필요한 값이 전달되는데 이것을 하나의 인터페이스로 받아 수행하도록 추상화 하는 역할의 인터페이스다.
Authentication 관련 정보는 인증프로세스 도중, 그리고 인증 이후에 이용할 수 있다.

Authentication은 Principal 인터페이스를 확장한다. Principal(주체)란 애플리케이션에 접근을 요청하는 사용자를 뜻하며, 인증 요청에 대한 최상위 인터페이스이다. 이에 따라 Authentication의 구현체는 Principal.getName()도 재정의하고 있다.

Spring Security는 다양한 인증 양식에 따른 Authetication 구현체를 제공한다. 이들은 모두 AbstractAuthentication 추상 클래스를 구체화하고 있다. 

- UsernamePasswordAuthenticationToken

- AnonymousAuthenticationToken

- RememberMeAuthenticationToken

- TestingAuthenticationToken

<br/>
</p>
  </blockquote>
</details>