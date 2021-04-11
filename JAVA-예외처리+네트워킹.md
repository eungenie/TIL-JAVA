# 4.1 예외처리

<br>

## 예외
---
- 프로그램에 문제가 있는 것
- 예외로 인해 시스템 동작이 멈추는 것을 방지하는 것을 <code>예외처리</code>라고 한다.

<br>

> Exception
<br>

- 개발자가 <code>대처할 수 있다.</code>
- 코드상의 문제
- 예) 정수를 0으로 나눔
- <code>Checked Exception</code>과 <code>Unchecked Exception</code>으로 나뉜다.

<br>

- Checked Exception
    - <code>예외처리</code>를 반드시 해야하는 경우
    - 처리하지 않을 시 compile 부터 진행되지 않는다.
    - 예) 네트워크, 파일 시스템(파일의 입출력)

<br>

- Unchecked Exception
    - <code>예외처리</code>를 개발자 판단에 맡기는 경우
    - 예) 데이터 오류

<br>

> Error
<br>

- 개발자가 <code>대처할 수 없다.</code>
- 소프트웨어적으로 해결할 수 없는 물리적 장애 요소
- 예) 메모리 부족, JVM 문제 등

<br>

## Exception 클래스
---
- JAVA에서 다양한 하위 클래스로 제공한다.
- <code>NullPointerException</code> : 객체를 가리키지 않고 있는 레퍼런스를 이용하는 경우
- <code>ArrayIndexOutOfBoundException</code> : 배열에 존재하지 않는 인덱스를 가리키는 경우
- <code>NumberFormatException</code> : 숫자 데이터에 문자 데이터 등 다른 데이터를 넣는 경우
- <code>IllegalArgumentException</code>: 잘못된 인자를 전달하는 경우
    - Error Msg: Mapped Statements collection does not contain value~

<br>

## try ~ catch
---
- 개발자가 예외처리하기 가장 쉽고, 많이 사용되는 방법
- try 구문 안에서 예외가 발생한 이후에 작성된 코드부터는 실행되지 않는다.

<br>

- 사용 방법
```java
try {
    //예외가 발생할 수 있는 코드
} catch (Exception e) {
    //예외가 발생했을 때 처리할 코드
}
```

<br>

- 예시 - 실행
```java
int i = 10;
int j = 0;
int r = 0;

try {
    r = i/j;
} catch (Exception e) {
    e.printStackTrace(); //발생한 예외를 console에 출력
    String msg = e.getMessage(); //발생한 예외를 문자열로 간략하게 나타냄
    System.out.println("Exception msg: " + msg);
}
```

<br>

- 예시 - 결과
```java
java.lang.ArithmeticException: / by zero
Exception msg: / by zero
```

<br>

- Exception 뿐만 아니라 직접 해당하는 하위 클래스를 이용해서 예외처리
    - NullPointerException, IllegalArgumentException 등

<br>

## finally
---
- 예외 발생 여부에 상관없이 반드시 실행된다.

<br>

- 예시 - 실행
```java
int i = 10;
int j = 0;
int r = 0;

try {
    r = i/j;
} catch (Exception e) {
    e.printStackTrace();
    String msg = e.getMessage();
    System.out.println("Exception msg: " + msg);
} finally { // 예외 발생여부와 관계없이 반드시 실행되어야 하는 경우
    System.out.println("가나다라");
}
```

<br>

- 예외 - 결과
```java
java.lang.ArithmeticException: / by zero
Exception msg: / by zero
가나다라
```

<br>

## throws
---
- 예외 발생 시 예외처리를 직접 하지 않고, 호출한 곳으로 넘긴다.

- 예시 - 실행
```java
MainClass mainClass = new MainClass();

try {
    mainClass.firstMethod();
} catch (Exception e) {
    e.printStackTrace();
}

public void firstMethod() throws Exception {
    secondMethod();

public void secondMethod() throws Exception {
    System.out.println("10 / 0 = " + (10 / 0));
}
```

<br>

- 예시 - 결과
```java
java.lang.ArithmeticException: / by zero
    at project.MainClass.secondMethod(MainClass.java:n번째 줄)
    at project.MainClass.firstMethod(MainClass.java:i번째 줄)
    at project.MainClass.main(MainClass.java:j번째 줄)
```

<br>

- 예시 - flow
> 1. <code>secondMethod()</code>의 Exception이 f<code>irstMethod()</code>로 throw
> 2. <code>firstMethod()</code>의 Exception이 <code>mianClass</code>로 throw
> 3. <code>mianClass</code>에서 <code>해당 Exception을 catch</code>하여, e.pringStackTraece() 실행

<br>
<br>

<pre></pre>

<br>
<br>

# 4.2 입력과 출력

<br>

## 입출력
---
 - <code>입력(input)</code>: 다른 곳의 데이터를 가져오는 것
    - 파일 읽기, 이미지 불러오기
 - <code>출력(output)</code>: 다른 곳으로 데이터를 내보내는 것
    - 파일 쓰기, 이미지 내보내기
- <code>stream</code>: 데이터가 오가는 길
    - 입출력할 대상들을 stream으로 연결

<br>

## 입출력 기본 클래스
---
- 입출력에 사용되는 기본 클래스
- <code>1byte</code>단위로 데이터를 전송
- InputStream, OutputStream

<br>

- InputStream
    - FileInputStream
    - DataInputStream
    - BufferedInputStream

<br>

- OutputStream
    - FileOutputStream
    - DataOutputStream
    - BufferedOutputStream

<br>

## FileInputStream / FileOutputStream
---
- 파일에 데이터를 <code>읽기</code> / <code>쓰기</code> 위한 클래스
- <code>read()</code> / <code>write()</code> 메소드를 이용

<br>

- FileInputStream

    > <code>read()</code>: 1byte씩 읽기<br>
    > <code>read(byte[])</code>: [](배열) 크기만큼 읽기 -> 그냥 read()보다 속도 up

<br>

- FileOutputStream

    > <code>write(byte[] b)</code>: 전체 쓰기<br>
    > <code>write(byte[], int off, int len)</code>: off -> 시작점, len -> 길이

<br>

```java
//예시 추가
```

<br>

## 파일 복사
---
- 파일 입출력 클래스를 이용해 파일을 복사할 수 있다.
```java
//예시 추가
```

<br>

## DataInputStream / DataOutputStream
---
- 문자열 단위로 <code>읽기</code> / <code>쓰기</code>
- byte 단위의 입출력을 개선
```java
//예시 추가
```

<br>

## BufferedReader / BufferedWriter
---
- 문자열 단위로 <code>읽기</code> / <code>쓰기</code>
- byte 단위의 입출력을 개선
```java
//예시 추가
```