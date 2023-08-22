# 2023. 08. 22 

|분류|✏️ 할 일|💭 설명|✅ 완료 |
|-|-|-|-|
| Algo | Programmers - 베스트앨범 | `Lv3` / `자료구조(Hash)` |[x]|
| Algo | Programmers - 이중우선순위큐 | `Lv3` / `자료구조(Heap)` |[x]|
| SQL | Programmers - 오랜 기간 보호한 동물(1) | `Lv3` / `JOIN` | [x] |
| CS | SSIA ch3 공부 | 책 읽고 정리 | [x] |

## 인증 📸

### Programmers Lv3. 베스트앨범
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/jHzezPP.png">
  <p>
    HashMap과 PQ를 사용하여 구현
  </p>
</details>
<br/>

### Programmers Lv3. 이중우선순위큐
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/UfQ62ll.png">
  <p>
    TreeMap을 사용해 구현
  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 오랜 기간 보호한 동물(1)
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/VpvXrqK.png">
  <p>
    HashMap과 PQ를 사용하여 구현
  </p>
</details>
<br/>

### Spring Security In Action ch3 공부
<details open>
  <summary> 내용 보기 </summary>
  <blockquote>
  <p>

**3장 사용자 관리 - UserDetailsService**

UserDetailService는 인증 대상인 사용자의 세부 정보를 검색한다. 일반 아이디/패스워드 방식의 인증 절차에 사용되며, OAuth2 소셜 로그인만 사용할 경우엔 정의하지 않아도 된다.

**SpringSecurity의 인증 구조(자동 구성 기준)**
1. request가 DispatcherServlet에 도달하기 전, 필터 Layer에서 인증 필터가 요청을 가로챈다.
2. 요청한 사용자의 인증 절차를 거치기 위해 AuthenticationManager에게 인증 책임을 위임한다.
3. AuthenticationManager는 인증 논리를 구현하는 AuthenticationProvider를 이용한다.
4. AuthenticationProvider는 UserDetailsService에서 요청한 사용자를 찾고, PasswordEncoder에서 암호를 검증한다.
5. 인증 결과가 인증 필터에 반환된다.
6. 인증 이력이 SecurityContext에 저장된다.

**[UserDetailsService Component의 구조]**
- UserDetailsService : UserDetails를 검색한다.
- UserDetailsManager : UserDetails를 관리한다(사용자 추가, 수정, 삭제).
- UserDetails : 사용자 세부 정보 인터페이스로, 사용자 권한 관련 인터페이스인 GrantedAuthority를 가지고 있다.
- GrantedAuthority : 사용자 권한을 나타내는 인터페이스

UserDetailsService와 UserDetailsManager는 서로 분리되어 있는데, 이로 인해 앱에 필요한 동작만 구현할 수 있게 되면서 유연성이 향상된다. (인터페이스 분리 원칙)
- 사용자를 인증하는 기능만 필요한 경우 -> UserDetailsService만 구현
- 사용자를 관리하는 기능도 필요할 경우 -> UserDetailsManager까지 구현

**[UserDetails 정의]**
UserDetailsService와 UserDetailsManager를 사용한 인증을 위해서는 UserDetails를 구현한 사용자 클래스를 정의해야 한다.
UserDetails의 구현체는 GrantedAuthority로 나타나는 권한을 하나 이상 가지고 있어야 한다.
 -> UserDetails의 구현체가 재정의해야 하는 메소드 중에 `Collection<? extends GrantedAuthority> getAuthorities()` 가 있는데, 이를 정의하면서 위의 요구사항을 준수하게 된다.

※ 테이블 매핑을 위한 JPA User 엔티티에 UserDetails를 implement하는 것은 좋지 않다. 
-> 사용자 엔티티는 JPA 엔티티 책임만 위임하고, 인증 책임은 인증을 위한 사용자 객체에만 위임하여 "책임을 분리"하는 것이 좋다. 
예) User 엔티티, UserDetail를 구현하는 SecurityUser를 각각 정의하고, SecurityUser 클래스가 필드로 User를 가지고 있게 래핑한다.

**[UserDetailsService 정의]**</p>
  </blockquote>
</details>