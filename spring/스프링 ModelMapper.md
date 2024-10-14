# ModelMapper란

ModelMapper는 Java 객체 간 매핑을 자동화하는 유용한 라이브러리로, 소스 객체의 필드 값을 대상 객체의 필드로 자동으로 매핑합니다.

- 주로 DTO와 엔티티 간 변환이나 서로 다른 객체 간 데이터 전송에 사용됩니다.

### 작동 원리

ModelMapper는 리플렉션을 사용하여 객체의 타입을 분석하고, 설정된 매칭 전략에 따라 속성들을 매핑합니다.
`map(source, destination)` 메서드가 호출되면 소스와 대상 객체의 구조를 분석하여 일치하는 필드를 찾아 값을 복사합니다.

### 주요 기능

#### 1. 자동 매핑

기본적으로 이름이 일치하는 필드들을 자동으로 매핑합니다.

```java
ModelMapper modelMapper = new ModelMapper();
DestinationObject dest = modelMapper.map(sourceObject, DestinationObject.class);
```

#### 2. 커스텀 매핑

필드 이름이 다르거나 복잡한 변환이 필요한 경우 커스텀 매핑을 설정할 수 있습니다1:

```java
modelMapper.typeMap(SourceClass.class, DestClass.class)
    .addMapping(SourceClass::getSourceField, DestClass::setDestField);
```

#### 3. 매칭 전략

ModelMapper는 세 가지 주요 매칭 전략을 제공합니다12:

- **STANDARD:** 기본 전략으로, 유연하게 매칭합니다.
- **LOOSE:** 가장 관대한 전략으로, 부분적 일치도 허용합니다.
- **STRICT:** 가장 엄격한 전략으로, 정확히 일치하는 필드만 매핑합니다.

```java
modelMapper.getConfiguration().setMatchingStrategy(MatchingStrategies.STRICT);
```

#### 장점

- **코드 간소화:** 반복적인 `setter/getter` 호출을 줄여줍니다.
- **유연성:** 다양한 매칭 전략과 커스텀 설정을 통해 복잡한 매핑도 처리 가능합니다.
- **유지보수성:** 객체 구조 변경 시 매핑 코드 수정이 최소화됩니다.

#### 주의사항

- **성능:** 리플렉션 사용으로 인한 약간의 성능 저하가 있을 수 있습니다.
- **복잡성:** 매우 복잡한 매핑의 경우 디버깅이 어려울 수 있습니다.
- **타입 안전성:** 컴파일 시점에 타입 체크가 어려울 수 있습니다.

ModelMapper는 객체 간 데이터 전송을 크게 간소화해주는 강력한 도구입니다. 적절히 사용하면 코드의 가독성과 유지보수성을 크게 향상시킬 수 있습니다.
