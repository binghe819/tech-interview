# Tech Interview 대비 지식 정리집

:baby_chick: 기술 인터뷰 지식 정리집

<br>

## 자료구조

<details>
  <summary>자료구조란?</summary>
  <ul>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EB%9E%80.md">자료구조란?</a></li>
  </ul>
</details>

<details>
  <summary>ArrayList vs LinkedList</summary>
  <ul>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/List/ArrayList.md">ArrayList</a></li>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/List/LinkedList.md">LinkedList</a></li>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/List/DoubleLinkedList.md">DoubleLinkedList</a></li>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/List/ArrayList%20vs%20LinkedList.md">ArrayList vs LinkedList</a></li>
  </ul>
</details>

<details>
  <summary>Stack</summary>
  <ul>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/Stack/Stack.md">Stack</a></li>
    <li><a href="#">Stack으로 Queue 구현하기 - 미완성</a></li>
  </ul>
</details>

<details>
  <summary>Queue</summary>
  <ul>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/Queue/Queue.md">Queue</a></li>
    <li><a href="./%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/Queue/Deque.md">Deque</a></li>
  </ul>
</details>

<br>

## 알고리즘

<details>
  <summary>정렬 알고리즘</summary>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=ww6URL1l1ho&t=19s">링크</a></li>
  </ul>
</details>

<br>

## JAVA

<br>

### 공통

<details>
  <summary>자바란 무엇인가?</summary>

  * 자바는 제임스 고슬링과 다른 연구원들이 개발한 객체 지향적 프로그래밍 언어이다.
  * 특징은 JVM (WORA), GC등등
</details>

<details>
  <summary>Primitive Type vs Wrapper class</summary>

  * Wrapper Class를 사용하는 이유
    * Nullable
    * `toString()`를 통해 String 타입으로 바로 변환 가능
    * Generic 타입으로 사용하기 위함
    * 멀티스레딩에서 동기화를 지원하려면 객체가 필요 (?)
  * Boxing vs Unboxing (Auto)
    * Primitive -> Warpper : Boxing
    * Wrapper -> Primitive : Unboxing
    * JVM은 상황에 따라 Boxing을 하기도, Unboxing을 하기도 한다.
    * [편리한 AutoBoxing의 단점](./JAVA/AutoBoxing/AutoBoxing의%20단점.md)
      * **Wrapper Class를 연산하면 오토박싱/언박싱이 일어나기에 비효율적이다.**
</details>

