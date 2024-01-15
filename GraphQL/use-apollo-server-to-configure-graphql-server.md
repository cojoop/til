# Apollo Server를 사용하여 GraphQL 서버를 설정하기

**Apollo Server**는 `GraphQL` 서버를 빠르고 쉽게 설정할 수 있도록 도와주는 `GraphQL` 서버 라이브러리입니다. Apollo Server는  `GraphQL` 스키마, 데이터 소스 및 리졸버를 관리하며, `Apollo Client`와 함께 사용하면 클라이언트와 서버 간의 데이터 통신을 용이하게 만들어줍니다.

## 기본 환경 구성

프로젝트 폴더에서 다음 명령어를 사용하여 기초적인 세팅을 합니다.

```bash
# package.json setting
npm init -y

# graphql 및 apollo server 설치
npm i apollo-server graphql

# nodemon 설치
npm i nomdemon -D
```

> `nodemon`은 코드 변경을 감지하고 자동으로 서버를 다시 시작해주는 기능을 제공합니다.

<br>

`package.json` 파일을 다음과 같이 수정합니다.

```json
'scripts': {
    'dev': 'nodemon server.js'
}
'type': 'module'
```

- `scripts` 항목은 개발 서버를 실행하는데 사용되는 `dev` 스크립트를 정의합니다.
- `dev` 스크립트는 `nodemon`을 사용하여 `server.js` 파일을 실행하며, 코드 수정 시 자동으로 서버를 다시 시작합니다.
- `type` 항목은 `ECMAScript` 모듈을 사용한다는 것을 나타내며, `JavaScript` 파일의 확장자는 `.mjs` 또는 `.js`를 사용합니다.

<br>

## 서버 설정

`GraphQL` 스키마와 리졸버를 사용하여 `Apollo Server`를 설정합니다. 아래 코드에서는 `typeDefs`에 스키마를 정의하고 `resolvers`에 해당 스키마를 해결하는 함수를 작성합니다.

#### 임시 데이터

```js
let users = [
    {
        id: '1',
        firstName: 'Lionel',
        lastName: 'Messi',
    },
    {
        id: '2',
        firstName: 'Cristiano',
        lastName: 'Ronaldo',
    },
];
```

<br>

#### GraphQL 스키마 정의

```js
// 자료요청에 사용될 쿼리 정의 및 반횐될 데이터 형태 지정
const typeDefs = gql`
    type User {
        id: ID!
        firstName: String!
        lastName: String!
        fullName: String!
    }
    type Query {
        allUsers: [User!]!
    }
    type Mutation {
        addUser(firstName: String!, lastName: String!): User!
        deleteUser(id: ID!): Boolean!
    }
`;
```

<br>

#### 리졸버 함수 정의

```js
const resolvers = {
    // Query는 object의 항목들로 데이터를 반환(GET과 유사)
    Query: {
        allUsers() {
            console.log('allUsers called!');
            return users;
        },
    },
    // Mutation은 삭제, 수정, 추가 등의 요청 (POST와 유사)
    Mutation: {
        addUser(_, { firstName, lastName }) {
            const newUser = {
                id: tweets.length + 1,
                firstName,
                lastName,
            };
            users.push(newUser);
            return newUser;
        },
        deleteUser(_, { id }) {
            const user = users.find((user) => user.id === id);
            if (!user) return false;
            users = userss.filter((user) => user.id !== id);
            return true;
        },
    },
    User: {
        fullName({ firstName, lastName }) {
            return `${firstName} ${lastName}`;
        },
    },
};
```

<br>

#### Apollo Server 인스턴스 생성

```js
const server = new ApolloServer({ typeDefs, resolvers });
server.listen().then(({ url }) => {
    console.log(`Running on ${url}`);
});
```
