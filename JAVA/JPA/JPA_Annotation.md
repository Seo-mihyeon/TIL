# JPA ANNOTATION 정리

    * ✅jpa를 사용하면서 하나씩 추가해보자 !

------------------------------------------------
## 1. @Entity
- DB 테이블에 대응하는 하나의 클래스
 - 해당 annotation이 붙어 있는 경우 JPA가 관리해주며, JPA를 사용해서 DB테이블과 
    매핑 작업을 할경우에는 필수적으로 매핑 처리를 해줘야만 한다.

### **🛠️속성**
    1. name : 기본적으로는 class 이름으로 지정되지만 따로 엔티티의 이름을 지정할 수 있다.

### **👀주의사항**
    1. 접근 제어자로 public 혹은 protected 인 기본 생성자가 필수적으로 필요하다.
    2. final 클래스, enum, interface, inner 클래스에서는 사용이 불가능하다.
    3. 저장하려는 속성은 final 이면 안된다.

### **✏️예시**
```java
@Entity // @Entity(name = "ExT" )이름 직접 지정
public class ExTable{
    ...
}
```

------------------------------------------------
## 2. @Id
- 특정 속성 값을 기본키로 설정해준다.

### **🛠️속성**
    ❌

### **👀주의사항**
    1. Id의 annotation만 설정해줄 경우 기본키에 대한 값을 직접 부여해줘야한다.
        : 자동으로 기본키의 값이 생성 되도록 설정해주는 annotation을 사용하면 유용하다.
          ( @GeneratedValue )

### **✏️예시**
```java
@Entity // @Entity(name = "ExT" )이름 직접 지정
public class ExTable{
    @Id
    private Long id;
}
```

------------------------------------------------
## 3. @GeneratedValue
- @Id로 설정된 기본키의 값이 자동으로 생성되게 설정해준다.

### **🛠️속성**
    1. strategy
        1) startegy = GenerationType.IDENTITY : (mysql) 기본키 생성을 DB에서 자체적으로 생성한다. 
        2) startegy = GenerationType.SEQUENCE : (oracle) 기본키 생성을 DB시퀀스를 이용해서 생성한다.
        3) startegy = GenerationType.TABLE : (전체DB)키 생성 테이블을 사용한다.
        4) startegy = GenerationType.AUTO : DB에 따라 자동으로 선택되어 생성된다. / JPA가 자동으로 선택해서 이행하기 때문에 DB를 변경 이후에도 코드 수정을 하지 않아도 된다.

### **👀주의사항**
    1. Id의 annotation만 설정해줄 경우 기본키에 대한 값을 직접 부여해줘야한다.
        : 자동으로 기본키의 값이 생성 되도록 설정해주는 annotation을 사용하면 유용하다.
          ( @GeneratedValue )

### **✏️예시**
```java
@Entity // @Entity(name = "ExT" )이름 직접 지정
public class ExTable{
    @Id
    @GeneratedValue
    private Long id;
}
```

------------------------------------------------
## 3. @Column
- 테이블 컬럼과 매핑한다.

### **🛠️속성**
    1. name
       : 필드와 매핑할 테이블 컬럼명 지정
    2. insertable (true/false)
       : 엔티티 저장시 필드값 저장 유/무
    3. updatable (true/false)
       : 엔티티 수정시 필드값 저장 유/무
    4. table
       : 하나의 엔티티를 두개 이상의 테이블에 매핑할 때 사용
    5. nullable (true/flase)
       : null값 허용 여부
    6. unique
       : 유니크 제약조건 부여
    7. columnDefinition
        : 데이터베이스 컬럼 정보를 직접 부여
    8. length
        : 문자 길이 제약조건 부여 (String 타입일때만)
    9. precision
        : 소수점을 포함한 전체 자릿수 여부 (BigDecimal 타입일때만)
    10. scale
        : 소수의 자릿수 (BigDecimal 타입일때만)

### **👀주의사항**
    ❌

### **✏️예시**
```java
@Entity // @Entity(name = "ExT" )이름 직접 지정
public class ExTable{
    @Id
    @GeneratedValue
    @Column(insertable = false)
    private Long id;
    
    @Column(updatable = false)
    private String name;

    @Column(nullable = false)
    private String age;

    ...

}
```

------------------------------------------------
