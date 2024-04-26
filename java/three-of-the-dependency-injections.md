# 의존성 주입(Dependency Injection) 방법 3가지

의존성 주입은 클래스가 직접 필요한 의존 객체를 생성하지 않고, 외부에서 주입받는 디자인 패턴입니다. 이를 통해 클래스 간의 의존성을 낮추고, 객체 간의 결합도를 약화시켜 코드의 유연성을 높입니다.

아래는 의존성 주입을 활용한 간단한 자바 코드 예시입니다.

```java
abstract class Storage {
    // 데이터를 저장하는 메서드를 추상화합니다.
    abstract void save(String data);
}

class FileStorage extends Storage {
    // 추상 클래스를 상속받은 FileStorage 클래스입니다.
    // 저장 메서드를 구현합니다.
    void save(String data) {
        System.out.println("파일 저장 끝!"); // 파일 저장이 완료되었음을 출력합니다.
    }
}

class DatabaseStorage extends Storage {
    // 추상 클래스를 상속받은 DatabaseStorage 클래스입니다.
    // 저장 메서드를 구현합니다.
    void save(String data) {
        System.out.println("DB 저장 끝!"); // 데이터베이스 저장이 완료되었음을 출력합니다.
    }
}
```

- `Storage` 추상 클래스를 정의하고, 이를 상속받아 파일 저장과 데이터베이스 저장을 수행하는 두 개의 클래스를 구현합니다.

## 의존성 주입 방법

의존성 주입은 크게 세 가지 방법으로 구현할 수 있습니다.

#### 생성자 주입(Constructor Injection)

생성자 주입은 의존성을 클래스의 생성자를 통해 주입하는 방식 입니다.

```java
class DataManager {
    private Storage storage;

    // 생성자를 통해 저장소를 초기화합니다.
    DataManager(Storage storage) {
        this.storage = storage;
    }

    // 데이터를 저장하는 메서드입니다.
    void saveData(String data) {
        storage.save(data);
    }
}

public static void main(String[] args) {
    DataManager manager = new DataManager(new DatabaseStorage()); // DataManager 객체를 생성하고 데이터베이스 저장소를 사용합니다.
    manager.saveData("중요한 내용"); // DataManager를 통해 데이터를 저장합니다.
}
```

- `DataManager`은 `Storage` 인터페이스를 통해 의존성을 받습니다.
- 따라서 `DataManager`는 어떤 종류의 `Storage` 구현체를 사용할지에 대한 결정을 내릴 필요가 없습니다.

#### Setter 주입(Setter Injection)

`Setter` 주입은 의존성을 클래스의 `Setter` 메서드를 통해 주입하는 방식입니다.

```java
class DataManager {
    private Storage storage; // 저장소 객체를 선언합니다.

    // 저장소를 설정하는 메서드입니다.
    void setStorage(Storage storage) {
        this.storage = storage;
    }

    // 데이터를 저장하는 메서드입니다.
    void saveData(String data) {
        storage.save(data); // 현재 설정된 저장소에 데이터를 저장합니다.
    }
}

public static void main(String[] args) {
    DataManager manager = new DataManager(); // DataManager 객체를 생성합니다.
    manager.setStorage(new DatabaseStorage()); // DataManager에 데이터베이스 저장소를 설정합니다.
    manager.saveData("중요한 내용"); // DataManager를 통해 데이터를 저장합니다.
}
```

- `Setter` 주입은 객체 생성 후에 의존성을 주입하는 방식으로, 클래스의 인스턴스를 만든 후에 의존성을 변경할 수 있습니다.

#### 필드 주입(Field Injection)

필드 주입은 의존성을 클래스의 필드에 직접 주입하는 방식입니다.

```java
class DataManager {
    private Storage storage = new DatabaseStorage(); // 기본적으로 DatabaseStorage를 사용합니다.

    // 데이터를 저장하는 메서드입니다.
    void saveData(String data) {
        storage.save(data); // 현재 설정된 저장소에 데이터를 저장합니다.
    }
}

public static void main(String[] args) {
    DataManager manager = new DataManager(); // DataManager 객체를 생성합니다.
    manager.saveData("중요한 내용"); // DataManager를 통해 데이터를 저장합니다.
}
```

- 필드 주입은 코드가 간결하지만, 테스트 용이성이 떨어질 수 있습니다.
- 또한 의존성이 변경될 때 클래스의 수정이 필요하므로 유연성이 떨어질 수 있습니다.
