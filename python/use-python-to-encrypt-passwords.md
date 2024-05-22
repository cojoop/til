# Python을 사용하여 비밀번호 암호화하기

비밀번호를 안전하게 보호하기 위해서는 암호화가 필수적입니다.

&nbsp;

## 해시 함수를 사용한 비밀번호 암호화

해시 함수는 입력값을 고정된 길이의 해시 값으로 변환하는 함수입니다. 파이썬에서는 `hashlib` 모듈을 사용하여 다양한 해시 함수를 제공받을 수 있습니다.
> 가장 일반적으로 사용되는 해시 함수 중 하나는 `SHA-256`입니다.

```python
import hashlib

def encrypt_password(password):
    # 문자열을 UTF-8로 인코딩
    password = password.encode('utf-8')
    # SHA-256 해시 객체 생성
    hash_object = hashlib.sha256()
    # 비밀번호를 해시화
    hash_object.update(password)
    # 해시값 반환
    return hash_object.hexdigest()

# 비밀번호 입력 받기
password = input("비밀번호를 입력하세요: ")
# 비밀번호 암호화
hashed_password = encrypt_password(password)
print("암호화된 비밀번호:", hashed_password)
```

&nbsp;

## 솔트(Salt)를 사용한 보안 강화

단순한 해시 함수만으로는 완전한 보안을 제공할 수 없습니다. `Rainbow table` 공격과 같은 기법으로 해시된 비밀번호를 미리 계산해 두고 이를 비교하는 공격이 가능하기 때문입니다. 이를 방지하기 위해 솔트를 사용합니다.

```python
import hashlib
import os

def encrypt_password(password, salt=None):
    if not salt:
        salt = os.urandom(16) # 무작위 솔트 생성
    # 문자열을 UTF-8로 인코딩
    password = password.encode('utf-8')
    # 솔트와 비밀번호를 결합
    salted_password = salt + password
    # SHA-256 해시 객체 생성
    hash_object = hashlib.sha256()
    # 솔트와 비밀번호를 해시화
    hash_object.update(salted_password)
    # 솔트와 해시값 반환
    return salt, hash_object.hexdigest()

# 비밀번호 입력 받기
password = input("비밀번호를 입력하세요: ")
# 비밀번호 암호화
salt, hashed_password = encrypt_password(password)
print("솔트:", salt)
print("암호화된 비밀번호:", hashed_password)
```
