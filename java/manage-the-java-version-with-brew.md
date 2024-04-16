# Brew를 사용하여 Java 버전 관리하기

`macOS` 환경에서 `brew`를 사용하면 자바를 손쉽게 설치할 수 있고 더불어 다양한 자바 버전을 필요할 때마다 변경해서 사용할 수 있습니다.

## Java 설치하기

#### Homebrew 설치 및 업데이트

```bash
brew update
```

#### adoptopenjdk/openjdk 추가

```bash
brew tap adoptopenjdk/openjdk
```

#### 설치 가능한 모든 JDK 찾기

```bash
brew search jdk
```

#### 원하는 Java 버전 설치

```bash
# java jdk 11 버전 설치
brew install openjdk@11

# java jdk 17 버전 설치
brew install openjdk@17
```

#### Java 설치 경로 확인

```bash
/usr/libexec/java_home -V
```

#### 환경변수 설정

위 `Java` 경로를 `~/.zshrc` 파일에 환경변수 추가

```bash
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-17.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```

변경사항 적용

```bash
source ~/.zshrc
```

## Java 버전 변경

`Java` 버전이 여러 개 설치된 경우, 원하는 버전을 선택하여 환경 변수를 설정합니다.

```bash
# Java 11 경로
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH

# Java 17 경로
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-17.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```

#### Java 11을 사용할 경우

```bash
# Java 11 경로
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH

# Java 17 경로
# export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-17.jdk/Contents/Home
# export PATH=$JAVA_HOME/bin:$PATH
```

#### Java 17을 사용할 경우

```bash
# Java 11 경로
# export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home
# export PATH=$JAVA_HOME/bin:$PATH

# Java 17 경로
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-17.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```
