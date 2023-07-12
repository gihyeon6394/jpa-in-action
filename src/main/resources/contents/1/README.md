## 1장 JPA 소개

1. SQL을 직접 다룰 때 발생하는 문제점
    1. 반복, 반복 그리고 반복
    2. SQL에 의존적인 개발
    3. JPA와 문제 해결
2. 패러다임의 불일치
    1. 상속
    2. 연관관계
    3. 객체 그래프 탐색
    4. 비교
    5. 정리
3. JPA란 무엇인가?
    1. JPA 소개
    2. 왜 JPA를 사용해야 하는가?

- Q&A ORM에 대한 궁금증과 오해

---

## 1. SQL을 직접 다룰 때 발생하는 문제점

Java application은 JDBC API를 통해 DB에 접근한다.

### 1.1 반복, 반복 그리고 반복

CRUD 업무에 따른 SQL이 무수히 반복

```java
public class Member {
    private String memberId;
    private String name;
    // ...
}
//...

public class MemberDAO {
    public Member find(String memberId) {
        //...
    }
}
```

#### 조회

1. 회원 조회 SQL 작성
2. JDBC API로 SQL 실행
3. 조회 결과를 Member 객체에 매핑

#### 저장

1. 회원 등록 SQL 작성
2. Member 객체의 값을 꺼내 SQL에 바인딩
3. JDBC API로 SQL 실행

데이터 베이스가 아닌 자바 컬렉션에 저장한다면 아래로 충분하다.

```java
list.add(member);
```

### 1.2 SQL에 의존적인 개발

Member 객체에 속성이 추가된다면?

```java
public class Member {
    private String memberId;
    private String name;
    private String tel; // 속성 추가
}
```

#### 저장

1. Member class 수정
2. insert SQL 문 수정

조회, 저장, 수정 모두 수정 필요

#### 연관된 객체

```java
// Entity
public class Member {
    private String memberId;
    private String name;
    private Team team; //연관 객체
}

public class MemberDAO {
    public Member find(String memberId) {
    }

    public Member findWithTeam(String memberId) {
    } // 연관 객체 조회
}
```

#### 문제점

- SQL과 JDBC API를 DAO에 숨겼지만 논리적으로 Entity와 강한 결합이 형성
- 진정한 의미의 계층 분할 어려움
- Entity 신뢰 문제
- SQL에 의존적인 개발

### 1.3 JPA와 문제 해결

```java
// 저장
jpa.persist(member);

// 조회
        String memberId="helloId";
        Member member=jpa.find(Member.class,memberId);

// 수정
        Member member=jpa.find(Member.class,memberId);
        member.setName("HelloJPA");

// 연관 객체 조회
        Member member=jpa.find(Member.class,memberId);
        Team team=member.getTeam();
```

## 2. 패러다임의 불일치

### 2.1 상속

객체는 상속이 있지만, 데이터베이스 테이블은 상속이 없음  
슈퍼타입, 서브타입 관계로 상속과 유사하게 설계 가능

```java
abstract class Human {
    private String name;
    private int age;
}

class IdolMember extends Human {
    private String group;
}

class Actor extends Human {
    private String agency;
}
```


### 2.2 연관관계

### 2.3 객체 그래프 탐색

### 2.4 비교

### 2.5 정리

