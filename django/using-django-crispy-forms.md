# django-crispy-forms 사용하기

`django-crispy-forms`는 `Django` 웹 애플리케이션에서 `HTML` 폼을 보다 쉽게 관리할 수 있도록 도와주는 패키지입니다. 이 패키지를 사용하면 폼을 더 간단하게 만들고, 폼 필드를 배치하고, 폼을 스타일링할 수 있습니다.

### 설치

- `django-crispy-forms` 패키지 설치

```bash
poetry add django-crispy-forms
```

- `Bootstrap 5`를 사용하여 `django-crispy-forms`를 스타일링하는 데 도움이 되는 패키지 설치

```bash
poetry add crispy-bootstrap5    
```

### settings.py에 추가

`settings.py` 파일에 다음과 같이 `crispy_forms` 앱을 추가합니다.

```py
INSTALLED_APPS = [
    ...
    'crispy_forms',
    "crispy_bootstrap5",
    ...
]
```

### 템플릿 설정

`settings.py` 파일에 다음과 같이 `crispy_forms`의 템플릿 팩을 설정합니다:

```py
CRISPY_ALLOWED_TEMPLATE_PACKS = "bootstrap5"
CRISPY_TEMPLATE_PACK = "bootstrap5"
```

### Form 클래스에 적용

사용하려는 `Form` 클래스에 `crispy-forms`를 적용합니다. 이를 위해 해당 폼 클래스의 `forms.py` 파일을 열고 다음과 같이 `crispy-forms`의 `Form` 클래스를 상속받습니다.

```py
from crispy_forms.helper import FormHelper
from crispy_forms.layout import Layout, Submit
from django import forms

class MyForm(forms.Form):
    # 폼 필드 정의
    
    def __init__(self, *args, **kwargs):
        super(MyForm, self).__init__(*args, **kwargs)
        self.helper = FormHelper()
        self.helper.layout = Layout(
            # 필드 배치 및 추가적인 레이아웃 정의
            Submit('submit', 'Submit', css_class='btn-primary')
        )
```

### HTML 템플릿에서 폼 렌더링

마지막으로, `Form`을 `HTML` 템플릿에서 렌더링합니다. 이를 위해 템플릿 파일에서 폼 객체를 다음과 같이 렌더링합니다.

```py
{% load crispy_forms_tags %}
<form method="post" class="form">
    {% crispy form %}
</form>
```

- form은 Django 뷰에서 템플릿으로 전달된 폼 객체를 나타냅니다.
