# Typing 모듈과 Type Hinting

`Python 3.5`부터는 타입 힌트(`Type Hint`)를 지원하여 코드에 타입 정보를 추가할 수 있게 되었고, `typing` 모듈을 통해 `Type Hinting`을 좀 더 효율적으로 사용할 수 있습니다.

&nbsp;

## Type Hinting

타입 힌트는 변수, 함수 매개변수, 반환 값 등에 대한 타입 정보를 주석으로 명시하는 방법입니다. 이를 통해 코드의 가독성을 높이고, 버그를 사전에 방지할 수 있습니다.

```py
# 타입 힌트 예제
def greet(name: str) -> str:
    return 'Hello, ' + name

print(greet('John'))  # Hello, John
```

- 위의 예제에서 `name` 매개변수와 함수의 반환 값이 문자열(`str`)임을 명시하고 있습니다.

&nbsp;

## typing 모듈

`typing` 모듈은 타입 힌트를 지원하기 위한 여러 유용한 클래스와 함수를 제공합니다.
&nbsp;

### 기본 타입 힌트

`typing` 모듈을 사용하여 다양한 기본적인 타입 힌트를 지정할 수 있습니다.

#### 1. List

```py
from typing import List

def process_data(data: List[int]) -> List[int]:
    # 리스트 내의 모든 요소를 두 배로 만듭니다.
    return [2 * x for x in data]
```

&nbsp;

#### 2. Tuple

```py
from typing import Tuple

def pair_values(x: int, y: int) -> Tuple[int, int]:
    return x, y
```

&nbsp;

#### 3. Dict

```py
from typing import Dict

def process_data(data: Dict[str, int]) -> Dict[str, int]:
    # 모든 값에 2를 더합니다.
    return {key: value + 2 for key, value in data.items()}
```

&nbsp;

#### 4. Set

```py
from typing import Set

def unique_elements(data: Set[int]) -> Set[int]:
    return data
```

&nbsp;

#### 5. Iterable

```py
from typing import Iterable

def process_data(data: Iterable[int]) -> List[int]:
    # Iterable에서 리스트로 변환하여 반환합니다.
    return list(data)
```

&nbsp;

### Callable 타입

`Callable` 타입은 함수나 메소드를 나타냅니다. `Callable[..., ...]` 형태로 사용되며, 첫 번째 `...`은 함수의 매개변수를, 두 번째 `...`는 반환 값의 타입을 나타냅니다.

```py
from typing import Callable

def apply_function(func: Callable[[int, int], int], x: int, y: int) -> int:
    return func(x, y)

def add(x: int, y: int) -> int:
    return x + y

def subtract(x: int, y: int) -> int:
    return x - y

result1 = apply_function(add, 5, 3)  # 5 + 3 = 8
result2 = apply_function(subtract, 5, 3)  # 5 - 3 = 2
```

- `apply_function` 함수는 `Callable` 타입을 사용하여 함수를 매개변수로 받습니다.
- 주어진 두 개의 숫자와 함수를 적용하여 결과를 반환합니다.
&nbsp;

### 유니온(Union) 및 옵셔널(Optional) 타입

`Union`과 `Optional`을 사용하여 여러 타입 중 하나를 나타내거나, 옵셔널한 값을 표현할 수 있습니다.

```py
from typing import Union, Optional

def square_or_none(number: Union[int, float]) -> Optional[Union[int, float]]:
    if isinstance(number, (int, float)):
        return number ** 2
    else:
        return None
```

- 정수 또는 부동소수점 숫자를 받아서 해당 숫자의 제곱을 반환하거나, 입력이 유효하지 않을 경우 `None`을 반환합니다.
&nbsp;

### 제네릭(Generic) 타입

제네릭을 사용하여 함수나 클래스가 여러 타입을 지원하도록 할 수 있습니다.

```py
from typing import TypeVar, Iterable

T = TypeVar('T')

def first_item(items: Iterable[T]) -> T:
    return next(iter(items))
```

- 모든 `Iterable` 타입에서 첫 번째 아이템을 반환합니다.
&nbsp;

> 타입 힌트를 적극적으로 활용하여 코드를 작성하면 가독성과 안정성을 높일 수 있습니다. 이는 특히 대규모 프로젝트에서 협업과 유지 보수를 용이하게 만들어줍니다.
