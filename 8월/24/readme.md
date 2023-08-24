# 2023. 08. 22 

|분류|✏️ 할 일|💭 설명|✅ 완료 |
|-|-|-|-|
| Algo | Programmers - 기지국 설치 | `Lv3` / `그리디` |<ul><li>- [x] </li></ul>|
| Algo | Programmers - 네트워크 | `Lv3` / `BFS` |<ul><li>- [x] </li></ul>|
| Algo | Programmers - 최고의 집합 | `Lv3` / `비둘기집` |<ul><li>- [x] </li></ul>|
| SQL | Programmers - 있었는데요 없었습니다 | `Lv3` / `JOIN` | <ul><li>- [x] </li></ul> |
| CS | User Entity와 UserDetails 책임 분리 방식 테스트 | 벤치마크 테스트를 통해 책임 분리 설계가 오버헤드를 유발하는 지 체크 | <ul><li>- [x] </li></ul> |

## 인증 📸

### Programmers Lv3. 기지국 설치
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/w7kYKD6.jpg">
  <p>
    이미 설치된 기지국의 범위를 벗어난 지역들마다, 그 길이를 w*2 + 1만큼으로 나누고, 나머지가 있으면 +1 을 하는 식으로 필요한 기지국의 최소 개수를 구했다.
  </p>
</details>
<br/>

### Programmers Lv3. 네트워크
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/BTmrB63.jpg">
  <p>
    모든 vertex들을 순회하며 bfs 진행, 이미 탐색한 vertex는 건너뛰는 방식으로 연결된 그래프들의 개수를 구했다.
  </p>
</details>
<br/>

### Programmers Lv3. 최고의 집합
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/epVhQAC.jpg">
  <p>
    n개의 수가 최대한 균등하게 분배될 수록 결과값이 커진다는 규칙 발견, 균등하게 분배했다.
  </p>
</details>
<br/>

### (SQL) Programmers Lv3. 있었는데요 없었습니다
<details close>
  <summary> 코드 보기 </summary>
  <img src="https://i.imgur.com/FbAkm2R.jpg">
  <p>
    inner join을 사용하여 구현
  </p>
</details>
<br/>

### User Entity와 UserDetails 책임 분리 방식 테스트
<details open>
  <summary> 내용 보기 </summary>
  <blockquote>
  <p>

`SRP를 적용한 User Entity와 UserDetails 설계 관련 추가 공부`

- UserDetails에서 제공하는 사용자 계정 관련 상태(isAccountNonExpired, isAccountNonLocked, isCredentialsNonExpired, isEnabled)를 서비스에서 사용한다면 User 엔티티에 상태값들을 추가해 관리할 수 있다. 


`User 엔티티 정의`

``` java

@Getter
@NoArgsConstructor
@Builder(toBuilder = true)
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id", nullable = false)
    private Long id;

    @Column(nullable = false)
    private String username;

    @Column(nullable = false)
    private String password;

    ...

    @Column(nullable = false)
    private Boolean isAccountNonExpired;

    @Column(nullable = false)
    private Boolean isAccountNonLocked;

    @Column(nullable = false)
    private Boolean isCredentialsNonExpired;

    @Column(nullable = false)
    private Boolean isEnabled;

}
```

`UserDetails 구현체 정의`

```java

public class CustomUserDetails implements UserDetails {

    private User user;

    public CustomUserDetails(User user) { this.user = user; }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() { return Collections.emptyList(); }

    @Override
    public String getPassword() { return user.getPassword(); }

    @Override
    public String getUsername() { return user.getUsername(); }

    @Override
    public boolean isAccountNonExpired() { return user.isAccountNonExpired; }

    @Override
    public boolean isAccountNonLocked() { return user.isAccountNonLocked; }

    @Override
    public boolean isCredentialsNonExpired() { return user.isCredentialsNonExpired; }

    @Override
    public boolean isEnabled() { return user.isEnabled; }
}
```

`UserDetailsService를 확장하는 UserDetailsManager 구현체 정의`

```java

@RequiredArgsConstructor
@Service
public class CustomUserDetailService implements UserDetailsManager {

    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;

    @Override
    public UserDetails loadUserByUsername(String id) throws UsernameNotFoundException  { ... }

    @Override
    public void createUser(UserDetails user)  { ... }

    @Override
    public void updateUser(UserDetails user) { ... }

    @Override
    public void deleteUser(String id) { ... }

    @Override
    @Transactional
    public void changePassword(String oldPassword, String newPassword) { ... }

    @Override
    public boolean userExists(String username) { ... }

}
```

<br/>
</p>
  </blockquote>
</details>