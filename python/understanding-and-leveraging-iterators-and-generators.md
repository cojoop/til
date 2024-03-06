# 이터레이터(Iterators)와 제네레이터(Generators)의 이해와 활용

`Python`은 이터레이터와 제네레이터 같은 고급 기능을 제공하여 데이터를 효율적으로 처리하고 메모리를 효율적으로 활용할 수 있습니다.

&nbsp;

## 이터레이터(Iterators)

`Iterators`는 컬렉션, 리스트, 튜플 등의 요소를 반복적으로 탐색하는 데 사용됩니다. `Iterators`를 사용하면 메모리를 효율적으로 사용할 수 있고, 대용량 데이터에 대한 반복 작업을 수행할 때 유용합니다.

#### 이터레이터의 특징

- 값을 순차적으로 탐색하는 데 사용됨
- `iter()`와 `next()` 함수를 사용하여 다음 값을 가져옴
- 모든 요소를 한 번에 메모리에 로드하지 않고 필요할 때마다 요소를 생성하여 메모리를 절약함

**예제 코드**

```py
class MyIterator:
    def __init__(self, data):
        self.data = data
        self.index = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.index >= len(self.data):
            raise StopIteration
        value = self.data[self.index]
        self.index += 1
        return value

# 이터레이터 사용 예시
my_iter = MyIterator([1, 2, 3, 4, 5])
for num in my_iter:
    print(num)
```

&nbsp;

## 제네레이터(Generators)

`Generators`는 `Iterators`를 만드는 간편한 방법 중 하나입니다. `Generators`는 함수 내에서 `yield` 키워드를 사용하여 값을 반환하고 호출자에게 제어를 반환합니다. 이를 통해 함수의 실행 상태를 유지하고 나중에 필요할 때 값을 계산할 수 있습니다.

#### 제네레이터의 특징

- 함수 내에서 `yield` 키워드를 사용하여 값을 반환
- 호출자에게 값을 한 번에 하나씩 반환
- 함수의 상태를 유지하고 계산을 재개할 수 있음

**예제 코드**

```py
def my_generator(data):
    for item in data:
        yield item

# 제네레이터 사용 예시
gen = my_generator([1, 2, 3, 4, 5])
for num in gen:
    print(num)
```

&nbsp;

### 차이점

- `Iterators`는 클래스를 사용하여 직접 구현하고, `iter()`와 `next()` 메서드를 정의해야 합니다. 반면에 `Generators`는 함수 내에서 `yield` 키워드를 사용하여 간단하게 구현할 수 있습니다.
- `Iterators`는 상태를 명시적으로 유지하고, `Generators`는 함수의 실행 상태를 유지합니다.

### 활용

- `Iterators`는 복잡한 반복 작업을 수행할 때 사용됩니다. 대용량 데이터나 복잡한 알고리즘을 구현할 때 유용합니다.
- `Generators`는 간단한 반복 작업이나 데이터 스트림을 처리할 때 유용합니다. 또한 무한한 시퀀스를 생성할 때  `Generators`를 사용할 수 있습니다.
