# JDK, JVM, JRE

JDK, JVM, JRE는 Java 프로그래밍 환경의 핵심 구성 요소입니다. 각각의 역할과 관계를 설명하겠습니다.

### JDK (Java Development Kit)

JDK는 Java 애플리케이션을 개발하기 위한 소프트웨어 개발 키트입니다.

- Java 프로그램을 개발하고 컴파일하는 데 필요한 도구들을 포함합니다.

#### 주요 구성 요소

- 컴파일러 (`javac`)
- 디버거
- 개발 도구 (`javadoc` 등)

JDK는 개발자가 Java 프로그램을 작성하고 빌드하는 데 필요한 모든 것을 제공합니다.

### JRE (Java Runtime Environment)

JRE는 Java 프로그램을 실행하기 위한 환경입니다.

- Java 프로그램 실행에 필요한 라이브러리와 JVM을 포함합니다.
- JDK의 일부이지만, 독립적으로도 설치 가능합니다 (JDK 11 이전 버전까지).
- Java 프로그램을 실행만 하고 개발은 하지 않는 사용자에게 필요합니다.

### JVM (Java Virtual Machine)

JVM은 Java 바이트코드를 실행하는 가상 머신입니다.

- Java의 플랫폼 독립성을 가능하게 하는 핵심 요소입니다.
- Java 소스코드가 컴파일된 바이트코드를 해석하고 실행합니다.
- 메모리 관리, 가비지 컬렉션 등을 담당합니다.

#### 관계 정리

- JDK는 JRE를 포함하고, JRE는 JVM을 포함합니다.
- **Java 프로그램 개발:** JDK 필요
- **Java 프로그램 실행:** JRE 필요 (JVM 포함)

JDK, JRE, JVM의 이러한 구조는 Java의 `"Write Once, Run Anywhere"` 철학을 실현하는 데 중요한 역할을 합니다.
