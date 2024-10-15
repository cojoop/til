# Typing 모듈과 Type Hinting

`Python 3.5`부터는 타입 힌트(`Type Hint`)를 지원하여 코드에 타입 정보를 추가할 수 있게 되었고, `typing` 모듈을 통해 `Type Hinting`을 좀 더 효율적으로 사용할 수 있습니다.

## typing 모듈 소개

typing 모듈은 Python 3.5부터 표준 라이브러리에 추가되었으며, 변수, 함수의 매개변수, 반환값에 대한 타입 정보를 명시적으로 선언할 수 있게 해줍니다.

### 주요 기능

#### 기본 타입 힌팅

```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

#### 컨테이너 타입

```python
from typing import List, Dict, Tuple, Set

numbers: List[int] = [1, 2, 3]
user_info: Dict[str, str] = {"name": "John", "age": "30"}
coordinates: Tuple[int, int] = (10, 20)
unique_chars: Set[str] = {"a", "b", "c"}
```

#### 유니온 타입

```python
from typing import Union

def process_data(data: Union[int, str]) -> str:
    return str(data)
```

#### 옵셔널 타입

```python
from typing import Optional

def find_user(id: int) -> Optional[Dict[str, str]]:
    # 사용자를 찾으면 딕셔너리 반환, 없으면 None 반환
    pass
```

### 이점

**1. 코드 가독성 향상:** 타입 힌트는 코드의 의도를 명확히 전달합니다.
**2. 버그 예방:** 정적 타입 검사 도구를 사용하여 실행 전 타입 관련 오류를 발견할 수 있습니다.
**3. IDE 지원:** 코드 자동 완성 및 리팩토링 기능이 개선됩니다.
**4. 문서화:** 함수의 입력과 출력 타입을 명확히 하여 문서 역할을 합니다.

#### 주의사항

- 타입 힌트는 Python의 동적 타이핑 특성에 영향을 주지 않습니다.
- 실행 시 타입 검사를 하지 않으므로, 런타임 에러를 완전히 방지할 수는 없습니다.

타입 힌팅은 대규모 프로젝트나 복잡한 시스템에서 특히 유용하며, 코드의 품질과 유지보수성을 크게 향상시킵니다.