<details>
  <summary>Generic은 왜 Wrapper Class만 사용한가?</summary>

  * 우선 Generic을 사용하는 가장 큰 이유가 타입 체크를 위함이다. 즉, 컴파일 타임시에만 타입 체크 및 제약을 적용하고, 자동 형변환을 해준다. 그리고 컴파일 된 .class 파일에는 실제로 제네릭 정보가 전혀 없다. (소거됨)
  * 다르게 말하면 런타임엔 Generic으로 주어진 타입으로 형변환 된 Object만이 존재할 수 있다. 그러기 때문에 Primitive 타입은 Object가 될 수 없기에 불가능한 것.
  * 쉽게 말하면 **Generic 특성상 Object로 Convertable한 타입만 가능하다.**
  * [참고 1](https://www.quora.com/Why-is-it-impossible-to-use-primitive-types-as-a-type-parameter-in-Java), [참고 2](https://stackoverflow.com/questions/2721546/why-dont-java-generics-support-primitive-types)
</details>

<details>
  <summary>생성자 vs 정적 팩토리 메서드</summary>

  * 생성자와 정적 팩토리 메서드의 차이는 정적 팩토리 메서드의 장단점으로 알 수 있다.
  * 정적 팩토리 메서드의 장점
    * 이름을 가질 수 있다.
    * **반드시 새로운 객체를 만들 필요가 없다. 불변 객체를 캐싱하거나, Validation을 처리할 수 있다.**
    * 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.
    * 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.
    * static 팩토리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.
  * 정적 팩토리 메서드의 단점
    * 상속하려면 public, protected 생성자가 필요하니, 정적 팩토리 메서드만 제공하면 하위 클래스를 만들 수 없다.
    * static 팩토리 메서드는 프로그래머가 찾기 어렵다.
</details>

<details>
  <summary>String 객체는 객체인데 왜 new로 선언하지 않는가?</summary>

  * `String`은 대표적 **불변 객체**로, `String 상수 풀 영역`에서 객체를 관리한다.
  * 즉, 상수처럼 **이미 선언된 String 객체가 있으면 이 영역에서 가져다 사용하고, 없다면 여기에 새롭게 객체를 생성하여 사용한다.**
</details>

<details>
  <summary>불변 객체를 써야하는 이유</summary>

  * 불변 객체란?
    * 불변 객체란 **생성 후 그 상태를 변경할 수 없는 객체**를 말한다. 반대 개념으로 가변(mutable)객체가 있다.
    * 불변 객체란 **외부에서 불변 객체의 값을 수정할 수 없는 객체**를 의미한다.
    * 대표적인 불변 객체: `String`, `Boolean`, `Integer`
    * 대표적인 가변 객체: `StringBuilder`
  * 불변 객체를 왜 사용하는가?
    * 멀티 스레드 환경에서 안전하다. 동기화를 고려하지 않아도 된다.
    * 부수효과가 발생할 확률이 적다.
      * 객체는 기본적으로 참조 값을 통해 접근하기 때문에, 방어적 복사를 통해 불변으로 만들어 두는 것이 좋다.
      * 예를 들어, 여러 스레드나 메서드에서 Money를 사용하게 된다면 언제 어디서 부수 효과가 발생해 내부 값이 변경 될지 모르기 때문에 안전하지 않다.
    * 캐시나 Map또는 Set의 요소를 활용하기에 적합하다.
    * GC의 성능을 높일 수 있다.
  * 컬렉션을 불변으로 만들려면 요소도 불변으로 만들어줘야된다.
    * `List`를 불변으로 해도, 그 요소가 불변이 아니면 언제든 가변이 될 수 있기 때문이다. 
</details>

<details>
  <summary>불변으로 객체를 만드는 방법</summary>

  * 원시 타입에서의 불변
    * 원시 타입은 값을 그대로 외부로 내보내도 불변임을 보장한다.
    * 하지만, 객체의 `Setter`를 통해서는 객체 내부에서의 원시 타입은 불변을 막을 수 없다.
    * **`Setter`를 생성하지 않고, 생성자만을 통해서 설정되도록하면 불변을 보장할 수 있다.** 혹은 특정 메시지를 통해서만 원시 타입이 변경되도록 하면 된다.
  * 참조 타입에서의 불변
    * 객체는 기본적으로 참조 값을 통해 접근하기에, 불변성을 보장하기 더 힘들다.
    * **final + 방어적 복사 (생성자, Getter, 기타 반환 메서드)를 통해 참조 타입을 불변으로 만들 수 있다.**
    * **컬렉션을 불변으로 만들기 위해서는, 해당 컬렉션의 요소도 불변으로 만들어줘야한다.**
    * 더 자세한 내용은 [여기](https://github.com/binghe819/TIL/blob/master/JAVA/%EA%B8%B0%ED%83%80/%EB%B6%88%EB%B3%80%20%EA%B0%9D%EC%B2%B4.md)
</details>

<details>
  <summary>자바에서 null을 안전하게 다루는 방법은?</summary>

  * null의 정의
    * null은 값이 할당되지 않은 변수
    * 모든 참조 유형이 될 수 있는 특수 리터럴
    * "객체 없음", "알 수 없음", "사용할 수 없음"등 응용 프로그램(환경)마다 정의를 다르게 할 수 있다.
  * null의 문제점
    * null은 쉽게 NPE를 발생시킬 수 있다.
    * null을 반환할 수 있는 메서드는 클라이언트로 하여금 혼란을 초래할 수 있다.
      * 클라이언트 입장에서 null이 반환되는 메서드인지 아닌지 항상 확인해줘야한다.
  * null을 안전하게 다루는 방법
    * Assertion (단정문) 사용
    * **Objects** 사용 (`isNull`, `nonNull`, `requireNonNull`, ...)
    * `Optional`
  * 추천하는 null 방지 도구
    * `Optional`
    * JSR 305
    * JSR 308 (`@NonNull`, `@Nullable`)
</details>

<details>
  <summary>Optional 사용시 주의할 점</summary>

  * 쉽게 요약하면, `Optional`은 최대 1개 원소를 가지는 특별한 Stream이라고 생각하고 사용하면 된다.
  * `isPresent()`를 사용하지 않는다. -> `orElse`, `orElseGet` 등을 사용하자.
    * `isPresent()`를 호출하여 null인지 확인하고 다른 로직을 가져가는 경우. 이 경우 굳이 `Optional`로 감쌀 필요가 없다.
    * 차라리 그냥 null인지 확인하는 로직을 넣는 것이 더 좋다. 대신 `orElse`, `orElseGet`등등을 사용하자.
  * `orElse(new ...)` 대신 `orElseGet(() -> new ...))`를 사용하자.
    * `orElse(new ...)`는 무조건 실행된다. 만약 새로운 객체를 생성하거나 새로운 연산을 수행하는 경우에는 `orElseGet(() -> new ...))`를 사용하자. 이는 Optional에 값이 없을 때만 실행된다.
  * Optional은 필드로 사용하면 안된다. 반환 값으로만 사용하자
  * Optional은 비싸다. 비어있는 컬렉션을 반환할 때는 Optional을 감싸지 말고, 빈 컬렉션을 반환하자.
  * 더 자세한 내용은 [여기](http://homoefficio.github.io/2019/10/03/Java-Optional-%EB%B0%94%EB%A5%B4%EA%B2%8C-%EC%93%B0%EA%B8%B0/)를 참고
</details>

<details>
  <summary>java의 main 메서드가 static인 이유 - 미완</summary>
  <ul>
    <li></li>
    <li></li>
  </ul>
</details>

<details>
  <summary>java의 non-static와 static의 차이</summary>

  * non-static은 특정 객체의 대한 상태(동적 변수 혹은 인스턴스 변수)를 의미하고, static은 여러 객체가 공유하는 상태(정적 변수 혹은 클래스 변수)를 의미한다.
  * non-static은 객체가 생성되고 할당되며, 해당 객체의 상태를 나타내며, static은 객체가 생성되지 않아도 할당되며, 모든 객체에서 사용 가능하다.
  * non-static 메서드에서는 static 변수와 메서드에 모두 접근 가능하지만, static 메서드에서는 non-static 변수와 메서드에 접근하지 못한다. (아직 생성되지 않았기에)
  * **생명주기가 다르다.** non-static은 인스턴스와 생명주기를 같이 하며, static은 프로그램과 생명주기를 같이한다.
  * 쉽게 얘기하면, **non-static은 인스턴스(객체)에 속하고, static은 클래스 자체에 속한다.**
</details>

<details>
  <summary>java의 데이터 타입</summary>

  * 기본형 데이터 타입
    * 숫자형
      * 정수 - byte (1byte), short(2byte), int(4byte), long(8byte)
      * 실수 - float(4byte), double(8byte)
      * java는 기본적으로 unsigned를 제공하지 않는다. wrapper class를 이용하면 되지만 추천하지 않는다.
      * 데이터 타입별 표현 가능 범위는 [여기](https://velog.io/@bsjp400/JAVA-%EB%8D%B0%EC%9D%B4%ED%84%B0%ED%83%80%EC%9E%85-Datatype)
    * 논리형 - boolean (1byte)
    * 문자형 - char (2byte) 모든 유니코드
    * 문자열 - String
  * 참조형 데이터 타입
    * 배열 타입
    * 열거 타입
    * 클래스, 인터페이스
</details>

<details>
  <summary>Enum을 사용하는 이유는?</summary>

  * Enum이 나오게 된 이유는 [여기](https://github.com/binghe819/TIL/blob/master/JAVA/%EA%B8%B0%ED%83%80/%EC%97%B4%EA%B1%B0%ED%98%95(enum).md)참고
  * Enum 장점
    * 코드가 단순해지며 가독성이 좋다.
    * 인스턴스 생성과 상속을 방지한다.
    * 상수를 의미할 뿐만 아니라, 객체처럼 사용할 수 있다. - 추가 속성, 메시지를 통한 자율성 보장등
  * Enum은 싱글톤 (하나만 생성하여 여러 객체가 나눠서 사용함)이며, new를 통해 생성할 수 없다.
</details>

<details>
  <summary>Generic을 사용하는 이유</summary>
  <ul>
    <li></li>
    <li></li>
  </ul>
</details>

<br>

### JVM, GC

<br>

## OOP

<br>

## 네트워크

<br>

## 운영체제

<br>

## DB

<br>

## 그 외

<br>
