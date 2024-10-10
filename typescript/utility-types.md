## 유틸리티 타입

- TypeScript는 복잡한 타입을 쉽게 조작할 수 있는 여러 유틸리티 타입을 제공함
- 타입 유틸리티들을 활용하면 코드의 타입 안정성을 높이고, 재사용 가능한 타입을 쉽게 정의할 수 있음

<br/>

## 종류

### Partial<T>

모든 속성을 선택적으로 변경한 새로운 타입을 반환

```typescript
interface User {
  name: string;
  age: number;
  phone: number;
}

// 인터페이스 User의 속성을 모두 optional 설정
function updateUser(user: Partial<User>) {
  // 일부 필드만 업데이트 가능
}

updateUser({ name: 'John' }); // 유효
```

<br/>

### Required<T>

모든 속성을 필수로 변경한 새로운 타입을 반환

```typescript
interface User {
  name?: string;
  age?: number;
  phone?: number;
}

type RequiredUser = Required<User>;

// 모든 속성이 필수
const config: RequiredUser = {
  name: '홍길동',
  age: 22,
  phone: 111,
};
```

<br/>

### Pick<T, K>

특정 속성만을 선택한 새로운 타입을 반환

```typescript
interface Product {
  id: number;
  name: string;
  price: number;
  description: string;
}

type ProductPreview = Pick<Product, 'name' | 'price'>;
// { name: string; price: number; }

const preview: ProductPreview = {
  name: 'Laptop',
  price: 1000,
};
```

<br/>

### Omit<T, K>

특성 속성을 제외한 새로운 타입을 반환

```typescript
interface User {
  id: number;
  username: string;
  password: string;
}

type PublicUser = Omit<User, 'password'>;
// { id: number; username: string; }

const publicInfo: PublicUser = {
  id: 1,
  username: 'john_doe',
};
```

<br/>

### Record<K, T>

키-값 쌍의 타입을 정의

```typescript
const fruitInventory = {
  apple: 10,
  banana: 20,
  orange: 15,
};

type Fruit = 'apple' | 'banana' | 'orange';
type Stock = Record<Fruit, number>;

const fruitInventory: Stock = {
  apple: 10,
  banana: 20,
  orange: 15,
};
```

<br/>

### Readonly<T>

모든 속성을 읽기 전용으로 변경한 새로운 타입을 반환

```typescript
interface Config {
  apiKey: string;
  timeout: number;
}

type ReadonlyConfig = Readonly<Config>;

const config: ReadonlyConfig = {
  apiKey: 'my-secret-key',
  timeout: 3000,
};

// config.apiKey = "new-key"; // ERROR: 읽기 전용 속성
```

<br/>

### ReturnType<T>

함수의 return 타입을 추출

```typescript
function fetchUser() {
  return { id: 1, name: 'John', age: 30 };
}

type User = ReturnType<typeof fetchUser>;
// 결과: { id: number; name: string; age: number; }

const user: User = {
  id: 2,
  name: 'Jane',
  age: 28,
};
```

<br/>

### Parameters<T>

함수의 매개변수 타입을 튜플로 추출

```typescript
function greet(name: string, age: number) {
  return `Hello, ${name}! You are ${age} years old.`;
}

type GreetParams = Parameters<typeof greet>;
// 결과: [string, number]

const params: GreetParams = ['Alice', 25];
console.log(greet(...params));
```
