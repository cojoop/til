# 비동기 데이터 로딩 방식 비교: 함수 분리 vs 직접 호출

비동기 데이터를 로드하는 방식은 코드의 구조, 가독성, 재사용성 등에 영향을 미칩니다. 따라서 프로젝트의 요구사항에 따라 어떤 방식으로 진행할지 선택해야 합니다.

&nbsp;

## 직접 호출 방식

```js
export const load = async ({ fetch }: any) => {
    const productRes = await fetch('https://dummyjson.com/products?limit=10');
    const productData = await productRes.json();
    const products = productData.products;

    const usersRes = await fetch('https://dummyjson.com/users?limit=10');
    const usersData = await usersRes.json();
    const users = usersData.users;

    return {
        products: products,
        users: users,
    };
};
```

&nbsp;

## 함수 분리 방식

```js
export const load = async ({ fetch }: { fetch: any }) => {
    const fetchProducts = async () => {
        const productRes = await fetch(
            'https://dummyjson.com/products?limit=10'
        );
        const productData = await productRes.json();
        return productData.products;
    };

    const fetchUsers = async () => {
        const usersRes = await fetch('https://dummyjson.com/users?limit=10');
        const usersData = await usersRes.json();
        return usersData.users;
    };

    const [products, users] = await Promise.all([
        fetchProducts(),
        fetchUsers(),
    ]);

    return {
        products: products,
        users: users,
    };
};
```

&nbsp;

## 분석 및 비교

#### 코드 구조와 재사용성

- 함수 분리 방식은 기능을 별도의 함수로 분리하여 재사용성을 높입니다.
- 직접 호출 방식은 코드 중복이 발생하고 재사용성이 낮을 수 있습니다.

#### 가독성

- 함수 분리 방식은 기능별로 함수가 분리되어 있어 가독성이 높습니다.
- 직접 호출 방식은 코드가 직렬로 연결되어 있어 가독성이 떨어질 수 있습니다.

#### 동시성

- 함수 분리 방식은 병렬로 호출하여 성능을 향상시킬 수 있습니다.
- 직접 호출 방식은 순차적으로 호출되어 성능이 저하될 수 있습니다.

&nbsp;

> **함수 분리 방식**은 구조화되고 재사용성이 높은 반면, **직접 호출 방식**은 간단하고 코드 중복이 발생할 수 있습니다.
