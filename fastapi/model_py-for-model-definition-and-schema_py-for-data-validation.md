# 모델 정의를 위한 model.py, 데이터 유효성 검사를 위한 schema.py

`FastAPI`를 사용하여 데이터 모델을 정의하고 API를 개발할 때, `model.py`와 `schema.py`를 함께 사용하는 것이 효율적인 방법입니다.

## model.py

`model.py` 파일은 데이터베이스의 테이블을 정의하는 데 사용됩니다. 이 파일에서는 보통 `ORM(Object-Relational Mapping)` 라이브러리인 `SQLAlchemy`를 사용하여 데이터베이스 모델을 정의합니다. 데이터베이스의 스키마를 표현하고 데이터베이스와의 상호 작용을 담당합니다.

```py
# model.py
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True, index=True)
    username = Column(String, unique=True, index=True)
    email = Column(String, unique=True, index=True)
```

## schema.py

`schema.py` 파일은 데이터 유효성 검사를 위해 사용됩니다. 여기서는 `Pydantic`을 사용하여 데이터 스키마를 정의하고, `FastAPI`에서 요청 및 응답 데이터의 유효성을 검사하는 데 활용됩니다. 또한 자동으로 생성되는 API 문서의 스키마를 제공하기도 합니다.

```py
# schema.py
from pydantic import BaseModel

class UserBase(BaseModel):
    username: str
    email: str

class UserCreate(UserBase):
    password: str

class User(UserBase):
    id: int

    class Config:
        orm_mode = True
```

## 사용 방법과 이유

**1. 분리된 역할:** `model.py`는 데이터베이스와 관련된 로직을 담당하고, `schema.py`는 데이터 유효성 검사와 API 문서 생성을 담당하여 역할이 명확하게 분리됩니다.

**2. 재사용성 및 유연성:** 데이터 모델과 API 요청/응답 스키마가 분리되어 있으므로, 필요에 따라 서로 다른 형식으로 데이터를 사용할 수 있습니다.

**3. 가독성 및 유지보수성:** 코드의 가독성을 높이고 유지보수를 용이하게 합니다. 각각의 파일은 특정한 역할을 수행하므로 코드베이스가 더욱 구조화되고 관리하기 쉬워집니다.

**4. 자동 문서 생성:** `Pydantic` 모델은 `FastAPI`에 의해 자동으로 문서화되므로, API의 이해도를 높이고 개발 생산성을 향상시킵니다.

> 따라서 `FastAPI` 프로젝트에서는 `model.py`를 사용하여 데이터베이스 모델을 정의하고, `schema.py`를 사용하여 데이터 유효성을 검사하고 API 문서를 생성하는 것은 좋은 방법이니다.
