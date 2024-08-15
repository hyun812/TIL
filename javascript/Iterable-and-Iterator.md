## Iterable

- **반복 가능한 객체, 순회 가능한 자료 구조**
- **for…of문 , 전개문법 (Spread syntax) , 구조 분해 할당 등을 사용 가능**
- **배열, 문자열, Map, Set**

**조건**

1. 객체 내에 `[Symbol.iterator]` 를 프로퍼티 키로 사용한 메서드가 존재해야 함

```jsx
const array = [1, 2, 3];

// 배열은 Symbol.iterator 메소드를 소유한다.
// 따라서 배열은 이터러블 프로토콜을 준수한 이터러블이다.
console.log(Symbol.iterator in array); // true

// 이터러블 프로토콜을 준수한 배열은 for...of 문에서 순회 가능하다.
for (const item of array) {
  console.log(item);
}
-----------------------------------------------------------------------------------------------------
const obj = { a: 1, b: 2 };

// 일반 객체는 Symbol.iterator 메소드를 소유하지 않는다.
// 따라서 일반 객체는 이터러블 프로토콜을 준수한 이터러블이 아니다.
console.log(Symbol.iterator in obj); // false
```

## Iterator

- Iterable 객체의 요소를 탐색하기 위한 포인터
- Iterable 객체의 `[Symbol.iterator]` 메서드를 호출하면 이터레이터 프로토콜을 준수한 **Iterator**를 반환함

**조건**

1. Iterator는 `next` 메서드가 존재해야 함
2. `next` 메서드는 `IteratorResult 객체`를 `반환`해야 함
3. `IteratorResult 객체`는 `done: boolean`과 `value: any` 프로퍼티를 가짐

**⇒ done과 value 프로퍼티를 가지는 객체를 반환하는 next 메서드를 가진 객체**

```jsx
// 배열은 이터러블 프로토콜을 준수한 이터러블이다.
const array = [1, 2, 3];

// Symbol.iterator 메소드는 이터레이터를 반환한다.
const iterator = array[Symbol.iterator]();

// 이터레이터 프로토콜을 준수한 이터레이터는 next 메소드를 갖는다.
console.log('next' in iterator); // true

// 이터레이터의 next 메소드를 호출하면 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환한다.
// next 메소드를 호출할 때 마다 이터러블을 순회하며 이터레이터 리절트 객체를 반환한다.
console.log(iterator.next()); // {value: 1, done: false}
console.log(iterator.next()); // {value: 2, done: false}
console.log(iterator.next()); // {value: 3, done: false}
console.log(iterator.next()); // {value: undefined, done: true}
```

## 직접 Iterable 객체 만들기

```jsx
// 피보나치 수열을 구현한 사용자 정의 이터러블을 반환하는 함수
// 수열의 최대값을 인수로 전달받음
const fibonacciFunc = function (max) {
	let [pre, cur] = [0, 1];

	// Symbol.iterator 메서드를 구현한 이터러블을 반환
	return {
		[Symbol.iterator]() {
			returun {
				next() {
					[pre, cur] = [cur, pre+cur];
					return { value: cur, doce: cur >= max };
				}
			};
		}
	};
};

// 이터러블을 반환하는 함수에 수열의 최대값을 인수로 전달하면서 호출함
// fibonacciFunc(10)은 이터러블을 반환함
for (const num of fibonacciFunc(10)) {
	console.log(num); // 1 2 3 5 8
}
```

### **Arrays.from()**

이터러블이나 유사배열 객체를 인수로 전달받아 배열로 변환

- **유사 배열 ( array-like )**
  인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체

```jsx
let arrayLike = { // 인덱스와 length프로퍼티가 있음 => 유사 배열
  0: "Hello",
  1: "World",
  length: 2
};

for (let item of arrayLike) {} // Symbol.iterator가 없으므로 에러 발생

----------------------------------------------------------------------------------------------------------

let arr = Array.from(arrayLike); // ["Hello", "World"] 배열이 됨으로서 이터러블 객체도 된다.
for (let item of arr) {} // ["Hello", "World"]
```

## 이터레이션 프로토콜의 중요성

> **데이터 소비자와 데이터 공급자를 연결하는 인터페이스 역할을 함**

데이터 소비자 : for…of , 스프레드 문법, 배열 디스트럭처링 할당, Map/Set 생성자
데이터 공급자: Array, String, Map/Set, DOM 컬렉션
