# Depends를 활용한 종속성 관리

`FastAPI`의 `Depends`는 특히 유용한 기능 중 하나입니다. `Depends`를 사용하면 함수에 필요한 종속성을 쉽게 관리하고 조작할 수 있습니다.

`Depends`는 엔드포인트의 함수가 실행되기 전에 특정 조건을 만족해야 하는 경우를 처리할 수 있습니다.

## 사용 방법

```py
from fastapi import Depends, FastAPI

app = FastAPI()

# 예제 의존성 함수
def get_db():
    # 데이터베이스 연결 로직
    return db

# 의존성을 사용하는 엔드포인트
@app.get("/")
async def read_item(db: DB = Depends(get_db)):
    # db를 사용한 로직
    return {"message": "Hello World"}
```

- `get_db` 함수는 데이터베이스에 대한 연결을 설정하고 반환합니다.
- `Depends`를 사용하여 `read_item` 함수에 이 의존성을 주입합니다.

> `FastAPI`는 이 함수를 호출하여 필요한 의존성을 자동으로 관리합니다.

## 의존성 체인

`Depends`는 체인으로 연결될 수 있습니다. 이는 여러 종속성을 함께 사용하고 각각을 순서대로 실행할 수 있다는 것을 의미합니다.
> 예를 들어, 인증 및 권한 확인을 위해 두 개의 의존성 함수를 연결할 수 있습니다.

```py
from fastapi import Depends, FastAPI, HTTPException

app = FastAPI()

# 예제 의존성 함수
async def get_token_header(x_token: str = Depends(get_token)):
    if x_token != "fake-super-secret-token":
        raise HTTPException(status_code=400, detail="X-Token header invalid")

async def get_query_token(token: str):
    if token != "fake-super-secret-token":
        raise HTTPException(status_code=400, detail="No permission")
    return token

# 의존성을 사용하는 엔드포인트
@app.get("/")
async def read_item(token: str = Depends(get_query_token)):
    return {"token": token}
```
