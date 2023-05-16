# StringBuilder vs StringBuffer  
  

#### String vs StringBuilder, StringBuffer  
```
우선 Java에서 문자열을 선언하기 위해 String과 StringBuilder StringBuffer  
를 사용한다. String이 이 위의 둘과의 차이점에 대해서 먼저 알아보겠다.  

우선 String은 불변하다는 특징이 있다.  
그래서 String으로 한번 선언한 문자열은 이후에 값 변경이 불가능하다는 것이다.
예를들어 +나 .concat을 사용하여 String의 값을 변경하면 기존의 값을 버리고 새로운 메모리를 할당한다.  
  
아래 예제를 보면,  
```

```java
    public static void main(String[] args) {
        String s = "Hello";
        //s이 기존 메모리 주소 버리고 새로운 메모리 주소 할당
        s.concat(" World");
        }
```
```
위 코드를 보면 String s가 "Hello"에서 "Hello World로 바뀌기를 기대한다.  
하지만 그렇지 않다. String s는 .concat등을 써서 문자열을 바꾸면, 기존의 할당된 메모리 값을 버리고,  
new String을 선언해 새로운 메모리를 할당받아 문자열을 만들고 반환한다.  
변경이 잦은 문자열을 계속 위 방식으로 사용한다면 속도가 급격히 느려질 것이다.

이를 해결하기 위해서는 StringBuffer 또는 StringBuilder를 사용하면 된다.  
이 둘은 String과 달리 가변적이다.   
StringBuffer 또는 StringBuilder로 선언된 문자열은 값을 변경해도 새로운 메모리가 할당 되지 않는다.

아래 예제를 보면,
```
```java
    public static void main(String[] args) {
        StringBuilder s = new StringBuilder("Hello");
        //새로운 메모리가 할당 되지 않음
        s.append(" World");
        }
```
```
위 코드와 같이 .append를 사용하여 값을 변경하더라도 
새로운 메모리가 할당 되지 않는다. StringBuffer도 마찬가지이다. 

그러면 StringBuilder와 String Buffer의 차이점은 무엇일까?
```
  
#### StringBuilder vs StringBuffer  
```
둘의 차이점은 동기화 지원 여부에 있다. 동기화를 지원 한다는 말은 멀티 쓰레드 환경에서 공유 자원에 접근할 때 안전 하다는 의미이다.  
StringBuilder는 동기화를 지원하지 않지만, StringBuffer는 동기화를 지원한다.

동기화 지원: StringBuffer
동기화 미지원: StringBuilder

따라서 멀티쓰레드 환경에서는 StringBuffer를 사용하는게 안전하다. 
하지만, StringBuilder는 StringBuffer보다 더 높은 속도를 자랑하므로  
싱글 쓰레드 환경에서는 StringBuilder를 사용하는게 유리하다.
```
  

  
