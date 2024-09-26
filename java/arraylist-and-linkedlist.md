# ArrayList와 LinkedList

`ArrayList`와 `LinkedList`는 Java에서 자주 사용되는 `List` 인터페이스의 두 가지 대표적인 구현체입니다. 두 클래스는 모두 목록을 저장하고 처리하는 데 사용되지만, 내부적으로 데이터를 관리하는 방식이 다르기 때문에 성능 특성이 다릅니다.

## 1. ArrayList

- **배열 기반의 리스트:** `ArrayList`는 내부적으로 크기가 고정된 배열을 사용해 요소를 저장합니다. 배열의 크기가 가득 차면 자동으로 크기를 증가시키며, 새로운 배열을 만들어 기존 요소를 복사합니다.
- **빠른 조회:** 배열에 기반하고 있기 때문에 인덱스를 사용한 조회(get, set)가 매우 빠릅니다. `O(1)` 시간 복잡도를 가집니다.
- **느린 삽입과 삭제:** 배열의 중간에 요소를 삽입하거나 삭제하려면, 요소들을 이동시켜야 하기 때문에 `O(n)` 시간 복잡도가 발생합니다.

#### 예제 코드

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        // ArrayList 선언
        ArrayList<String> arrayList = new ArrayList<>();

        // 요소 추가
        arrayList.add("Apple");
        arrayList.add("Banana");
        arrayList.add("Orange");

        // 인덱스를 사용한 요소 조회
        System.out.println("Element at index 1: " + arrayList.get(1)); // Banana

        // 요소 삭제
        arrayList.remove(2); // Orange 삭제

        // 리스트 출력
        System.out.println("ArrayList elements: " + arrayList);
    }
}
```

## 2. LinkedList

- **이중 연결 리스트 구조:** `LinkedList`는 각각의 요소가 이전 및 다음 요소에 대한 참조(포인터)를 가지는 이중 연결 리스트입니다. 배열처럼 고정 크기가 아니므로 동적으로 요소를 추가할 수 있습니다.
- **빠른 삽입과 삭제:** 리스트의 중간에 요소를 삽입하거나 삭제할 때는 참조만 변경하면 되므로 `O(1)` 또는 `O(n)` 시간 복잡도를 가집니다. (삽입/삭제할 위치를 찾는 것이 `O(n)`이고, 찾은 후 삽입/삭제 자체는 `O(1)`
- **느린 조회:** 인덱스에 기반한 조회가 배열처럼 `O(1)`이 아니고, `O(n)`의 시간 복잡도를 가지므로 성능이 떨어집니다.

#### 예제 코드

```java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        // LinkedList 선언
        LinkedList<String> linkedList = new LinkedList<>();

        // 요소 추가
        linkedList.add("Apple");
        linkedList.add("Banana");
        linkedList.add("Orange");

        // 첫 번째 요소에 추가
        linkedList.addFirst("Mango");

        // 마지막 요소 삭제
        linkedList.removeLast(); // Orange 삭제

        // 리스트 출력
        System.out.println("LinkedList elements: " + linkedList);
    }
}
```

**ArrayList**를 사용하는 것이 적합한 경우

- 데이터를 많이 읽고, 순차적으로 추가하는 경우.
- 인덱스를 이용한 빠른 접근이 중요한 경우.

**LinkedList**를 사용하는 것이 적합한 경우

- 중간에서 빈번한 삽입 및 삭제 작업이 필요한 경우.
- 데이터를 한 번에 많이 조회하지 않고, 순차적으로 접근하는 경우.
