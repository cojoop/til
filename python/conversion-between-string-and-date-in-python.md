# Python에서 문자열과 날짜 사이의 변환

파이썬에서는 날짜와 시간 정보를 문자열로 표현하고, 이를 날짜 객체로 변환하거나 반대로 날짜 객체를 문자열로 변환해야 하는 경우가 많습니다. 이러한 작업을 수행할 때는 `strptime()` 및 `strftime()` 메서드가 주로 사용됩니다.

&nbsp;

## 문자열을 날짜로 변환하기: strptime( )

`strptime()` 메서드는 문자열을 날짜 객체로 변환하는 데 사용됩니다. 이 메서드는 형식화된 문자열을 해석하여 그에 맞는 날짜 객체를 반환합니다.

```python
from datetime import datetime

date_string = '2024-02-18'
try:
    date_object = datetime.strptime(date_string, '%Y-%m-%d')
    print("날짜 객체:", date_object)
except ValueError as e:
    print("잘못된 형식입니다:", e)
```

- `%Y-%m-%d`는 `연도-월-일`의 형식을 나타냅니다.
- `strptime()` 메서드는 이 형식에 맞게 문자열을 해석하여 날짜 객체를 생성합니다.

&nbsp;

## 날짜를 문자열로 변환하기: strftime( )

`strftime()` 메서드는 날짜 객체를 형식화된 문자열로 변환하는 데 사용됩니다. 이 메서드는 날짜 객체의 각 부분을 포맷 문자열에 따라 문자열로 변환합니다.

```python
from datetime import datetime

date_object = datetime.now()
date_string = date_object.strftime('%Y-%m-%d %H:%M:%S')
print("문자열로 변환된 날짜:", date_string)
```

- `%Y-%m-%d %H:%M:%S`는 `연도-월-일 시:분:초`의 형식을 나타냅니다.
- `strftime()` 메서드는 형식에 맞게 날짜 객체를 문자열로 변환합니다.
