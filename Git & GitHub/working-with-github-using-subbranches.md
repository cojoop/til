# GitHub에서 sub-branch를 사용하여 작업하기

`GitHub`에서 작업할 때 서브 브랜치(`sub-branch`)를 사용하는 것은 여러 개발자가 동시에 작업하고 코드를 통합할 때 특히 유용합니다. `sub-branch`를 사용하면 메인 브랜치에서 독립적으로 작업하고 변경 사항을 테스트할 수 있습니다.

### 새로운 sub-branch 생성하기

```bash
# 현재 branch에서 새로운 sub-branch 생성
git checkout -b sub-branch-name
# 또는
git branch sub-branch-name
git checkout sub-branch-name
```

#### 원격 저장소에 반영하기

```bash
# 새로 생성한 sub-branch를 원격 저장소에 푸시
git push origin sub-branch-name
```

<br>

### sub-branch에서 작업하기

```bash
# 새로 생성한 sub-branch로 이동
git checkout sub-branch-name
```

- 이제 `sub-branch`에서 변경 사항을 추가하고 커밋할 수 있습니다.

<br>

### 변경 사항을 원격 저장소에 push하기

```bash
# 변경사항을 추가
git add .
# 커밋
git commit -m "내용을 입력하세요"
# 서브브랜치의 변경 사항을 원격 저장소에 push
git push origin sub-branch-name
```

<br>

### 변경 사항을 메인 branch에 병합하기

- `Pull Request (PR)` 생성
`GitHub` 웹 인터페이스에서 원격 저장소로 이동하여 `Pull Requests` 탭을 선택하고 `New Pull Request` 버튼을 클릭합니다. 비교할 브랜치를 선택하고 `PR`을 생성합니다.

- 코드 리뷰
동료 개발자들이 변경 사항을 리뷰하고 의견을 추가합니다.

- 병합(`Merge`)
리뷰가 완료되면 `Merge Pull Request` 버튼을 클릭하여 서브브랜치의 변경 사항을 메인 브랜치로 병합합니다.

- 삭제(`Optional`):
`PR`이 병합되면 로컬에서는 해당 `sub-branch`를 삭제할 수 있습니다.

    ```bash
    git branch -d sub-branch-name
    ```
