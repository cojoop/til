# try-except 구문으로 예외처리하기

예외 처리는 프로그래밍에서 중요한 측면 중 하나입니다. `try-except`는 파이썬에서 예외 처리를 담당하는 구문입니다.

### 기본적인 예외 처리 구문

```python
try:
    # 예외가 발생할 수 있는 코드
    # 예를 들어, 파일 열기, 네트워크 연결 등
except ExceptionType:
    # 예외 처리 코드
    # 예외가 발생했을 때 실행될 내용
else:
    # 예외가 발생하지 않았을 때 실행될 내용
finally:
    # 항상 실행되는 코드 블록
    # 파일 닫기 등의 정리 작업에 유용

```

- `try`: 예외가 발생할 수 있는 코드 블록을 포함합니다.
- `except`: 예외가 발생했을 때 실행될 코드 블록을 정의합니다. 특정한 예외 타입을 명시하여 해당 예외에 대한 처리를 할 수도 있습니다.
- `else`: 예외가 발생하지 않았을 때 실행될 코드를 포함합니다.
- `finally`: 예외 발생 여부와 상관없이 항상 실행되는 코드 블록을 정의합니다.

&nbsp;

### 예시

다음은 파일을 열고 읽는 동작에서 발생할 수 있는 예외를 처리하는 간단한 예시입니다.

```python
try:
    with open('example.txt', 'r') as f:
        content = f.read()
except FileNotFoundError:
    print("파일을 찾을 수 없습니다.")
except PermissionError:
    print("파일에 접근할 권한이 없습니다.")
else:
    print("파일 내용:", content)
finally:
    print("예외 처리 완료")
```

> 이 예시에서는 파일을 열 때 발생할 수 있는 `FileNotFoundError`와 `PermissionError`를 처리합니다. 파일이 존재하지 않거나 접근할 권한이 없는 경우에 대비하여 각각 다른 예외 처리를 제공합니다.
