# 3. 상속 및 클래스

<br>

## 상속
---
- 부모 클래스를 상속 받은 자식 클래스는 "부모 클래스의 속성과 기능도 이용"할 수 있다.
- <code>Parent Class</code> = 부모 클래스 = 상위 클래스</br>
- <code>Child Class</code> = 자식 클래스 = 하위 클래스</br>
> Child Class로 생성한 객체는 <code>Parent Class의 속성과 기능 + Child Class의 속성과 기능</code> 모두 이용할 수 있다. 

<br>

## 상속의 필요성
---
- 기존의 검증된 클래스를 이용해서 빠르고 쉽게 새로운 클래스를 만들 수 있다. 
- 검증된 상위 클래스를 보완, 개선하기 때문에 더욱 견고한 클래스를 만들 수 있다.
> 상위 클래스의 속성과 기능에 <code>새로 필요한 속성과 기능만 추가</code>하면 된다.

<br>

## 상속 구현
---
- 상위 클래스
```java
package project;

public class parentClass {

    // 기본 생성자
    public ParentClass() {
        System.out.println("ParentClass constructor");
    }

    //메소드
    public void parentFun() {
        System.out.println("--parentFun() START--");
    }

}
```

<br>

- 하위 클래스

```java
package project;

public class childClass {

    // 기본 생성자
    public ChildClass() extends ParentClass {
        System.out.println("ChildClass constructor");
    }

    //메소드
    public void childFun() {
        System.out.println("--childFun() START--");
    }

}
```

<br>

- 실행
```java
package project;

public class MasinClass {
    ChildClass child = new ChildClass();
    child.parentFun();
    child.childFun();
}
```

<br>

- 결과

```java
ParentClass constructor <br>
ChildClass constructor <br>
--parentFun() START-- <br>
--childFun() START-- <br>
```

<br>

> JAVA는 <code>단일 상속</code>만 지원한다.
 
<br>

## 부모 클래스의 private 접근자
---
- 자식 클래스는 부모 클래스의 모든 자원을 사용할 수 있지만,
- <code>private</code> 접근자의 속성과 메소드는 사용할 수 없다.

<br>

![Alt text](/img/private.jpg)

<br>

- 상위 클래스의 private 메소드
```java
package project;

public class parentClass {

    // 기본 생성자
    public ParentClass() {
        System.out.println("ParentClass constructor");
    }

    //메소드
    public void parentFun() {
        System.out.println("--parentFun() START--");
    }

    //private 메소드
    private void privateFun() {
        System.out.println("--privateFun() START--");
    }

}
```

<br>

- 실행
```java
package project;

public class MasinClass {
    ChildClass child = new ChildClass();
    child.parentFun();
    child.childFun();

    //private 메소드 강제 실행
    childClass.privateFun();
}


```

<br>

- 결과

```java
Error: 접근불가
```

<br>

> 부모 클래스의 private 메소드는 상속이 불가하다.