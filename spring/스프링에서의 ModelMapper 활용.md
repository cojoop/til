# 스프링에서의 ModelMapper 활용

ModelMapper는 Java 객체 간 매핑을 자동화하는 유용한 라이브러리로, 소스 객체의 필드 값을 대상 객체의 필드로 자동으로 매핑합니다.

- 주로 DTO와 엔티티 간 변환이나 서로 다른 객체 간 데이터 전송에 사용됩니다.

### 주요 특징

- **자동 매핑:** 소스 객체와 대상 객체의 필드명이 유사할 경우 자동으로 매핑을 수행합니다.
- **유연한 매칭 전략:** `STANDARD`, `LOOSE`, `STRICT` 등 다양한 매칭 전략을 제공하여 상황에 맞는 매핑 방식을 선택할 수 있습니다.
- **커스텀 매핑:** 필드명이 다르거나 복잡한 매핑 로직이 필요한 경우 사용자 정의 매핑을 설정할 수 있습니다.

### 사용 방법

#### 기본 사용

```java
ModelMapper modelMapper = new ModelMapper();
DestinationObject dest = modelMapper.map(sourceObject, DestinationObject.class);
```

#### TypeMap을 이용한 커스텀 매핑

```java
modelMapper.typeMap(SourceClass.class, DestinationClass.class)
    .addMappings(mapper -> {
        mapper.map(SourceClass::getSourceField, DestinationClass::setDestField);
    });
```

#### 매핑 제외

```java
modelMapper.typeMap(SourceClass.class, DestinationClass.class)
    .addMappings(mapper -> {
        mapper.skip(DestinationClass::setFieldToSkip);
    });
```

### ModelMapper의 추가 기능

#### 1. 조건부 매핑

특정 조건을 기반으로 매핑을 수행할 수 있습니다.
예를 들어, 소스 객체의 필드 값이 `null`이 아니거나 특정 조건을 만족할 때만 매핑하도록 설정할 수 있습니다.

```java
modelMapper.typeMap(SourceClass.class, DestinationClass.class)
    .addMappings(mapper -> {
        mapper.when(context -> context.getSource() != null)
              .map(SourceClass::getSourceField, DestinationClass::setDestField);
    });
```

#### 2. 컬렉션 매핑

컬렉션 또는 배열도 자동으로 매핑할 수 있습니다.
소스와 대상 객체의 컬렉션 필드를 간단하게 매핑할 수 있어 여러 개의 객체를 한 번에 처리할 때 유용합니다.

```java
List<DestinationObject> destList = modelMapper.map(sourceList, new TypeToken<List<DestinationObject>>(){}.getType());
```

#### 3. 매핑 전략 선택

매핑 전략을 설정하여 보다 엄격하거나 느슨한 기준을 적용할 수 있습니다.

- **STANDARD (기본):** 소스와 대상 객체의 필드 이름이 유사한 경우 매핑을 시도합니다.
- **STRICT:** 소스 객체와 대상 객체의 필드 이름이 정확히 일치해야 매핑됩니다.
- **LOOSE:** 필드 이름이 부분적으로 일치해도 매핑됩니다.

### 스프링에서의 활용

스프링 프로젝트에서는 ModelMapper를 빈으로 등록하여 전역적으로 사용할 수 있습니다.

```java
@Configuration
public class ModelMapperConfig {
    @Bean
    public ModelMapper modelMapper() {
        ModelMapper modelMapper = new ModelMapper();
        modelMapper.getConfiguration().setMatchingStrategy(MatchingStrategies.STRICT);
        return modelMapper;
    }
}
```

- **의존성 주입:** 설정한 ModelMapper 빈을 다른 서비스나 컴포넌트에서 의존성 주입을 통해 사용할 수 있습니다.
- **성능 고려:** 대규모 프로젝트에서는 빈번한 매핑이 성능에 영향을 줄 수 있으므로, 사용 빈도에 따라 성능 최적화 전략을 고려해야 합니다.
  - `ex.` DTO 변환이 많다면 별도의 DTO 전환 유틸리티를 만들거나, 복잡한 매핑은 수동으로 처리하는 방식도 고려할 수 있습니다.

```java
// DTO와 Entity 간 매핑
// Entity -> DTO
UserDTO userDTO = modelMapper.map(userEntity, UserDTO.class);

// DTO -> Entity
UserEntity userEntity = modelMapper.map(userDTO, UserEntity.class);
```

### ModelMapper vs 수동 매핑

#### 수동 매핑

- **장점:** 매핑의 세부 사항을 명확하게 제어할 수 있습니다.
- **단점:** 코드가 길어지고 반복적인 getter/setter 호출이 발생합니다.

#### ModelMapper

- **장점:** 코드가 간결해지고 유지보수가 용이합니다.
- **단점:** 복잡한 매핑 로직이 필요한 경우 성능 저하나 디버깅의 어려움이 있을 수 있습니다.

결론적으로, ModelMapper는 간결하고 유지보수하기 쉬운 코드를 작성하는 데 매우 유용하지만, 복잡한 매핑 로직이 필요한 경우에는 커스텀 매핑 또는 수동 매핑을 혼용하는 것이 좋습니다.
