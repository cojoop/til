# Django 모델 메서드와 메타클래스

`Django`에서 모델을 정의할 때, 모델의 동작을 제어하고 데이터를 다루는 데 도움이 되는 메타데이터와 메소드를 활용할 수 있습니다.
`Django`의 모델은 데이터베이스 스키마를 정의하고 데이터를 관리하는 핵심적인 요소입니다.

## 1. 메타데이터(Metadata)

`Django` 모델에서 메타데이터는 모델 자체의 특성을 정의하고 제어하는 데 사용됩니다.

#### 주요 메타 데이터

##### ordering

`ordering` 속성은 모델의 기본 레코드 순서를 제어합니다. 이것은 주로 쿼리 결과의 정렬을 위해 사용됩니다.

```py
class Book(models.Model):
    title = models.CharField(max_length=100)
    pubdate = models.DateField()

    class Meta:
        ordering = ['title', '-pubdate']
```

- 책들이 제목의 알파벳 순서대로 먼저 정렬되고, 그 후에는 발행일(pubdate)을 최신부터 오래된 순서대로 정렬됩니다.

##### verbose_name

`verbose_name`은 모델을 나타내는 보다 자세한 이름을 정의합니다.

```py
class BetterName(models.Model):
    # fields 정의

    class Meta:
        verbose_name = 'Better Name'
```

- 모델을 표현하는 데 더 명확한 이름인 'Better Name'을 정의합니다.

> **다른 메타데이터 옵션**
> 모델의 메타데이터에는 다른 옵션들도 있으며, 데이터베이스 매핑이나 저장 방식을 제어하는 데 사용됩니다.

## 메소드(Methods)

모델은 메소드를 통해 특정 동작을 정의할 수 있습니다.

#### 주요 메소드

##### \_\_str__( )

`__str__()` 메소드는 모델 인스턴스를 문자열로 표현할 때 사용됩니다. 주로 관리자 사이트나 템플릿에서 인스턴스를 표시할 때 활용됩니다.

```py
class Book(models.Model):
    title = models.CharField(max_length=100)

    def __str__(self):
        return self.title
```

- 책 인스턴스를 표현하는 문자열로 제목을 반환합니다.

##### get_absolute_url( )

`get_absolute_url()` 메소드는 모델 인스턴스의 절대 URL을 반환합니다. 주로 웹 페이지에서 개별 레코드를 보여줄 때 사용됩니다.

```py
from django.urls import reverse

class Book(models.Model):
    title = models.CharField(max_length=100)

    def get_absolute_url(self):
        return reverse('book-detail', args=[str(self.id)])
```

- 책 인스턴스의 절대 `URL`을 생성하여 반환합니다.

> `Django`의 모델 메타데이터와 메소드를 활용하면 데이터베이스 모델을 더욱 효율적으로 관리하고 활용할 수 있습니다.
