# GraphQL의 데이터 유형

`GraphQL`에서는 데이터를 타입으로 정의하며, 서버에서는 이러한 타입을 기반으로 데이터를 저장하고 처리합니다.

### Scalar Types (스칼라 타입)

- `GraphQL`은 기본적인 스칼라 타입을 제공합니다.
- 이는 단일 값만을 나타내는 간단한 데이터 유형입니다.
예: `Int`, `Float`, `String`, `Boolean`, `ID` 등.

<br>

### Object Types (객체 타입)

- 가장 기본적이며 중요한 유형 중 하나입니다.
- 객체 타입은 필드의 집합으로, 서버에서 제공하는 데이터의 구조를 정의합니다.

```graphql
type Person {
  name: String
  age: Int
  email: String
}
```

<br>

### List Types (리스트 타입)

- 여러 값을 가지는 배열 또는 리스트를 나타냅니다.

```graphql
type Post {
  title: String
  comments: [String]
}
```

<br>

### NonNull Types (NonNull 타입)

- 값이 `null`이 될 수 없음을 나타냅니다.
- !를 사용하여 표시됩니다.

```graphql
type Book {
  title: String!
  author: String!
}
```

<br>

### Enum Types (열거형 타입)

- 가능한 값의 정해진 집합을 나타냅니다.

```graphql
enum Status {
  DRAFT
  PUBLISHED
  ARCHIVED
}
```

<br>

### Interface Types (인터페이스 타입)

- 공통 필드 집합을 가진 객체 타입을 정의할 수 있습니다.

```graphql
interface Shape {
  area: Float
}

type Circle implements Shape {
  radius: Float
  area: Float
}

type Square implements Shape {
  sideLength: Float
  area: Float
}
```

<br>

### Union Types (유니온 타입)

- 둘 이상의 다른 타입 중 하나일 수 있는 유형을 정의합니다.

```graphql
union SearchResult = Book | Author | Magazine
```
