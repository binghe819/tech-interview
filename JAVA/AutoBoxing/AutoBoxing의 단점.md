# 편리함에 숨은 AutoBoxing의 단점

```java
public static long sumAllInteger() {
    Long sumValue = 0L;
    for (long i = 0L; i < Integer.MAX_VALUE; i++) {
        sumValue += i;
    }
    return sumValue;
}
```
위 코드에서 `sumValue`가 Wrapper Class를 사용하기 때문에 반복문 안에서 `Long + long` 연산이 발생한다.

연산 과정은 아래와 같다.
1. Wrapper Class도 클래스이기에 바로 연산할 수 없기에, 기본자료형 long으로 오토언박싱한다.
2. long끼리 연산을 한다.
3. 결과 값을 다시 Long 타입으로 오토박싱하여 `sumValue`에 담는다.

즉, 매 연산마다 오토언박싱 + 오토박싱이 발생한다.

**이렇게 불필요한 연산이 발생해 굉장히 비효율적이다.**

<br>

`sumValue`를 long으로만 바꾸면 문제는 해결된다.

실제로 8배 정도 차이가 난다.
