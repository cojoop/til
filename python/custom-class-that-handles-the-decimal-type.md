# Decimal 타입을 처리하는 사용자 정의 클래스

이 클래스는 `json.JSONEncoder` 클래스를 상속하며, `default` 메서드를 오버라이드하여 `JSON` 인코딩 시에 `decimal.Decimal` 객체를 처리합니다.

```py
class DecimalEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, decimal.Decimal):
            return float(obj)
        return super().default(obj)
```

- `default` 메서드는 객체를 `JSON`으로 직렬화할 때 호출되는데, 여기서는 주어진 객체가 `decimal.Decimal`의 인스턴스인지 확인합니다.
- Decimal 객체가 아닌 다른 타입의 객체가 주어지면, `super().default(obj)`를 호출하여 기본 인코딩 방식을 따릅니다.
