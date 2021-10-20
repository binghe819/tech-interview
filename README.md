# Tech Interview 대비 지식 정리집

:baby_chick: 기술 인터뷰 지식 정리집

> 틀렸거나 애매모호한 내용은 언제든 이슈 남겨주세요 :)

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

#### Q. 자바란 무엇인가?
<details>
  <summary>답변</summary>

  * 자바는 제임스 고슬링과 다른 연구원들이 개발한 **객체 지향적 프로그래밍 언어**이다.
    * 엄밀히 말하면 멀티 패러다임 프로그래밍언어 (절차형, 함수형 모두 지원)
  * 특징
    * JVM (WORA) 가상머신 -> 운영체제와 독립적
    * GC라는 프로세스를 통해 자동으로 메모리 관리는 수행한다.
    * 멀티 스레드를 지원한다.
</details>

#### Q. Primitive Type vs Wrapper class
<details>
  <summary>답변</summary>

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

#### Q. Generic은 왜 Wrapper Class만 사용한가?
<details>
  <summary>답변</summary>

  * 우선 Generic을 사용하는 가장 큰 이유가 타입 체크를 위함이다. 즉, 컴파일 타임시에만 타입 체크 및 제약을 적용하고, 자동 형변환을 해준다. 그리고 컴파일 된 .class 파일에는 실제로 제네릭 정보가 전혀 없다. (소거됨)
  * 다르게 말하면 런타임엔 Generic으로 주어진 타입으로 형변환 된 Object만이 존재할 수 있다. 그러기 때문에 Primitive 타입은 Object가 될 수 없기에 불가능한 것.
  * 쉽게 말하면 **Generic 특성상 Object로 Convertable한 타입만 가능하다.**
  * [참고 1](https://www.quora.com/Why-is-it-impossible-to-use-primitive-types-as-a-type-parameter-in-Java), [참고 2](https://stackoverflow.com/questions/2721546/why-dont-java-generics-support-primitive-types)
</details>

#### Q. 생성자 vs 정적 팩토리 메서드
<details>
  <summary>답변</summary>

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

#### Q. String 객체는 객체인데 왜 new로 선언하지 않는가?
<details>
  <summary>답변</summary>

  * `String`은 대표적 **불변 객체**로, `String 상수 풀 영역`에서 객체를 관리한다.
  * 즉, 상수처럼 **이미 선언된 String 객체가 있으면 이 영역에서 가져다 사용하고, 없다면 여기에 새롭게 객체를 생성하여 사용한다.**
</details>

#### Q. ""와 new String("")의 차이점은?
<details>
  <summary>답변</summary>
  
  * `""`은 Heap 내의 별도 공간인 `String 상수 풀 영역`에 문자열을 생성하고, 같은 문자열은 한번만 생성된다.
    * `String 상수 풀 영역`에 생성되는 String 객체는 불변이다.
  * `new String()`는 일반 클래스와 마찬가지로 Heap에 문자열 객체로 생성된다.
</details>

#### Q. 불변 객체를 써야하는 이유
<details>
  <summary>답변</summary>

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
  * 컬렉션을 불변으로 만들려면 요소도 불변으로 만들어줘야된다.
    * `List`를 불변으로 해도, 그 요소가 불변이 아니면 언제든 가변이 될 수 있기 때문이다. 
  * 단점으로는 메모리 낭비를 유발할 수 있다는 것이다.
    * 단, 이것은 GC 커스텀을 통해 개선할 수 있을 듯 하다.
</details>

#### Q. 불변 만드는 방법
<details>
  <summary>답변</summary>

  * 원시 타입에서의 불변
    * 원시 타입은 값을 그대로 외부로 내보내도 불변임을 보장한다.
    * 하지만, 객체의 `Setter`를 통해서는 객체 내부에서의 원시 타입은 불변을 막을 수 없다.
    * **`Setter`를 생성하지 않고, final을 붙여줘 생성자만을 통해서 설정되도록하면 불변을 보장할 수 있다.** 혹은 특정 메시지를 통해서만 원시 타입이 변경되도록 하면 된다.
  * 참조 타입에서의 불변
    * 객체는 기본적으로 참조 값을 통해 접근하기에, 불변성을 보장하기 더 힘들다.
    * **final + 방어적 복사 (생성자, Getter, 기타 반환 메서드)를 통해 참조 타입을 불변으로 만들 수 있다.**
    * **컬렉션을 불변으로 만들기 위해서는, 해당 컬렉션의 요소도 불변으로 만들어줘야한다.**
    * 더 자세한 내용은 [여기](https://github.com/binghe819/TIL/blob/master/JAVA/%EA%B8%B0%ED%83%80/%EB%B6%88%EB%B3%80%20%EA%B0%9D%EC%B2%B4.md)
</details>

#### Q. 자바에서 null을 안전하게 다루는 방법은?
<details>
  <summary>답변</summary>

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

#### Q. Optional 사용시 주의할 점
<details>
  <summary>답변</summary>

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

#### Q. java의 main 메서드가 static인 이유 - 미완
<details>
  <summary>답변</summary>
  <ul>
    <li></li>
    <li></li>
  </ul>
</details>

#### Q. java의 non-static와 static의 차이
<details>
  <summary>답변</summary>

  * **non-static은 특정 객체의 대한 상태(동적 변수 혹은 인스턴스 변수)를 의미하고, static은 여러 객체가 공유하는 상태(정적 변수 혹은 클래스 변수)를 의미한다.**
  * non-static은 객체가 생성되고 할당되며, 해당 객체의 상태를 나타내며, static은 객체가 생성되지 않아도 할당되며, 모든 객체에서 사용 가능하다.
  * non-static 메서드에서는 static 변수와 메서드에 모두 접근 가능하지만, static 메서드에서는 non-static 변수와 메서드에 접근하지 못한다. (아직 생성되지 않았기에)
  * **생명주기가 다르다.** non-static은 인스턴스와 생명주기를 같이 하며, static은 프로그램과 생명주기를 같이한다.
  * 쉽게 얘기하면, **non-static은 인스턴스(객체)에 속하고, static은 클래스 자체에 속한다.**
</details>

#### Q. java의 데이터 타입
<details>
  <summary>답변</summary>

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

#### Q. Enum을 사용하는 이유는?
<details>
  <summary>답변</summary>

  * Enum이 나오게 된 이유는 [여기](https://github.com/binghe819/TIL/blob/master/JAVA/%EA%B8%B0%ED%83%80/%EC%97%B4%EA%B1%B0%ED%98%95(enum).md)참고
  * Enum 장점
    * 코드가 단순해지며 가독성이 좋다.
    * 인스턴스 생성과 상속을 방지한다.
    * 상수를 의미할 뿐만 아니라, 객체처럼 사용할 수 있다. - 추가 속성, 메시지를 통한 자율성 보장등
  * Enum은 싱글톤 (하나만 생성하여 여러 객체가 나눠서 사용함)이며, new를 통해 생성할 수 없다.
</details>

#### Q. Generic을 사용하는 이유
<details>
  <summary>답변</summary>
  
  * 컴파일 타임때 런타임때 실행되는 타입의 안정성을 제공하기 위해.
  * 자바는 데이터 바인딩에 공변성의 특징을 가지기 때문에, 버그 가능성이 있습니다. 따라서, 컴파일 타임에 런타이에 사용되는 타입을 검증을 하기 위함이다.
    * `<Object>`: Object만을 받아 들인다.
    * `<? extends Object>`: Object를 상속받은 객체를 받아 들인다.
</details>

#### Q. 오버로딩과 오버라이딩의 차이
<details>
  <summary>답변</summary>
  
  * 오버로딩: 재구성
    * 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것.
    * 단, 기존 메서드와 매개변수의 개수 또는 타입이 달라야한다.
    * 새로운 메서드를 정의하는 것.
  * 오버라이딩: 재정의
    * 인터페이스 혹은 상위 클래스의 메서드를 재정의.
    * 기존의 메서드를 재정의하는 것.
</details>

#### Q. try-with-resource
<details>
  <summary>답변</summary>
  
  * JAVA 7부터 지원하는 기능
  * `Closeable`을 구현하고 있는 객체만이 사용 대상이 될 수 있다. **리소스에 대한 자동 반납 기능을 지원한다.**
</details>

#### Q. Stream이란? 장점과 특징은?
<details>
  <summary>답변</summary>
  
  * Stream이란?
    * 자바 8에서 추가한 **스트림은 람다를 활용할 수 있는 기술** 중 하나이다.
    * **컬렉션, 배열 등에 저장된 요소들에 쉽게 접근할 수 있도록 추상화된 기술을 제공한다.**
    * **스트림은 '데이터의 흐름'이다.** **배열 또는 컬렉션에 함수 여러 개를 조합해서 원하는 결과를 필터링하고 가공된 결과를 얻을 수 있다.**
    * 람다를 이용해서 코드의 양을 줄이고 간결하게 표현한다.
    * DB의 쿼리(SELECT)와 같이 **정형화된 처리 패턴**을 적용시킨 것.
      * 배열 혹은 컬렉션의 데이터를 쿼리(Stream와 동일하다고 봐도 무방)하는 것.
  * Stream의 특징
    * 스트림은 **외부 반복을 통해 작업하는 컬렉션과는 달리 내부 반복 (internal interation)을 통해 작업**을 수행한다
      * 외부 반복 예시 : for문, 내부 반복 예시 : stream()....
    * 스트림은 재사용이 가능한 컬렉션과는 달리 **단 한 번만 사용할 수 있다**. (불변)
    * 스트림은 **원본 데이터를 변경하지 않는다**.
    * 스트림의 연산은 필터-맵(filter-map) 기반의 API를 사용하여 **지연 (lazy) 연산**을 통해 성능을 최적화한다.
    * 스트림은 parallelStream() 메서드를 통한 손쉬운 병렬 처리를 지원한다.
  * 구조
    * 생성
    * 중간 연산
    * 최종 연산
</details>

#### Q. Stream에서 map과 flatmap의 차이는?
<details>
  <summary>답변</summary>
  
  * map은 단일 스트림 안의 요소를 원하는 특정 형태로 변환시켜주는 중간 연산 메서드.
  * flatmap은 스트림의 형태(요소)가 배열이나 리스트일 때 각 리스트의 모든 원소를 특정 형태로 변환하고 단일 원소 스트림으로 반환시켜주는 중간 연산 메서드.
</details>

#### Q. 함수형 프로그래밍 개념과 특징
<details>
  <summary>답변</summary>
  
  * 함수형 프로그래밍
    * 함수를 값으로 바라보고 명령형이 아닌 선언형으로 프로그래밍 하는 프로그래밍 방식을 말한다.
  * 명령형과 선언형
    * 명령형 프로그래밍
      * What보다는 How을 나타냄.
      * ex. 클래스에서 메서드를 정의하고, 필요할 때 그 메서드를 호출하는 명령하여 동작.
    * 선언형 프로그래밍
      * How보다는 What을 설명.
      * ex. 데이터가 입력으로 주어지고, 데이터가 처리되는 과정(흐름)을 정의하는 것으로 동작.
  * 함수형 프로그래밍의 조건
    * 순수 함수
      * 부수효과가 없으며, 같은 입력이 주어지면 항상 같은 결과를 반환한다.
      * 멀티 스레드로부터 안전하다.
    * 고차 함수
      * 일급 함수의 특징을 만족해야한다.
      * 함수의 인자로 함수를 전달할 수 있다.
      * 함수의 리턴값으로 함수를 사용할 수 있다
    * 익명 함수
      * 이름이 없는 함수. 자바에서의 익명 클래스 혹은 람다식.
    * 합성 함수
      * 새로운 함수를 생성하거나 어떤 계산을 수행하기 위해 둘 이상의 함수를 결합하는 것이다.
      * 메서드 체이닝
  * 함수형 프로그래밍의 특징
    * 불변성
      * 상태를 변경하지 않는 것.
      * 상태를 변경하게 되면, 부수 효과가 생기게 되어 순수함수의 조건을 만족하지 못한다.
    * 참조 투명성 (순수 함수)
      * 프로그램 동작의 변경없이 관련 값을 대체할 수 있다면 표현식을 참조 상 투명하다고 한다.
      * 즉, 참조상 투명한 함수는 같은 입력이 주어지면 항상 같은 결과를 반환한다.
    * 일급 함수
      * 함수를 함수의 매개변수, 반환 값, 자료구조로 사용할 수 있다.
    * 게으른 평가
      * 함수형 언어에서는 값이 필요한 시점에 평가된다.
  * 함수형 프로그래밍의 장점
    * 동시성에서 발생할 수 있는 부수 효과를 없앨 수 있다.
    * 멀티 스레딩 환경에서 스레드 세이프를 보장하면서 안정적으로 병렬처리를 할 수 있다.
    * 높은 수준의 추상화를 지원한다. 개발자는 How보다는 What에 집중할 수 있다. (핵심 가치에 집중 가능)
    * 함수 단위의 코드 재사용이 수월하다.
    * 불변이기에 코드를 예측하기 쉽다.
</details>

#### Q. Lambda식이란?
<details>
  <summary>답변</summary>
  
  * Lambda식이란
    * **람다식은 메서드(함수)를 하나의 '식(expression)'으로 표현한 것**이다
    * **메서드로 전달할 수 있는 익명 클래스 메서드를 단순화 한 것.**
    * 함수형 인터페이스를 이용하여 람다식을 구현한다.
  * Lambda는 함수형 프로그래밍의 특징을 모두 가지고 있다고 보면 된다.
    * 일급 객체의 역할을 수행할 수 있으며, 메서드의 매개변수로 전달될 수도 있다. 또한, 변수에 담거나, 메서드의 결과값으로 반환될 수도 있다.
  * 장점
    * 불필요한 코드를 줄여주고, 가독성을 높여준다.
    * 익명 클래스와는 다르게 클래스를 생성하지 않는다.
</details>

#### Q. 익명 클래스 vs 람다식
<details>
  <summary>답변</summary>
  
  * 둘의 차이점은 바이트 코드를 보면 쉽게 파악할 수 있다.
  * 익명 내부 클래스는 새로운 클래스를 생성하지만, 람다는 새로운 메서드를 생성하여 포함한다.
    * 익명 내부 클래스
      * **static 중첩 클래스**를 생성한다.
    * 람다식
      * 람다식은 static이든, 객체를 사용을 위한 non-static이든 클래스를 따로 생성하지 않고, **메서드를 생성**한다. 
  * this
    * 익명 내부 클래스의 this: 새로 생성된 클래스
      * 새로운 클래스를 만들기 때문에, **익명 내부 클래스에서의 this는 익명 클래스 자신**을 가리킨다.
    * 람다식의 this: 람다식이 선언된 (포함하고 있는) 클래스
      * **람다식은 새로운 메서드**로 볼 수 있으며, 메서드에서 **this는 메서드를 가진 클래스**를 의미한다.
      * 즉, **람다식에서 this는 람다를 포함하는 클래스의 인스턴스**이다.
  * 메서드의 개수
    * 익명 내부 클래스는 여러 개의 메서드를 가질 수 있다.
    * 람다식은 `@FunctionalInterface`를 사용하므로, 하나 이상의 메서드를 가지면 컴파일 에러가 발생한다.
  * 람다도 일종의 클로저다.
    * 클로저: 함수 범위 밖의 자유변수를 참조할 수 있는 함수
    * 람다가 람다식 범위 밖의 변수에 접근하고자 한다면, 해당 변수는 `final`이어야 한다.
</details>

#### Q. 함수와 메서드의 차이
<details>
  <summary>답변</summary>
  
  * 근본적으로 동일. 함수는 일반적 용어, 메서드는 객체지향개념 용어
  * 함수는 클래스에 독립적
    * 함수(람다식)는 이 모든 과정없이 오직 함수(람다식) 자체만으로도 이 메서드의 역할을 수행할 수 있다.
  * 메서드는 클래스에 종속적
    * 모든 메서드는 클래스에 포함되어야하므로 클래스도 새로 만들어야 한다.
</details>

#### Q. Java 8에 추가된 기능
<details>
  <summary>답변</summary>
  
  * 추가된 기능
    * 가장 크게 추가된 부분은 Java에서 함수형 프로그래밍을 지원하기 시작. (람다, 스트림)
    * LocalDate, LocalDateTime 클래스가 새로 생김.
      * 이전의 Date와 Calendar는 가변이었다. 즉, set을 통해 값을 변경할 수 있으며, 부수효과가 발생하기 쉽다. 또한, 객체의 역할이 분담되어 있어, 년/월/일을 표현하고 계산하기 위해 둘 모두를 생성하는 비용이 든다.
      * LocalDate와 LocalDateTime은 이러한 문제를 해결했다.
    * 인터페이스에 default 메서드 정의 가능해짐.
    * Optional
</details>

#### Q. ==과 equals()의 차이점은?
<details>
  <summary>답변</summary>
  
  * `==` : 동일성
    * `==`은 primitive면 값 비교, reference이면 주소 비교를 통해 boolean 값을 리턴한다.
  * `equals()` : 동등성
    * `equals()`는 Object 클래스에 정의된 메서드이며, 객체의 값을 비교하여 boolean 값을 리턴한다.
    * `equals()`와 `hashCode()`를 재정의함으로써 동등성을 구현한다.
  * `hashCode()`를 재정의하지 않는다면?
    * `HashMap`과 `HashTable`에서 key에 대한 중복 여부를 `equals()`와 `hashCode()`로 하기 떄문에, 둘 다 재정의해줘야한다.
    * `hashCode()`를 재정의할 땐, 해당 객체의 상태를 통해 해시값을 계산해야한다.
  * [더 자세한 내용](https://github.com/binghe819/TIL/blob/master/JAVA/Effective%20Java/item11.md)
</details>

#### Q. Checked Exception vs Unchecked Exception
<details>
  <summary>답변</summary>
  
  * Checked Exception 
    * 프로그래머가 별도의 예외처리를 하지 않으면 컴파일 단계에서 오류를 발생시키는 예외.
    * 비관적인 예외처리 기법이라 불린다.
    * ex. SQLException, IOException
  * Unchecked Exception
    * 프로그래머가 별도의 예외처리를 하지 않아도 컴파일 단계에서 오류를 발생시키지 않는 예외.
    * 낙관적인 예외처리 기법이라 불린다.
    * ex. NPE, RuntimeException
</details>

#### Q. Checked Exception을 지양하는 이유는?
<details>
  <summary>답변</summary>
  
  * 자칫 잘못하면 한 메서드를 사용하는 모든 메서드가 무책임하게 `throws`로 예외를 던지는 문제가 발생한다.
  * OCP를 위반하게 될 수도 있다.
    * 특정 클래스에 의존하는 다른 클래스들로 예외 시그니처가 전달되고, 그로인해 발생하는 결합도가 유지보수성에 악영향을 끼친다.
    * 즉, **모든 상위 메서드들이 최하위 메서드의 예외 시그니처를 알아야 하므로 캡슐화가 깨진다.**
  * 예외를 `throw`한 메서드와 **depth가 3만 멀어져도 이 예외의 발생 근원지를 추측하기가 어려워진다.**
    * 어디서 진짜 예외가 발생했는지 찾기가 힘들다는 것.
  * 물론 반대 의견도 있다. 바로 `엘레강트 오브젝트`..
    * 각 클래스, 메서드의 시그니처가 아주 명확해야 한다는 의견이다.
    * 즉, **예외 가능성이 있는 메서드가 Unchecked Exception을 사용하는 것은 클라이언트를 속인다는 것!**
    * 하지만, 개인적으로 Unchecked를 사용하고, 문서화를 하는 것이 좋아보인다.
</details>

#### Q. 업캐스팅과 다운캐스팅
<details>
  <summary>답변</summary>
  
  * `캐스팅 == 형변환`
  * 업캐스팅
    * **하위 클래스의 객체가 상위 클래스 타입으로 형변환 되는 것.**
    * **상위 클래스 타입의 참조변수로 하위 클래스의 인스턴스를 참조하면 묵시적으로 업캐스팅이 발생한다.**
    * 물론 이때, 하위 클래스의 멤버에는 접근 불가하다.
  * 다운캐스팅
    * **자신의 고유한 특성을 잃은 하위 클래스의 객체를 다시 복구시켜주는 것을 의미한다.**
    * 즉, 업캐스팅된 것을 다시 원상태로 돌리는 것.
    * **주의 할점은 업캐스팅이 선행되어야 하며, 명시적으로 타입을 지정해줘야한다.**
</details>

#### Q. 정적 바인딩 vs 동적 바인딩이란
<details>
  <summary>답변</summary>
  
  * 바인딩
    * 프로그램 구성 요소의 성격을 결정해주는 것.
    * ex. 변수의 데이터 타입이 무엇인지 정해지는 것.
  * 정적 바인딩
    * 컴파일타임에 성격이 결정된다.
      * 변수의 경우 정적 할당(ex. c, c++,java). 컴파일 타임에 타입이 결정됨.
      * 메서드의 경우, 호출되는 메서드가 컴파일 타임에 결정된다.
  * 동적 바인딩
    * 다형성을 사용하여 메서드를 호출할 때, 발생하는 현상.
    * 런타임에 성격이 결정된다.
      * 변수의 경우 동적 할당(ex. python, kotlin). 런타임에 타입이 결정됨.
      * 메서드의 경우, 호출되는 메서드가 런타임에 결정된다.
</details>

#### Q. String vs StringBuffer vs StringBuilder
<details>
  <summary>답변</summary>
  
  * String은 불변, 나머지 둘은 가변
    * String은 불변이므로 지정된 문자열을 변경할 수 없다.
    * 나머지 둘은 변경이 가능하다.
  * StringBuffer와 StringBuilder의 장점
    * 문자열을 변경할 수 있기에 많은 문자열 연산시에 더 효율적이다.
  * StringBuffer와 StringBuilder의 차이점
    * StringBuffer는 equals 메서드를 오버라이딩하지 않는다.
    * StringBuilder는 StringBuffer에서 스레드 동기화 기능만 뺀 클래스이다. 멀티 스레드가 아니라면 StringBuilder가 더 효율적이다.
</details>

#### Q. HashMap vs HashTable vs ConcurrentHashmap
<details>
  <summary>답변</summary>
  
  * 공통점
    * 모두 Map 인터페이스를 구현한 구현체이며, `key:value` 구조를 가진 자료구조다.
  * thread-safe
    * HashMap은 주요 메서드에 synchronized 키워드가 없어 thread-safe하지 않다.
    * HashTable은 주요 메서드에 synchronized 키워드가 있어 thread-safe하다. 당연히 HashMap보다 느리다.
    * ConcurrentHashMap은 주요 메서드에 synchronized 키워드가 없지만, thread-safe하다. 서로 다른 스레드가 같은 해시 버킷에 접근할 때만 해당 블록이 잠기게 되므로, HashTable보다 효율적이다.
  * null 허용
    * HashMap은 key, value에 null을 허용한다.
    * HashTable과 ConcurrentHashMap은 key, value에 null을 허용하지 않는다.
</details>

#### Q. HashMap vs TreeMap vs LinkedHashMap
<details>
  <summary>답변</summary>
  
  * 조회
    * HashMap은 Hashing을 사용하여 데이터를 저장하기 때문에 조회시 O(1)이다.
    * TreeMap은 내부적으로 Red-Black 트리를 사용해 데이터를 저장하기 때문에 조회시 O(logN)이다.
  * 데이터 순서
    * HashMap은 데이터의 순서가 보장되지 않는다.
    * TreeMap과 LinkedHashMap은 데이터의 순서를 보장한다.
</details>

#### Q. java.util.Stack이 잘못된 이유
<details>
  <summary>답변</summary>
  
  * Stack의 문제점
    1. Vector를 상속받는다. Vector는 LIFO가 아닌 중간에 데이터 삽입, 삭제 연산도 가능하기 때문에 Stack의 본질에서 벗어난다.
    2. Stack은 synchronized 키워드로 thread-safe를 보장한다. 이는 성능적으로 오버헤드가 크다. 실사용 서버에선 좋은 선택이 아니다.
  * Stack 대신 무엇을 써야하는가?
    * Java API 문서에서는 더 완벽한 LIFO 자료구조로 Deque의 구현체인 ArrayDeque를 사용하라고 추천한다.
    * thread-safe해야한다면, ConcurrentLinkedDeque을 사용하면 된다. 이는 lock-free한 자료구조를 사용하여 thread-safe를 보장하여 성능상 더 유리하다고 한다.
</details>

#### Q. Inner Class와 Nested Class
<details>
  <summary>답변</summary>
  
  * 자바에선 class 안에 class를 선언할 수 있다.
    * 이를 통해 논리적으로 군집화를 할 수 있으며, 불필요한 외부 노출을 줄여 캡슐화를 할 수 있다. 또한, 가독성을 높이며 유지 보수하기 좋은 코드를 작성할 수 있다.
  * 종류
    * Static Nested Class
    * Inner Class
      * Local Inner Class
      * Anonymous Class
  * Static Nested Class vs Inner Class
    * 둘의 차이점은 static으로의 선언 여부이다. Inner Class는 static을 붙이지 않는 경우다.
    * 멤버 접근
      * Static Nested Class는 Outer Class의 static 멤버를 제외한 어떠한 멤버도 접근할 수 없다.
      * Inner Class는 Outer Class의 모든 멤버에 접근 가능하다.
    * 객체 생성
      * Static Nested Class는 Outer Class와 관계없이 독립적으로 객체를 생성 가능.
      * Inner Class는 Outer Class의 객체를 생성한 뒤 해당 객체를 이용해서 객체를 생성할 수 있다.
        * Inner Class의 경우 보통 Outer Class에 대한 참조를 갖고 있다. 이로인해 GC가 수거하지 못해, 메모리 누수 가능성이 있다.
  * Nested Class를 구현하는데 Outer Class에 대한 멤버를 참조하지 않는다면, 무조건 Static Nested Class로 선언해주는 것이 좋다.
</details>

#### Q. 접근 제어자
<details>
  <summary>답변</summary>
  
  * 접근 제어자란?
    * 클래스나 멤버 선언 시 부가적인 의미를 부여하는 키워드.
    * 객체지향의 정보 은닉을 위해 사용된다.
  * 종류
    * public: 외부에 전체 공개되며, 어디에서나 접근할 수 있다.
    * protected: 같은 패키지 혹은 다른 패키지에서 해당 클래스를 상속한 클래스에서 접근 가능하다.
    * default: 클래스 멤버는 같은 클래스의 멤버와 같은 패키지에 속하는 멤버에서만 접근 가능하다.
    * private: 같은 클래스 내에서만 접근 가능하며, 외부에서 접근이 불가능하다.
</details>

#### Q. System.out.println()대신 로깅을 사용하는이유
<details>
  <summary>답변</summary>
  
  * System.out.println의 단점
    * 로그가 시스템 콘솔에만 출력된다.
    * 로그 레벨을 설정할 수 없다.
    * 내부적으로 멀티스레드 환경에서 thread-safe를 보장하기 위해 synchronized를 이용하므로 성능이 좋지 않다.
  * 로깅 라이브러리의 장점
    * 많은 부가 정보 (스레드 정보, 클래스 이름)를 쉽게 볼 수 있다.
    * 로그 레벨을 설정할 수 있다.
    * 로그를 시스템 콘솔 외에도 파일이나 특정 서버로 보낼 수 있다. (저장 가능)
    * 비동기적으로 동작하도록 만들 수 있다. (성능상 좋음)
</details>

<br>

### JVM, GC

#### Q. JVM이란?
<details>
  <summary>답변</summary>
  
  * JVM이란
    * 자바 가상 머신.
    * 자바 바이트코드를 실행할 수 있게 해주는 주체다.
  * JVM의 특징
    * WORA (Write Once, Run Anywhere)
      * JVM은 플랫폼에 독립적이며, 모든 자바 가상 머신은 자바 가상 머신 규격에 정의된 대로 자바 바이트 코드를 실행한다. (스펙)
      * 모든 자바 프로그램은 CPU나 운영 체제의 종류와 무관하게 동일하게 동작하는 것을 보장한다.
      * 윈도우, 맥, 리눅스.. 등등 운영체제에 종속적이지 않다.
    * GC
      * 클래스 인스턴스는 사용자 코드에 의해 명시적으로 생성되고 GC에 의해 자동적으로 소멸된다.
</details>

#### Q. 자바 프로그램의 동작 과정
<details>
  <summary>답변</summary>
  
  1. JAVA 소스 코드 파일 (.java)를 JAVA 컴파일러 (javac)로 바이트 코드(.class)로 변환한다.
  2. JVM 내에 있는 Class Loader가 runtime data area로 바이트 코드 파일을 적재한다.
     * Loading -> Linking -> Initializing
  3. JVM 내에 있는 execution engine(Interpreter, JIT Compiler, GC)이 runtime data area에 적재된 바이트 코드를 기계어로 변경해 명령어 단위로 실행한다.
  
  > 더 자세한 내용은 [여기](https://github.com/binghe819/TIL/blob/master/JAVA/JVM/jvm_structure.md)
</details>

#### Q. JVM 메모리 구조
<details>
  <summary>답변</summary>
  
  * 자바의 실행 과정
    * JVM 내에 있는 Class Loader가 runtime data area로 바이트 코드 파일을 적재한다.
  * Runtime Data Area 구조
    * Method 영역 (static 영역)
      * 클래스 수준의 정보 (클래스 이름, 부모 클래스 이름, 메서드, 변수)를 저장한다. static으로 선언된 데이터들도 저장된다.
      * 프로그램이 끝날 때까지 유지되는 자원을 저장한다.
      * 모든 스레드에서 공유할 수 있는 자원
    * Heap 영역
      * new를 통해 생성된 객체와 배열이 저장된다.
      * GC의 대상이 되는 영역.
      * 모든 스레드에서 공유할 수 있는 자원.
    * Stack 영역
      * 메서드를 호출할 때마다 해당 메서드를 실행하기 위한 스택 프레임이 생성되는 영역. (콜스택)
      * 스택 프레임 내의 지역변수, 파라미터, 리턴 값, 참조 변수등을 저장한다.
      * 스레드마다 독립적으로 존재하는 영역이며, 스레드 간 공유가 불가능하다.
  * 더 자세한 내용은 [여기](https://github.com/binghe819/TIL/blob/master/JAVA/JVM/jvm_structure.md)
</details>

#### Q. GC란? - 예정
<details>
  <summary>답변</summary>
  
  
</details>

#### Q. GC 동작 방식 - 예정
<details>
  <summary>토글</summary>
  
  
</details>

#### Q. call by value와 call by reference
<details>
  <summary>답변</summary>
  
  * call by value
    * 함수 호출시 전달되는 변수의 값을 복사하여 함수의 인자로 전달하는 방식.
    * 복사된 인자는 함수 안에서 지역적으로 사용된다.
    * 따라서 함수 안에서 인자의 값이 변경되어도, 호출때 매개변수로 사용된 외부의 값은 변경되지 않는다.
    * Java의 경우 데이터 타입에 따라 함수 호출 방식이 달라진다.
      * primitive type (원시타입): call by value로 동작 (int, short, long, float, double, char, boolean)
      * reference type (참조타입): call by reference처럼 동작. (배열, 객체 인스턴스)
  * call by reference
    * 함수 호출시 인자로 전달되는 변수의 참조값을 전달하는 방식 (ex. c언어에서 포인터를 매개변수로 넘기는 것)
    * 따라서 함수 안에서 인자의 값이 변경되면, 호출때 매개변수로 사용된 외부의 값도 함께 변경된다.
  * Java는 call by value다.
    * 객체의 주소 값을 직접 넘기지 않고, 객체 주소를 바라보는 또 다른 변수를 복사해 만들어서 넘긴다.
      * 인스턴스에 접근하는 참조 값을 저장하는 변수를 넘기는 것.
    * Java uses only call by value while passing reference variables as well. It creates a copy of references and passes them as valuable to the methods.
</details>

#### Q. 리플렉션이란?
<details>
  <summary>답변</summary>
  
  * 리플렉션이란?
    * 컴파일되고 실행되면서 Class Loader에 의해 Method 영역에 로딩되있는 클래스의 메타데이터를 이용해 런타임 시점에 해당 클래스의 인스턴스를 생성하거나 멤버에 접근할 수 있도록 해주는 자바 API이다.
    * 이 모든 것을 런타임에 할 수 있다.
    * It allows an executing Java program to examine or "introspect" upon itself, and manipulate internal properties of the program. For example, it's possible for a Java class to obtain the names of all its members and display them.
  * 대표적 사용 예시
    * Component Scan (클래스의 애노테이션을 스캔하기 위해 클래스 메타 데이터를 이용하기 위함)
</details>

#### Q. 리플렉션 사용시 주의할 점
<details>
  <summary>답변</summary>
  
  1. 지나친 사용은 성능 이슈를 야기할 수 있다. 반드시 필요한 경우에만 사용할 것을 추천한다.
     * Component Scan처럼 프로그램 실행시 한 번만 하면 되는 경우에만 사용하는 것이 좋다.
  2. 컴파일 타임에 확인되지 않고 런타임 시에만 발생하는 문제를 만들 가능성이 있다.
  3. 접근 지시자를 의도적으로 무시할 수 있기 때문에 자칫하면 보안적 이유가 발생할 수 있다.
</details>

#### Q. 동기화(synchronized) vs 비동기화(asynchronized)
<details>
  <summary>답변</summary>
  
  * 동기화
    * 어느 메서드가 실행하는 동안 다른 메서드를 실행이 불가능하게 블록하는 것.
      * 작업을 요청한 후 해당 작업의 결과가 나올 때까지 기다린 후 처리하는 것.
    * **메서드를 실행시킴과 동시에 반환 값이 기대되는 경우.**
  * 비동기화
    * 어느 메서드를 실행하는 도웅에도 다시 메서드를 실행이 가능하다.
      * 작업을 요청한 후 해당 작업의 결과가 나올 때까지 기다리지 않고 다음 작업을 처리하는 것.
    * 메서드를 실행시키면 바로 blocking되지 않고 이벤트 큐 혹은 백그라운드 스레드에 해당 task를 위임하고, 바로 다음 코드를 실행하는 것.
    * ex. ajax, 스레드, 로깅 비동기 처리
</details>

<br>

## OOP

<br>

### 객체지향

#### Q. 객체지향이란?
<details>
  <summary>답변</summary>
  
  * 객체지향이란
    * 실세계에 존재하는 사물을 추상화시켜 상태와 행위를 가진 객체로 만들고, 그 객체들이 서로 상호작용하며 동작하도록 프로그래밍하는 프로그래밍 기법.
    * 프로그래밍 세계에서 "객체"들이 주가 되어, 각각의 "객체"가 메시지를 주고 받으며, 비즈니스 처리를 하는 것.
  * **객체지향의 본질**
    * **시스템을 상호작용하는 자율적인 "객체"들의 공동체로 바라보고 객체를 이용해 시스템을 분할하는 방법**
    * 자율적인 객체
      * 상태와 행위를 함께 지니며 스스로 자기 자신을 책임지는 객체.
    * 세 가지만 기억하자
      * **클래스는 도구일 뿐이다. 중요한 것은 객체의 역할, 책임, 협력이다.**
</details>

#### Q. SOLID 원칙이란?
<details>
  <summary>답변</summary>

  * 객체 지향 프로그래밍 및 설계의 다섯 가지 기본 원칙.
  > 보통 저수준의 SOLID를 많이 고민하지만, 고수준에도 동일하게 적용 가능하다. 이를 답변에서 얘기하자.
  * [SRP (Single Responsibility Principle)](https://github.com/binghe819/TIL/blob/master/OOP&%EC%84%A4%EA%B3%84/SOLID/SRP.md)
    * **어떤 클래스를 변경해야 하는 이유는 오직 하나뿐이어야 한다.**
    * 하나의 모듈은 하나의, 오직 하나의 액터에 대해서만 책임져야 한다.
      * 액터: 해당 모듈에 변경을 요청하는 한 명 이상의 사람들을 가리킴. (한명 혹은 집단)
    * 위반하는 예시
      * `Employee`라는 객체를 회계팀, 인사팀, DB 관리자 모두가 사용한다면, 해당 객체의 액터는 3개다.
      * 이때, 회계팀과 인사팀이 정의한 메서드가 동일한 private 메서드를 사용한다고 가정해보자, 해당 private 메서드의 변경으로 인해 두 액터에 영향을 끼치게 된다. 이는 SRP를 위반하는 것.
      * 이는 여러 액터가 단일 클래스에 의존하며, 의존하는 코드를 너무 가까이 배치했기 때문이다. 분리시켜야 한다.
    * 쉬운 예시
      * 남자보단 남자친구, 남편, 운동선수등등 구체적인 것이 SRP에 적합하다.
  * [OCP (Open Closed Priciple)](https://github.com/binghe819/TIL/blob/master/OOP&%EC%84%A4%EA%B3%84/SOLID/OCP.md)
    * **소프트웨어는 확장에 대해서는 열려 있어야 하지만 변경에 대해서는 닫혀 있어야 한다.**
      * **기존의 코드를 변경하지 않고 (Closed), 기능을 수정하거나 추가할 수 있도록 (Open)해야 한다.**
      * 인터페이스의 코드는 변경하지 않고, 인터페이스에 정의된 기능을 구현하는 구현체는 추가할 수 있도록 하는 원칙
    * OCP의 핵심은 런타임 의존성과 컴파일타임 의존성이다. - 다형성
      * 핵심은 컴파일타임 의존성을 고정시키고, 런타임 의존성을 변경하는 것. (동적 바인딩)
    * 예시
      * JDBC
  * [LSP (Liskov Substitution Priciple)](https://github.com/binghe819/TIL/blob/master/OOP&%EC%84%A4%EA%B3%84/SOLID/LSP.md)
    * 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다는 원칙
      * B가 A의 자식 타입이면, 부모 타입인 A객체는 자식 타입인 B로 치환해도, 기존 동작엔 문제가 없어야 한다는 원칙.
      * A - B의 부모 자식에 대한 정의가 논리적으로 제대로 된 상속이어야 기존 프로그램이 자식인 B로 치환해도 문제 없이 작동해야 한다는 의미
    * 부모에서 구현한 원칙을 자식도 따라야한다는 원칙.
      * 자식에서 부모의 구현을 변경하여, 기존의 로직에 영향을 주면 안된다.
    * 예시
      * 자동차 인터페이스가 있고 엑셀이라는 기능이 선언되어있다고 할때, 자동차 인터페이스의 구현체는 엑셀 기능을 앞으로 가는 기능으로 만들어야지 뒤로 가는 기능으로 만들면 안됩니다
  * [ISP (Interface Segregation Principle)](https://github.com/binghe819/TIL/blob/master/OOP&%EC%84%A4%EA%B3%84/SOLID/ISP.md)
    * 클라이언트는 자신이 사용하지 않는 메서드에 의존 관계를 맺으면 안된다.
      * 인터페이스는 그 역할에 충실한 최소한의 기능만 공개하라는 것.
    * 하나의 일반적인 인터페이스보다는, 여러 개의 구체적인 인터페이스가 낫다.
      * 불필요한 짐을 실은 무언가에 의존하면 예상치도 못한 문제가 발생할 수 있다.
    * 쉽게 말해, **인터페이스가 하나의 책임을 수행해야한다는 의미.**
  * [DIP (Dependency Inversion Principle)](https://github.com/binghe819/TIL/blob/master/OOP&%EC%84%A4%EA%B3%84/SOLID/DIP.md)
    * **추상화된 것은 구체적인 것에 의존하면 안된다는 원칙. 구체적인 것이 추상화된 것에 의존해야한다.**
    * **고차원 모듈은 저차원 모듈에 의존하면 안된다.** 이 두 모듈 모두 다른 추상화 된 것에 의존해야 한다는 원칙.
    * 예시
      * **카드 결제라는 고차원 모듈이 있다면, 카드 결제 컨트롤러에선 신한 카드 결제에 의존하지 말고, 카드 결제라는 추상적인 것에 의존해야 한다.**
      * 그리고 신한 카드 결제 혹은 다른 카드 결제들은 모두 카드 결제라는 모듈을 구현하는 저차원 모듈이다. (세부사항이다.)
</details>

#### Q. 응집도와 결합도
<details>
  <summary>답변</summary>
  
  * 응집도
    * **모듈에 포함된 내부 요소들이 연관돼 있는 정도를 나타냄.**
    * **응집도 높음** (좋음): 모듈 내의 요소들이 하나의 목적을 위해 긴밀하게 혀볅한다면 해당 모듈은 높은 응집도를 가진다고 할 수 있다.
    * 응집도 낮음: 모듈 내의 요소들이 서로 다른 목적을 추구한다면, 응집도가 낮다고 한다.
  * 결합도
    * **다른 모듈과의 의존성 정로를 나타낸다.**
    * 결합도 높음: 다른 모듈에 대해 너무 자세한 부분까지 알고 있으면 결합도가 높다고한다.
    * **결합도 낮음** (좋음): 다른 모듈에 대해 꼭 알아야 하는 부분만 알고 있다면 결합도가 낮다고 한다.
    * 결합도의 정도는 한 요소가 자신이 의존하고 있는 다른 요소에 대해 알고 있는 정보의 양으로 결정된다. 결합도가 낮을려면 협력하는 대상에 대해 더 적게 알아야 한다.
  * 이 둘은 캡슐화와도 관계가 있다.
    * 캡슐화의 정도가 객체의 응집도와 결합도를 결정하기 때문.
    * 캡술화를 잘 지키면 응집도는 높이고, 모듈 사이의 결합도는 낮출 수 있다.
</details>

#### Q. OOP의 4가지 특징
<details>
  <summary>답변</summary>
  
  * 캡상추다.
    * 캡슐화
      * 객체의 속성과 행위를 하나로 묶고, 실제 구현 내용 일부를 외부에 감추어 은닉하는 것.
      * 정보 은닉
    * 상속
      * 클래스들 간의 속성과 동작을 물려주는 것.
      * 이를 통해 클래스들 관계를 계층적으로 형성할 수 있다.
    * 추상화
      * 더 일반적인 개념을 의미.
      * 추상화를 통해 세부적인 내용이 아니라 일반적으로 표현하는 것.
      * ex. 신한 카드(구체)를 신용 카드로 추상화 시킴.
    * 다형성
      * 동일한 메시지를 수신 했을 때, 객체의 타입에 따라 다르게 응답할 수 있는 것. (컴파일 타임이 아닌 런타임에 형태가 결정된다.)
      * 인터페이스, 추상 클래스를 이용해 구현
</details>

#### Q. 추상클래스와 인터페이스의 차이
<details>
  <summary>답변</summary>
  
  * 목적이 다르다.
    * 추상 클래스: **상태와 행위들을 모아 놓은 템플릿**
      * 추상 클래스는 공통된 기능은 그대로 물려받거나 혹은 별도로 구현하고, 새로운 속성과 행위를 **확장하는 것이 목적**.
    * 인터페이스: **클라이언트에게 제공하는 명세(스펙).**
      * 인터페이스는 클라이언트에게 구현체의 메서드를 어떻게 사용할지에 대한 **명세를 제공하는 것이 목적**.
  * 상태와 행위
    * 추상 클래스는 non-static한 상태를 가질 수 있으며, 행위도 갖는다.
    * 인터페이스는 non-static한 상태를 가질 수 없으며, 행위도 갖지 못한다. 행위에 대한 명세만 가질 수 있다. (default로 상수는 가질 수 있다.)
  * 접근 제어자
    * 추상 클래스는 접근 제어자를 선택할 수 있다. (상속하려면 protected 이상)
    * 인터페이스는 모두 public으로 노출해야 한다.
  * 내부 구현
    * 추상 클래스는 내부 구현까지 물려준다(공유한다).(결합도가 높아진다.)
    * 인터페이스는 내부 구현이 없으므로, 공유하지 않는다.
  * 추상 클래스의 단점
    * **상위 하위 클래스 간의 결합도가 너무 높다.** (종속적이다)
      * 추상 클래스는 하위 클래스가 상위 클래스의 상태와 행위를 공유하기 때문에 하위 클래스가 상위 클래스에 의존하는 관계가 된다.
    * 정말 필요한 IS-A 관게를 제외하곤 인터페이스를 사용하는 것이 좋은 설계.
</details>

#### Q. 상속보다 합성이 좋은 이유는?
<details>
  <summary>답변</summary>
  
  * 상속
    * 두 관점에서 좋지 않다.
      1. 캡슐화를 위반
         * 내부 구현을 하위 클래스에 상속하므로 내용이 노출.
         * **상위 클래스가 변경되면 하위 클래스도 따라서 변경되므로 예상치 못한 결과를 얻을 수 있다.**
      2. 설계를 유연하지 못하게 한다.
         * **상위 하위 클래스 간의 관계가 컴파일 시점에 결정된다.**
         * 따라서 **실행 시점에 객체의 종류를 변경하는 것이 불가능하다.**
         * 부모에 너무 종속적이게 된다.
    * **추상 클래스는 하위 클래스가 상위 클래스의 대한 코드를 재정의하지 않고, 그저 확장할 때만 사용하는 것이 좋다.**
      * 템플릿 메서드 패턴
  * 합성
    * 인터페이스에 정의된 메시지를 통해서만 코드를 재사용하는 방법
    * 상속의 두 가지 단점을 모두 해결한다.
      * 인터페이스에 정의된 메시지를 통해서만 사용하기에 내부 구현을 캡슐화할 수 있다.
      * `setter`나 생성자를 통해 인스턴스 교체가 쉽기 때문에, 설계가 유연하다. 컴파일 타임이 아닌 런타임에 의존성 주입을 통하기 때문에 더 유연하다.
  * 쉽게 생각하면
    * **상속은 구체적인 것에 의존한다 (컴파일 타임) -> 코드의 수정이 발생한다.**
    * **합성은 추상적인 것에 의존한다 (런타임) -> 의존성만 바꿔주면 되므로, 코드의 수정이 필요없다.**
</details>

#### Q. 원시값 포장 vs VO
<details>
  <summary>답변</summary>
  
  * [여기](https://github.com/binghe819/TIL/blob/master/OOP&%EC%84%A4%EA%B3%84/%EA%B8%B0%ED%83%80/%EC%9B%90%EC%8B%9C%EA%B0%92%20%ED%8F%AC%EC%9E%A5%EA%B3%BC%20VO.md#3-%EC%9B%90%EC%8B%9C%EA%B0%92-%ED%8F%AC%EC%9E%A5%EA%B3%BC-vo%EC%9D%98-%EC%B0%A8%EC%9D%B4)를 참고
</details>

<br>

### 디자인 패턴


<br>

## 네트워크

<br>

## 운영체제

<br>

## DB

<br>

## 그 외

<br>
