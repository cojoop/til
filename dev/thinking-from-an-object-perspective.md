# 객체지향에서 클래스 관점이 아닌 객체의 관점으로 생각하기

객체지향 프로그래밍(`OOP, Object-Oriented Programming`)에서 객체의 관점에서 생각하는 것은 객체의 상태와 행동을 중심으로 시스템을 설계하는 것을 의미하며, 이는 보다 유연하고 직관적인 코드를 작성하는 데 도움을 줍니다.

이 접근 방식은 객체들의 협력과 상호작용을 중시하며, 각 객체가 가진 상태와 행동을 기반으로 설계를 진행합니다.

>객체지향 프로그래밍의 진정한 핵심은 `“객체”` 자체에 있습니다.

## 객체 지향 설계의 핵심 원칙

1. **캡슐화(Encapsulation):** 객체는 자신의 상태를 캡슐화하고, 외부에서는 객체가 제공하는 메서드를 통해서만 상태를 변경할 수 있습니다.
2. **상속(Inheritance):** 객체는 부모 객체의 특성과 행동을 상속받을 수 있으며, 이를 통해 코드의 재사용성을 높입니다.
3. **다형성(Polymorphism):** 객체는 동일한 메시지에 대해 다르게 응답할 수 있습니다. 이는 객체가 자신의 타입에 따라 서로 다른 방식으로 행동할 수 있도록 합니다.
4. **책임 할당(Responsibility Assignment):** 각 객체는 자신이 해야 할 일을 알고 있으며, 이는 객체의 책임으로 정의됩니다.

## 예제 코드

간단한 게임 캐릭터 시스템

#### 클래스 중심의 접근

클래스 중심의 접근은 클래스의 계층 구조와 메서드 정의에 중점을 둡니다.

```java
class Character {
    private String name;
    private int health;

    public Character(String name, int health) {
        this.name = name;
        this.health = health;
    }

    public void attack(Character target) {
        // 기본 공격 메서드 (재정의 필요)
    }

    public String getName() {
        return name;
    }

    public int getHealth() {
        return health;
    }

    public void setHealth(int health) {
        this.health = health;
    }
}

class Warrior extends Character {
    private int strength;

    public Warrior(String name, int health, int strength) {
        super(name, health);
        this.strength = strength;
    }

    @Override
    public void attack(Character target) {
        target.setHealth(target.getHealth() - strength);
    }
}

class Mage extends Character {
    private int mana;

    public Mage(String name, int health, int mana) {
        super(name, health);
        this.mana = mana;
    }

    @Override
    public void attack(Character target) {
        if (mana >= 10) {
            target.setHealth(target.getHealth() - 10);
            mana -= 10;
        }
    }
}
```

#### 객체 중심의 접근

객체 중심의 접근은 객체 간의 상호작용과 각 객체의 책임에 중점을 둡니다.

```java
class Character {
    private String name;
    private int health;

    public Character(String name, int health) {
        this.name = name;
        this.health = health;
    }

    public void attack(Character target) {
        // 기본 공격 메서드 (재정의 필요)
    }

    public void takeDamage(int damage) {
        health -= damage;
        System.out.println(name + " now has " + health + " health left.");
    }

    public String getName() {
        return name;
    }

    public int getHealth() {
        return health;
    }
}

class Warrior extends Character {
    private int strength;

    public Warrior(String name, int health, int strength) {
        super(name, health);
        this.strength = strength;
    }

    @Override
    public void attack(Character target) {
        System.out.println(getName() + " attacks " + target.getName() + " with strength " + strength);
        target.takeDamage(strength);
    }
}

class Mage extends Character {
    private int mana;

    public Mage(String name, int health, int mana) {
        super(name, health);
        this.mana = mana;
    }

    @Override
    public void attack(Character target) {
        if (mana >= 10) {
            System.out.println(getName() + " casts a spell on " + target.getName());
            target.takeDamage(10);
            mana -= 10;
        } else {
            System.out.println(getName() + " does not have enough mana!");
        }
    }
}

// 객체 생성 및 상호작용
public class Main {
    public static void main(String[] args) {
        Warrior warrior = new Warrior("Aragorn", 100, 15);
        Mage mage = new Mage("Gandalf", 80, 50);

        warrior.attack(mage);
        mage.attack(warrior);
    }
}
```

객체 중심의 접근은 다음과 같은 특징을 가집니다.

1. **객체 간 상호작용:** 각 객체는 다른 객체와 어떻게 상호작용할지를 명확하게 정의하고 있습니다. 예를 들어, `warrior.attack(mage)`는 전사가 마법사를 공격하는 동작을 나타냅니다.
2. **책임의 분산:** 각 객체는 자신의 상태를 관리하고, 필요한 경우 다른 객체와의 상호작용을 통해 상태를 변경합니다. 예를 들어, `takeDamage` 메서드는 객체가 데미지를 받을 때 호출되어 객체의 상태를 변경합니다.
3. **독립적 행동:** 각 객체는 자신의 속성과 메서드에 따라 독립적으로 행동합니다. 전사와 마법사는 각각의 고유한 행동 방식(공격 방법과 마법 사용)을 가지고 있습니다.
