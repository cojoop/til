# ModelMapper란

ModelMapper는 객체 간 매핑을 자동화하여, 수작업으로 작성해야 하는 번거로운 매핑 코드를 줄여주는 강력한 도구입니다. 주로 DTO(`Data Transfer Object`)와 VO(`Value Object`) 간의 변환에 사용되며, 다양한 계층 간 데이터를 주고받을 때 유용하게 활용됩니다.

### ModelMapper 주요 기능

**1. 자동 매핑 (Automatic Mapping)**
ModelMapper는 필드 이름이 동일하거나 유사할 경우, 별도의 매핑 설정 없이 자동으로 값을 매핑합니다. 이를 통해 객체 간의 변환 작업을 간편하게 처리할 수 있습니다.
   `ex. UserDTO의 name 필드와 User의 name 필드가 동일할 경우 자동으로 매핑됩니다.`
**2. 지능형 매핑 (Intelligent Mapping)**
단순한 필드 매핑 외에도, ModelMapper는 중첩된 객체나 컬렉션 등 복잡한 구조를 지능적으로 매핑할 수 있습니다. 복잡한 객체 그래프도 쉽게 매핑 가능하게 하여 개발자의 작업을 크게 줄여줍니다.
**3. 커스터마이징 가능 (Custom Mapping)**
복잡한 변환 로직이 필요한 경우, 사용자가 매핑 규칙을 세부적으로 정의할 수 있습니다. 필드 간의 이름이 다르거나, 특정 변환 로직이 필요할 경우 사용자 정의 매핑을 설정할 수 있습니다.

```java
    modelMapper.typeMap(Source.class, Destination.class)
            .addMappings(mapper -> mapper.map(Source::getSourceField, Destination::setDestinationField));
```

**4. 유연한 타입 변환 (Flexible Type Conversion)**
기본적인 데이터 타입뿐만 아니라 복잡한 객체나 다른 데이터 타입으로도 변환할 수 있습니다. 기본적으로 Date를 LocalDate로 변환하거나, 숫자를 문자열로 변환하는 등의 작업을 처리할 수 있습니다.

### 언제 사용해야 하는가?

**1. DTO와 VO 간의 변환**
API 레이어에서 데이터를 전송할 때, 도메인 객체를 DTO로 변환하여 외부 시스템에 맞는 구조로 전달하거나, 반대로 데이터를 VO나 엔티티 객체로 변환할 때 유용합니다.
**2. 반복적인 매핑 작업을 최소화할 때**
수작업으로 객체 간의 매핑을 반복하는 경우 코드의 유지보수성이 떨어지며, 실수할 가능성이 높습니다. ModelMapper는 이를 자동화하여 중복된 코드를 줄여주고, 유지보수를 쉽게 만듭니다.
**3. 복잡한 객체 매핑이 필요한 경우**
중첩된 객체나 컬렉션이 포함된 복잡한 매핑이 필요한 상황에서도 ModelMapper는 유용합니다. 재귀적으로 객체 간의 매핑을 처리하여, 개발자가 모든 단계를 명시하지 않아도 됩니다.

#### ModelMapper 설정 및 매핑

```java
// MyDto 객체의 값을 MyVo 객체로 변환하는 예제 코드
ModelMapper modelMapper = new ModelMapper();

// DTO와 VO 매핑
MyDto dto = new MyDto();
// dto에 값 설정
MyVo vo = modelMapper.map(dto, MyVo.class);
```

#### 장점

- 자동 매핑으로 인한 코드 간소화
- 객체 구조가 변경될 경우 수작업 매핑 코드 수정 부담 감소
- 테스트 코드 작성 시, 객체 간의 매핑 로직이 깔끔하게 분리되어 유지보수성 향상
- 복잡한 매핑도 간편하게 처리 가능

> ModelMapper는 DTO와 VO 간의 변환을 간편하게 해주며, 코드의 유지보수성을 높이고 개발 시간을 단축시키는 데 기여합니다. 복잡한 매핑이 필요한 경우 유용한 도구가 될 수 있습니다.
