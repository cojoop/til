# 백그라운드 허용된 아이템 강제 삭제

맥에서 `App`을 삭제하는 방법은 다양합니다. 보통 `AppCleaner`를 사용하여 깔끔하게 지우는데, 삭제했음에도 불구하고 `설정 > 일반 > 로그인 항목 > 백그라운드에서 허용` 에 남아있는 경우에는 강제로 삭제를 해야 합니다.

&nbsp;

## 로그인한 유저 권한의 파일 확인 및 지우기

`terminal`을 열고 다음 명령어를 입력하면 `finder` 앱이 열립니다.

```bash
open /Library/LaunchAgents
```

> 열린 `finder`앱에서 삭제하고 싶은 아이템에 대한 `.plist` 파일을 지웁니다.

&nbsp;

## 전체 유저 권한의 파일 확인 및 지우기

`terminal`을 열고 다음 명령어를 입력하면 `finder` 앱이 열립니다.

```bash
open /Library/LaunchDaemons
```

> 열린 `finder`앱에서 삭제하고 싶은 아이템에 대한 `.plist` 파일을 지웁니다.
