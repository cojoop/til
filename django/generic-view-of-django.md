# Django의 제네릭 뷰(Generic View)

제네릭 뷰(`Generic View`)는 `Django` 프레임워크에서 제공하는 편리한 기능으로, 반복적인 작업을 최소화하고 재사용 가능한 뷰를 쉽게 작성할 수 있도록 도와줍니다. 제네릭 뷰를 사용하면 데이터베이스 모델의 `CRUD(Create, Read, Update, Delete)` 기능을 빠르게 구현할 수 있으며, 코드의 재사용성과 유지보수성을 향상시킬 수 있습니다.

## 대표적인 제네릭 뷰(`Generic View`) 클래스

### ListView

`ListView`는 데이터베이스 모델의 여러 개의 레코드를 보여주는 뷰입니다. 대표적으로 블로그 글 목록이나 제품 목록을 표시하는 데 사용됩니다.

```py
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'blog/post_list.html'  # 템플릿 파일의 경로를 지정해줍니다.
    context_object_name = 'posts'  # 템플릿에서 사용할 변수 이름을 지정해줍니다.
    ordering = ['-date_posted']  # 글을 최신순으로 정렬합니다.
    paginate_by = 10  # 페이지네이션을 사용하여 페이지당 10개의 글을 보여줍니다.

```

### DetailView

`DetailView`는 단일 데이터베이스 레코드의 상세 정보를 보여주는 뷰입니다. 예를 들어, 개별 블로그 글이나 제품의 세부 정보를 표시하는 데 사용됩니다.

```py
from django.views.generic import DetailView
from .models import Post

class PostDetailView(DetailView):
    model = Post
    template_name = 'blog/post_detail.html'  # 템플릿 파일의 경로를 지정해줍니다.
    context_object_name = 'post'  # 템플릿에서 사용할 변수 이름을 지정해줍니다.
```

### CreateView

`CreateView`는 새로운 데이터베이스 레코드를 생성하는 뷰입니다. 사용자로부터 입력을 받아 데이터를 저장하는 데 사용됩니다.

```py
from django.views.generic import CreateView
from .models import Post
from .forms import PostForm

class PostCreateView(CreateView):
    model = Post
    form_class = PostForm
    template_name = 'blog/post_form.html'  # 템플릿 파일의 경로를 지정해줍니다.
    success_url = '/'  # 데이터 저장 후 이동할 URL을 지정해줍니다.
```

### UpdateView

`UpdateView`는 기존 데이터베이스 레코드를 업데이트하는 뷰입니다. 기존 데이터의 수정이 필요한 경우 사용됩니다.

```py
from django.views.generic import UpdateView
from .models import Post
from .forms import PostForm

class PostUpdateView(UpdateView):
    model = Post
    form_class = PostForm
    template_name = 'blog/post_form.html'  # 템플릿 파일의 경로를 지정해줍니다.
    success_url = '/'  # 데이터 업데이트 후 이동할 URL을 지정해줍니다.
```

### DeleteView

`DeleteView`는 데이터베이스 레코드를 삭제하는 뷰입니다. 주의를 기울여 사용하여 데이터의 손실을 방지해야 합니다.

```py
from django.views.generic import DeleteView
from django.urls import reverse_lazy
from .models import Post

class PostDeleteView(DeleteView):
    model = Post
    template_name = 'blog/post_confirm_delete.html'  # 삭제 확인을 위한 템플릿 파일의 경로를 지정해줍니다.
    success_url = reverse_lazy('post-list')  # 데이터 삭제 후 이동할 URL을 지정해줍니다.
```
