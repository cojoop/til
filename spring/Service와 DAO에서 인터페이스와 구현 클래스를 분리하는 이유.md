# Service와 DAO에서 인터페이스와 구현 클래스를 분리하는 이유

Service와 DAO(`Data Access Object`) 계층에서 인터페이스와 구현 클래스(일반적으로 `Impl` 접미사를 사용)를 분리하여 사용하는 것은 소프트웨어 설계에서 매우 일반적인 패턴입니다.
이러한 분리는 유지보수성, 확장성, 테스트 용이성 등을 향상시키며, 다양한 상황에서 유용하게 활용됩니다.

## 인터페이스와 구현 클래스 분리의 이유

### 유연성과 확장성 향상

인터페이스와 구현을 분리함으로써 구현체를 독립적으로 확장할 수 있습니다.

- 새로운 구현 방식을 쉽게 추가할 수 있음
- 기존 구현체를 변경하거나 확장해도 클라이언트 코드에 영향을 주지 않음
- OCP(`Open-Closed Principle`) 원칙을 준수할 수 있음

### 협업 용이성

인터페이스는 큰 뼈대 역할을 하여 팀원 간 협업에 도움이 됩니다.

- 함수명, 리턴 타입 등 주요 사항을 인터페이스에서 확인 가능
- 개발자들이 공통된 구조를 공유하며 작업 가능

### 추상화와 의존성 감소

인터페이스를 통해 세부 구현을 숨기고 추상화된 인터페이스만 노출할 수 있습니다.

- 클래스 간 의존관계를 줄일 수 있음
- 다형성을 활용할 수 있음

### 비즈니스 로직과 데이터 접근 분리

Service와 DAO를 분리함으로써

- **Service:** 사용자 요청에 대한 비즈니스 로직 구현
- **DAO:** 데이터베이스 접근 관련 로직 구현
- 각 계층의 역할과 책임을 명확히 분리

### 주의사항

- 1:1 관계의 `인터페이스-구현체` 구조는 실질적 이점이 없을 수 있음
- 프로젝트 특성에 따라 적절한 구조 선택 필요
- 확장 가능성과 현재 복잡도를 고려하여 결정해야 함

## 분리할 때와 분리하지 않을 때의 차이

### 분리할 때

#### 장점

- 코드의 유연성과 재사용성이 높아집니다.
- 구현 변경이 용이합니다.
- 테스트가 쉬워집니다.

#### 단점

- 초기 설계 시간이 더 필요할 수 있습니다.
- 작은 프로젝트에서는 과도한 복잡성을 야기할 수 있습니다.

### 분리하지 않을 때

#### 장점

- 코드가 간단하고 직관적일 수 있습니다.
- 작은 프로젝트나 프로토타입에 적합할 수 있습니다.

#### 단점

- 코드 재사용성이 떨어집니다.
- 구현 변경 시 의존하는 모든 코드를 수정해야 할 수 있습니다.
- 테스트가 어려워질 수 있습니다.

### 실제 적용 예시

#### Service 레이어

```java
// 인터페이스
public interface ProductService {
    List<ProductDto> getAllProducts();
    ProductDto getProductById(Long id);
    // 다른 메서드들...
}

// 구현 클래스
@Service
public class ProductServiceImpl implements ProductService {
    private final ProductDao productDao;

    @Autowired
    public ProductServiceImpl(ProductDao productDao) {
        this.productDao = productDao;
    }

    @Override
    public List<ProductDto> getAllProducts() {
        // 구현 로직
    }

    @Override
    public ProductDto getProductById(Long id) {
        // 구현 로직
    }
    // 다른 메서드 구현들...
}
```

#### DAO 레이어

```java
// 인터페이스
public interface ProductDao {
    List<Product> findAll();
    Product findById(Long id);
    // 다른 메서드들...
}

// 구현 클래스
@Component
public class ProductDaoImpl implements ProductDao {
    private final ProductRepository productRepository;

    @Autowired
    public ProductDaoImpl(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    @Override
    public List<Product> findAll() {
        // 구현 로직
    }

    @Override
    public Product findById(Long id) {
        // 구현 로직
    }
    // 다른 메서드 구현들...
}
```
