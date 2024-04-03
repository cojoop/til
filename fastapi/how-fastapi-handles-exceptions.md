# FastAPI 예외 처리하는 방법

`FastAPI`는 예외를 처리하기 위한 다양한 방법을 제공합니다.

## 기본적인 예외 처리

`FastAPI`에서는 기본적으로 `Python`의 `try-except` 구문을 사용하여 예외를 처리할 수 있습니다.

```py
from fastapi import FastAPI, HTTPException

app = FastAPI()

@app.get("/")
async def read_root():
    try:
        # 예외 발생 가능한 코드
        pass
    except Exception as e:
        # 예외 처리
        pass
```

## HTTPException 활용

`FastAPI`는 `HTTP` 예외를 처리하기 위한 `HTTPException` 클래스를 제공합니다. 이를 사용하면 클라이언트에게 적절한 `HTTP` 상태 코드와 메시지를 반환할 수 있습니다.

```py
from fastapi import FastAPI, HTTPException

app = FastAPI()

@app.get("/")
async def read_item(item_id: int):
    if item_id != 1:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item_id": item_id}
```

## 커스텀 예외 처리

`FastAPI`는 프로젝트에 특화된 예외 처리가 필요한 상황을 위해 커스텀 예외를 정의하고 처리할 수 있도록 지원합니다.

```py
from fastapi import FastAPI, HTTPException

class MyCustomException(Exception):
    def __init__(self, detail: str):
        self.detail = detail

app = FastAPI()

@app.get("/")
async def read_root():
    try:
        # 예외 발생 가능한 코드
        pass
    except MyCustomException as e:
        raise HTTPException(status_code=400, detail=e.detail)
```

## 예외 핸들러 사용

`FastAPI`는 예외를 전역적으로 처리할 수 있는 예외 핸들러를 제공합니다. 이를 통해 모든 뷰 함수에서 발생한 예외를 일관되게 처리할 수 있습니다.

```py
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse

app = FastAPI()

@app.exception_handler(MyCustomException)
async def custom_exception_handler(request: Request, exc: MyCustomException):
    return JSONResponse(
        status_code=400,
        content={"message": exc.detail}
    )
```
