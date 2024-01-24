## Mac에서 비밀번호 없이 ssh 원격접속하기

서버에 접속할 때는 다음 커맨드를 입력하여 접속해야 합니다.

```bash
ssh user@host(domain|ip_address) -i identity_file -p portnumber
```

- **user:** 원격 서버에 접속할 때 사용할 사용자 이름입니다.
- **host:** 원격 서버의 도메인 이름 또는 IP 주소입니다. `ex) 128.XXX.XX.XX, example.net`
- **-i:** 사용할 SSH 개인 키 파일의 경로를 나타냅니다.
- **-p:** 원격 서버에 접속할 때 사용할 포트 번호를 지정합니다. 기본값은 22이며, 명시적으로 다른 포트를 사용하고자 할 때 이 옵션을 사용합니다.

&nbsp;

매우 불편하기 때문에 `ssh 접속명`과 같은 커맨드만으로도 `ssh` 접속이 되도록 설정하는 방법에 대해 설명하고자 합니다

> - 접속 정보(호스트명, 유저명, 포트 번호)를 알고 있어야 합니다.
> - SSH 비밀 키를 가지고 있어야 합니다.

&nbsp;

### ~/.ssh 디렉토리 생성

```bash
# 디렉토리 생성하기(이미 있다면 skip)
$ mkdir ~/.ssh

# 소유자에 읽기, 쓰기, 실행 권한 부여
$ chmod 700 ~/.ssh
```

&nbsp;

### 비밀 키 파일 이동

```bash
# ~/.ssh 디렉토리로 파일이동
$ mv 현재_비밀키_경로 ~/.ssh/비밀키_파일명

# 소유자에게 읽기 권한 부여
$ chmod 400 ~/.ssh/비밀키 파일명
```

&nbsp;

### ~/.ssh/config 파일 생성

```bash
# config 파일 편집
$ vi ~/.ssh/config
```

```bash
# config 파일의 내용
Host 접속명(자유)
  HostName 호스트명
  User 유저명
  IdentityFile ~/.ssh/비밀키_파일명
  Port 포트번호
  TCPKeepAlive yes
  IdentitiesOnly yes
```

```bash
# 파일 권한 변경 (읽기, 쓰기 권한)
$ chmod 600 ~/.ssh/config
```

&nbsp;

### 서버 접속 확인

```bash
ssh 접속명
```

> 파일이나 디렉토리의 소유자나 권한이 틀렸거나, `config` 파일의 설정내용에 틀리면 접속이 안될 수 있습니다.
