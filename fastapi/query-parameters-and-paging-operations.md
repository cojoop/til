# 쿼리 파라미터 및 페이징 처리

`FastAPI`에서 자주 사용되는 쿼리 파라미터(`Query Parameter`)와 페이징 처리를 구현하는 방법에 대해 알아보려 합니다.
&nbsp;

## 쿼리 파라미터(Query Parameters)

쿼리 파라미터는 클라이언트가 서버로 전달하는 데이터입니다. 주로 `API` 엔드포인트에 필요한 필터링, 정렬, 검색 등의 기능을 구현할 때 사용됩니다.

```py
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/")
async def read_items(q: str = None):
    return {"q": q}
```

- `/items/` 엔드포인트로 `GET` 요청이 오면 `q`라는 쿼리 파라미터를 받아서 반환합니다.
- 만약 요청에 `?q=fastapi`와 같이 쿼리 파라미터가 전달되면 해당 값을 반환합니다.
&nbsp;

## 페이징 처리(Pagination)

대용량의 데이터를 다루는 `API`에서는 페이징 처리가 필수적입니다. 클라이언트는 특정 범위의 데이터만 요청하고, 서버는 해당 범위의 데이터만 반환합니다.

```py
from fastapi import FastAPI

app = FastAPI()

# 가상의 데이터베이스
fake_items_db = [{"item_name": f"Item {i}"} for i in range(100)]

@app.get("/items/")
async def read_items(skip: int = 0, limit: int = 10):
    return fake_items_db[skip : skip + limit]
```

- `/items/` 엔드포인트로 `GET` 요청이 오면 `skip`과 `limit`이라는 두 개의 쿼리 파라미터를 받아서 데이터를 반환합니다.
- `skip`은 건너뛸 항목의 수를, `limit`은 반환할 항목의 수를 나타냅니다.
&nbsp;

## 추가적인 쿼리 파라미터

특정 상황에서만 데이터를 반환하는 경우에는 추가적인 쿼리 파라미터를 사용해야 할 수 있습니다.

```py
from fastapi import FastAPI

app = FastAPI()

# 가짜 데이터베이스
fake_items_db = [{"item_id": "item1"}, {"item_id": "item2"}, {"item_id": "item3"}]


@app.get("/items/")
async def read_items(skip: int = 0, limit: int = 10, needy: str = None):
    if needy == "yes":
        return fake_items_db[skip : skip + limit]
    else:
        return {"error": "You are not needy!"}
```

- `needy`라는 추가적인 쿼리 파라미터를 사용하여 클라이언트는 특정 조건을 만족할 때만 데이터를 요청할 수 있습니다.
