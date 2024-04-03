# Python 프로젝트 관리(with pyenv & poetry)

`Python` 프로젝트를 관리할 때 가상 환경 및 의존성 관리는 매우 중요합니다. 따라서 `Pyenv`와 `Poetry`를 사용하여 `Python` 프로젝트를 효과적으로 관리하려고 합니다.

## Pyenv

`Pyenv`는 여러 버전의 `Python`을 관리하고 각 프로젝트에 필요한 버전을 지정할 수 있도록 도와주는 도구입니다. 이를 통해 각 프로젝트가 필요로 하는 `Python` 버전을 사용할 수 있어 환경 충돌을 방지하고 프로젝트 간 호환성을 유지할 수 있습니다.

##### pyenv & pyenv-virtualenv 설치

```bash
brew install pyenv
brew install pyenv-virtualenv
```

##### 환경변수 설정

```bash
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
export PATH="/opt/homebrew/sbin:$PATH"
```

##### pyenv로 원하는 python-version 설치

```bash
# python-version 확인
pyenv install —list

# 원하는 python-version 설치
pyenv install [python-version]

# 특정 python-version 삭제 (가상환경 삭제)
pyenv uninstall [python-version]

# 설치된 python list 확인
pyenv versions

# 전역에서 사용할 python-version 설정
pyenv global [python-version]

# 현재 디렉토리와 하위 디렉토리에서 사용할 python-version 설정
pyenv local [python-version]
```

##### pyenv-virtualenv으로 가상 환경 생성

```bash
# python-version 지정
pyenv virtualenv (python-version) <environment_name>

# python-version 생략
pyenv virtualenv <environment_name>
```

## Poetry

`Poetry`는 `Python` 패키지 및 의존성 관리를 위한 툴입니다. 프로젝트의 의존성을 관리하고 가상 환경을 관리하는데 편리한 기능을 제공합니다. 또한 `Lock` 파일을 통해 의존성의 정확한 버전을 고정하여 `reproducible`한 환경을 유지할 수 있습니다.

##### poetry 설치

```bash
brew install poetry
```

##### 가상환경 실행된 위치에서 사용할 프로젝트 패키지 관리자(poetry) 생성

```bash
poetry init
```

##### 패키지 설치

```bash
poetry add [package-name]
```

##### 프로젝트 의존성 관리

```bash
# 현재 프로젝트 의존성 고정
poetry update

# 프로젝트 의존성 최신 상태로 업데이트
poetry lock
```

##### 패키지 삭제

```bash
poetry remove [package-name]
```
