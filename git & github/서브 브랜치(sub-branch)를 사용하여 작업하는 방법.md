# 서브 브랜치(sub-branch)를 사용하여 작업하는 방법

서브 브랜치(`sub-branch`)를 사용하는 것은 여러 개발자가 동시에 작업하고 코드를 통합할 때 특히 유용합니다.
`sub-branch`를 사용하면 메인 브랜치에서 독립적으로 작업하고 변경 사항을 테스트할 수 있습니다.

### 서브 브랜치 생성 및 전환

1. 메인 브랜치(보통 develop)에서 새로운 서브 브랜치를 생성합니다.

```bash
git checkout -b feature/new-feature develop
```

- 이 명령어는 `develop` 브랜치를 기반으로 `feature/new-feature`라는 새 브랜치를 만들고 그 브랜치로 전환합니다.

### 작업 수행

2. 새로 만든 서브 브랜치에서 필요한 작업을 수행합니다.
3. 작업한 내용을 커밋합니다.

```bash
git add .
git commit -m "Add new feature"
```

### 변경사항 동기화

4. 작업 중 메인 브랜치(`develop`)에 변경사항이 있다면 다음과 같이 동기화합니다.

```bash
git checkout develop
git pull
git checkout feature/new-feature
git rebase develop
```

- 이렇게 하면 최신 `develop` 브랜치의 변경사항을 서브 브랜치에 적용할 수 있습니다.

### 작업 완료 및 병합 요청

5. 작업이 완료되면 원격 저장소에 서브 브랜치를 푸시합니다.

```bash
git push -u origin feature/new-feature
```

6. `GitHub`나 `GitLab` 등의 플랫폼에서 `Pull Request` 또는 `Merge Request`를 생성하여 코드 리뷰를 요청합니다.
7. 코드 리뷰가 완료되고 승인되면, 서브 브랜치의 변경사항이 메인 브랜치(`develop`)에 병합됩니다.

### 정리

8. 병합이 완료된 후에는 로컬과 원격의 서브 브랜치를 삭제합니다.

```bash
git checkout develop
git branch -d feature/new-feature
git push origin --delete feature/new-feature
```

이러한 방식으로 서브 브랜치를 사용하면 메인 코드베이스에 영향을 주지 않고 독립적으로 새로운 기능을 개발할 수 있으며, 코드 리뷰와 품질 관리가 용이해집니다.
