# 생성자 this( ), 참조변수 this

`Java`에서 `this()`와 참조변수 `this`는 모두 클래스 내에서 인스턴스 멤버를 참조하거나 호출하는 데 사용되지만, 그 용도와 사용 방법이 다릅니다.

### 생성자 this( )

`this()`는 같은 클래스 내의 다른 생성자를 호출할 때 사용되는데, 클래스 이름 대신 `this`를 사용합니다.

- 생성자 체이닝(`constructor chaining`)을 통해 중복 코드를 줄이고 생성자 간의 논리적인 연결을 만들 수 있습니다.
- `this()` 호출은 반드시 생성자의 첫 번째 명령어로 작성되어야 합니다.

```java
// 예제 코드
public class Person {
    private String name;
    private int age;

    // 기본 생성자
    public Person() {
        this("Unknown", 0); // 다른 생성자를 호출
    }

    // 두 개의 매개변수를 가진 생성자
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 출력 메서드
    public void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }

    public static void main(String[] args) {
        Person p1 = new Person();
        Person p2 = new Person("Alice", 30);

        p1.display(); // Name: Unknown, Age: 0
        p2.display(); // Name: Alice, Age: 30
    }
}
```

- `this("Unknown", 0)`는 두 번째 생성자를 호출합니다.
- 이는 기본 생성자가 호출되었을 때도 `name`과 `age`가 초기화되도록 합니다.

### 참조변수 this

`this` 키워드는 객체 자신을 참조하며, 인스턴스 변수와 메서드를 가리키는 데 사용됩니다.

- 주로 메서드나 생성자 내부에서 매개변수 이름과 인스턴스 변수 이름이 동일할 때 혼동을 피하기 위해 사용됩니다.
- 인스턴스 메서드에서 사용, `static` 메서드는 사용 불가

```java
// 예제 코드
public class Employee {
    private String name;
    private double salary;

    // 생성자
    public Employee(String name, double salary) {
        this.name = name; // 인스턴스 변수 name을 매개변수 name으로 초기화
        this.salary = salary; // 인스턴스 변수 salary를 매개변수 salary로 초기화
    }

    // 인스턴스 변수와 동일한 이름의 매개변수를 갖는 메서드
    public void setSalary(double salary) {
        this.salary = salary; // this.salary는 인스턴스 변수, salary는 매개변수
    }

    // 출력 메서드
    public void display() {
        System.out.println("Name: " + this.name + ", Salary: " + this.salary);
    }

    public static void main(String[] args) {
        Employee e = new Employee("Bob", 50000);
        e.display(); // Name: Bob, Salary: 50000

        e.setSalary(60000);
        e.display(); // Name: Bob, Salary: 60000
    }
}
```
