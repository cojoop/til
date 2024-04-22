# 생성자(Constructor)란?

`Java`에서 생성자(`Constructor`)는 클래스를 인스턴스화할 때 호출되는 특별한 메서드입니다. 생성자는 객체를 생성하고 초기화하는 데 사용되며, 주로 클래스의 멤버 변수를 초기화하고 초기 상태를 설정하는 역할을 합니다.

> 객체를 생성할 때 객체의 초기화를 담당하는데, 클래스 이름과 동일하며 반환 유형을 지정하지 않습니다. 이를 통해 생성자는 일반적인 메서드와 구별됩니다.

## 사용 이유

1. **객체 초기화:** 생성자는 새로운 객체를 만들 때 필요한 초기화 작업을 수행할 수 있습니다. 이를 통해 객체를 사용하기 전에 필요한 초기 설정을 할 수 있습니다.
2. **인스턴스 변수 설정:** 생성자를 사용하여 클래스의 인스턴스 변수를 설정하고 초기화할 수 있습니다. 이를 통해 객체의 상태를 관리하고 관련 데이터를 설정할 수 있습니다.
3. **객체 상태 설정:** 객체의 초기 상태를 설정하는 데 사용됩니다. 예를 들어, 객체가 생성될 때 특정 값을 기본값으로 설정할 수 있습니다.
4. **불변성 보장:** 불변 클래스를 만들 때 생성자는 객체의 상태를 변경할 수 없도록 보장합니다. 생성자를 통해 한 번 생성된 객체는 변경되지 않도록 유지됩니다.

## 예제 코드

#### 생성자를 사용한 경우

```java
public class Car {
    private String brand;
    private String model;

    // 생성자
    public Car(String brand, String model) {
        this.brand = brand;
        this.model = model;
    }

    // Getter 메서드
    public String getBrand() {
        return brand;
    }

    public String getModel() {
        return model;
    }
}

public class Main {
    public static void main(String[] args) {
        // 생성자를 사용하여 객체 생성
        Car car = new Car("Toyota", "Corolla");
        System.out.println("Brand: " + car.getBrand());
        System.out.println("Model: " + car.getModel());
    }
}
```

#### 생성자를 사용하지 않은 경우

```java
public class Car {
    private String brand;
    private String model;

    // 생성자를 사용하지 않고 인스턴스 변수를 초기화하는 메서드
    public void initialize(String brand, String model) {
        this.brand = brand;
        this.model = model;
    }

    // Getter 메서드
    public String getBrand() {
        return brand;
    }

    public String getModel() {
        return model;
    }
}

public class Main {
    public static void main(String[] args) {
        // 생성자를 사용하지 않고 객체 생성
        Car car = new Car();
        // 객체를 사용하기 전에 initialize 메서드를 호출하여 초기화해야 함
        car.initialize("Toyota", "Corolla");
        System.out.println("Brand: " + car.getBrand());
        System.out.println("Model: " + car.getModel());
    }
}
```

#### 생성자 사용 여부

#### 사용하는 경우

- 객체를 생성할 때 초기화가 필요한 경우.
- 클래스의 인스턴스 변수를 설정하고 초기화해야 하는 경우.
- 객체의 초기 상태를 설정해야 하는 경우.
- 불변 클래스를 만들 때 객체의 상태를 변경할 수 없도록 보장하는 경우.

#### 사용하지 않는 경우

- 객체의 초기화가 필요하지 않은 경우.
- 클래스의 인스턴스 변수가 이미 초기화되어 있거나, 다른 방식으로 초기화될 때.
- 객체의 초기화를 수동으로 처리하거나, 초기화 메서드를 사용하는 경우.
