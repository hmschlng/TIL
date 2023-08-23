# 2023. 08. 22 

|분류|✏️ 할 일|💭 설명|✅ 완료 |
|-|-|-|-|
| Algo | Programmers - 정수 삼각형 | `Lv3` / `DP` |[x]|
| Algo | Programmers - 이중우선순위큐 | `Lv3` / `자료구조(Heap)` |[x]|
| SQL | Programmers - 오랜 기간 보호한 동물(2) | `Lv3` / `JOIN` | [x] |
| CS | SSIA ch4 공부 | 책 읽고 정리 | [x] |

## 인증 📸

### Programmers Lv3. 정수 삼각형
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/Xa6oVHT.jpg">
  <p>
    그리디를 사용하여 구현
  </p>
</details>
<br/>

### Programmers Lv3. 이중우선순위큐
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/8NaC5XI.jpg">
  <p>
    TreeMap을 사용해 구현
  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 오랜 기간 보호한 동물(2)
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/3jvHC83.jpg">
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
`암호 처리 - PasswordEncoder`

PasswordEncoder는 암호 validation을 위한 컴포넌트로, Spring Security에서는 암호 관리를 위한 SSCM(Spring Security Crypto Module)이라는 암호화 모듈에서 제공한다.
UserDetailsService와 함께 AuthenticationProvider가 서비스의 인증 논리를 위해 사용한다.
국내 법령(전자금융감독규정 13조 2항)에도 명시되어 있듯이, 시스템은 End user의 비밀번호를 보관할 시 암호화를 거쳐야 한다.

`기본 검증 로직`
기본적으로 사용되는 검증로직은 다음과 같다.

1. 사용자 추가 시 지정한 해싱 알고리즘으로 인코딩된 해시 값을 저장한다.
2. 인증 요청이 오면, 넘어온 raw password string을 인코딩한다.
3. 이 해시 값을 저장된 해시 값과 비교(equals)하여 일치하면 성공, 다르면 실패

`PasswordEncoder 재정의`

서비스에서 사용할 암호 인코딩과 검증을 지정하기 위해 PasswordEncoder 구현체를 재정의함으로써, 암호화/복호화에 사용할 알고리즘을 서비스에 맞게 구현할 수 있다. 하지만 Spring Security가 Encoding/Decoding을 위한 여러 알고리즘 모듈을 제공하기 때문에 직접 검증로직을 짜지 않아도 된다.

`PasswordEncoder 구현 옵션`

제공되는 인코더들의 종류는 다음과 같다(Springboot 2 기준 Deprecated 된 모듈들 제외)

1. ByCryptPasswordEncoder
2. SCryptPasswordEncoder
3. Pbkdf2PasswordEncoder
4. Argon2PasswordEncoder
5. DelegatePasswordEncoder

이 중 DelegatePasswordEncoder는 여러 해싱 알고리즘을 사용한 검증을 할 수 있게 해준다.

이게 가능한 이유는 DelegatePasswordEncoder가 Map<String, PasswordEncoder>의 형태로 PasswordEncoder들을 관리하고, 인코딩된 해시 값이 {bycrypt}$2a$10$xn3LI....의 형태로 해시 값의 맨 앞에 Map의 key string이 접두사로 붙기 때문이다.

※ 실제 서비스에서 기존의 알고리즘에 취약성이 발생하는 등 모종의 이유로 인증 알고리즘을 변경해야 한다면, 신규 유저들에게는 변경된 알고리즘으로 인코딩해서 DB에 저장하고, 이미 DB에 있는 기존 사용자들은 이전 알고리즘으로 인증하는 방법 등으로 써먹을 수 있어 보인다. 

 -> 개인적인 생각으로는 기존 유저에 대해 비밀번호 변경이나 MFA를 시키는 등의 추가 대처가 있어야 좀더 보안성이 보장될 것 같다. (워크넷에서 최근 인증 정책 변경에 대한 기존 사용자 인증 플로우에서 이 비슷한 방법을 사용하는 것 같다).

`SSCM의 기타 제공 옵션`

SSCM은 KeyGenerator나 Encryptor 등 다른 암호 관련 Util도 제공한다. 
KeyGenerator는 특정한 종류의 키를 생성하는 모듈이다.

※ PasswordEncoder에 해싱 알고리즘을 정의할 때 들어가는 salt를 이 KeyGenerator로 생성하는 등의 활용 예시가 있다.

Encryptor는 암호화를 시키는 암호기이다. 

※ 시스템의 컴포넌트 간에 데이터를 전송하거나 데이터를 저장할 때 암호화가 필요하다면 Encryptor를 사용할 수 있다.

<br/>
</p>
  </blockquote>
</details>