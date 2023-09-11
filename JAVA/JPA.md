## JPA(Java Persistence API)이란 뭘까?
> JAVA를 활용해서 데이터베이스의 상호작용을 할 수 있게 도와주는 라이브러리이다.
> 즉, 데이터베이스와의 상호작용을 쉽고 효율적으로 만들어주는 도구나 프레임워크 중 하나를 말한다.

##### 장점
1. 쿼리를 사용하지 않고도 데이터베이스를 다를 수 있다
2. 데이터베이스와 애플리케이션 코드간의 매핑을 자동화 한다.
3. 코드를 간결하게 작성할 수 있다. 즉, 유지보수에 용이하다.

##### 엔티티 정의하기
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

```java
@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private int age;

    // Getter와 Setter 메서드는 생략
}
```

1. @Entity를 사용해서 해당 클래스가 데이터베이스 테이블과 매핑 되는 엔티티임을 표현한다.
2. @Id는 해당 클래스의 primary key 임을 나타낸다.
3. @GeneratedValue 는 해당 키 값이 자동으로 생성 되도록 설정한다.

