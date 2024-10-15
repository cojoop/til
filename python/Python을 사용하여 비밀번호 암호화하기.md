# Python을 사용하여 비밀번호 암호화하기

Python에서 비밀번호를 안전하게 암호화하려면 암호화 해싱(`Hashing`)을 사용하는 것이 일반적입니다.
해싱은 비밀번호를 고정된 길이의 암호화된 문자열로 변환하고, 이를 사용하여 안전하게 저장할 수 있습니다.

### bcrypt를 사용한 비밀번호 해싱

`bcrypt`는 비밀번호 해싱에 특화된 알고리즘으로, 보안성이 높고 사용하기 쉽습니다.

1. bcrypt 라이브러리를 설치

```bash
pip install bcrypt
```

2. 비밀번호 해싱 및 검증

```python
import bcrypt

# 비밀번호 해싱
def hash_password(password: str) -> bytes:
    # 비밀번호는 bytes 형식으로 변환
    password_bytes = password.encode('utf-8')
    # bcrypt에서 솔트와 해시를 생성
    salt = bcrypt.gensalt()
    hashed_password = bcrypt.hashpw(password_bytes, salt)
    return hashed_password

# 비밀번호 검증
def check_password(password: str, hashed_password: bytes) -> bool:
    # 입력받은 비밀번호를 해싱된 비밀번호와 비교
    return bcrypt.checkpw(password.encode('utf-8'), hashed_password)

# 사용 예시
password = "my_secure_password"
hashed_pw = hash_password(password)
print(f"Hashed password: {hashed_pw}")

# 비밀번호 검증
is_valid = check_password("my_secure_password", hashed_pw)
print(f"Password is valid: {is_valid}")
```

- `hashpw()` 함수는 주어진 비밀번호와 솔트를 사용해 해시를 생성합니다.
- `gensalt()` 함수는 솔트를 생성하는데, 이는 해시가 항상 다른 값을 갖도록 보장합니다.
- `checkpw()` 함수는 해시된 비밀번호와 입력한 비밀번호가 일치하는지 확인합니다.

### hashlib를 사용한 비밀번호 해싱

`hashlib`은 Python의 표준 라이브러리로, 다양한 해싱 알고리즘을 제공합니다.
하지만, `hashlib`만으로는 솔트 생성이나 시간 복잡도 조정 기능이 없기 때문에 직접 솔트를 생성해야 하고, 보안이 `bcrypt`만큼 강력하지는 않습니다.

1. 비밀번호 해싱

```python
import hashlib
import os

# 비밀번호 해싱
def hash_password(password: str, salt: bytes = None) -> str:
    if not salt:
        salt = os.urandom(16)  # 랜덤 솔트 생성
    password_bytes = password.encode('utf-8')
    hashed_password = hashlib.pbkdf2_hmac('sha256', password_bytes, salt, 100000)
    return salt.hex() + hashed_password.hex()  # 솔트와 해시 결합 후 반환

# 비밀번호 검증
def check_password(password: str, hashed_password: str) -> bool:
    salt = bytes.fromhex(hashed_password[:32])  # 첫 32자리를 솔트로 분리
    stored_password_hash = hashed_password[32:]
    new_password_hash = hash_password(password, salt)[32:]
    return new_password_hash == stored_password_hash

# 사용 예시
password = "my_secure_password"
hashed_pw = hash_password(password)
print(f"Hashed password: {hashed_pw}")

# 비밀번호 검증
is_valid = check_password("my_secure_password", hashed_pw)
print(f"Password is valid: {is_valid}")
```

- `os.urandom(16)`은 16바이트 길이의 랜덤 솔트를 생성합니다.
- `pbkdf2_hmac()`은 hashlib에서 제공하는 함수로, 반복적인 해싱을 통해 더 안전한 해시를 생성합니다. 여기서는 100,000번 반복합니다.
- 해시된 비밀번호에 솔트를 포함시켜 검증 시에도 동일한 솔트로 해싱 과정을 반복해 비교합니다.
