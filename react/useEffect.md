> 무분별한 useEffect 사용은 불필요한 렌더링 + 성능 저하 + 의도치 않은 오류 + 가독성 저하

## 왜 useEffect라고 이름을 지었을까?

- `useEffect`는 컴포넌트가 `렌더링된 이후`에 실행되는 코드로, `부수 효과`를 처리하기 위한 훅

- 여기서 Effect는 부수 효과를 의미하며, 컴포넌트가 UI를 업데이트할 때와 별개로 발생해야 하는 작업을 의미

- 컴포넌트가 재렌더링 될 때 특정 조건에 의존하여 수행되며, 컴포넌트가 최대한 순수 함수를 유지할 수 있도록 도와줌

<br/>

## 주의할 점

- 렌더링 중에 계산할 수 있다면 Effect가 필요하지 않음

- useEffect 안에서 사용하는 모든 변수들은 의존성 배열에 추가

- 조건부로 useEffect 를 활용해야 한다면 함수 초기에 바로 return 하도록 구현

- useEffect, eventHandler 둘 중 어디에 코드를 작성해야할지 모르겠다면 코드가 실행되어야 하는 이유에 생각

  - useEffect는 컴포넌트가 사용자에게 표시되었기 때문에 실행되어야 하는 코드

  - eventHandler는 사용자가 한 행동(상호작용)에 의해 실행되어야 하는 코드

<br/>

## props, state 변경에 따라 또 다른 state를 업데이트 해야할 때

- 기존 props나 state에서 계산할 수 있다면 렌더링 중에 계산

```javascript
function Form() {
  const [firstName, setFirstName] = useState('Taylor');
  const [lastName, setLastName] = useState('Swift');

  // 🔴 피하세요: 중복된 state 및 불필요한 Effect
  const [fullName, setFullName] = useState('');
  useEffect(() => {
    setFullName(firstName + ' ' + lastName);
  }, [firstName, lastName]);
  // ...
}
```

```javascript
function Form() {
  const [firstName, setFirstName] = useState('Taylor');
  const [lastName, setLastName] = useState('Swift');
  // ✅ 좋습니다: 렌더링 중에 계산됨
  const fullName = firstName + ' ' + lastName;
  // ...
}
```

<br/>

## props 변경에 따라 데이터를 수정해야 하는 경우

- 불필요한 리렌더링을 발생시킴

```javascript
function TodoList({ todos, filter }) {
  const [newTodo, setNewTodo] = useState('');

  // 🔴 피하세요: 중복된 state 및 불필요한 효과
  const [visibleTodos, setVisibleTodos] = useState([]);
  useEffect(() => {
    setVisibleTodos(getFilteredTodos(todos, filter));
  }, [todos, filter]);

  // ...
}
```

- 컴포넌트가 리렌더링 될 때마다 visibleTodos가 업데이트 되기 때문에 최신 ui를 보장

```javascript
function TodoList({ todos, filter }) {
  const [newTodo, setNewTodo] = useState('');
  // ✅ getFilteredTodos()가 느리지 않다면 괜찮습니다.
  const visibleTodos = getFilteredTodos(todos, filter);
  // ...
}
```

- 복잡한 연산이라면 `useMemo` 활용

```javascript
import { useMemo, useState } from 'react';

function TodoList({ todos, filter }) {
  const [newTodo, setNewTodo] = useState('');
  // ✅ todos나 filter가 변경되지 않는 한 getFilteredTodos()를 다시 실행하지 않습니다.
  const visibleTodos = useMemo(() => getFilteredTodos(todos, filter), [todos, filter]);
  // ...
}
```

<br/>

## props 변경에 따라 상태가 초기화되어야 하는 경우

- userId 변경 => 리렌더링 => comment 변경 => 리렌더링

```javascript
export default function ProfilePage({ userId }) {
  const [comment, setComment] = useState('');

  // 🔴 피하세요: Effect에서 prop 변경 시 state 초기화
  useEffect(() => {
    setComment('');
  }, [userId]);
  // ...
}
```

- userId 변경 시 key 값이 변경되기 때문에 comment를 리셋할 필요가 없음

- 명시적인 key를 전달하여 각 사용자의 프로필이 개념적으로 다른 프로필임을 알릴 수 있음

- key값인 userId가 변경될 때마다 React는 새로운 DOM을 다시 생성하고 state를 재설정함

```javascript
export default function ProfilePage({ userId }) {
  return <Profile userId={userId} key={userId} />;
}

function Profile({ userId }) {
  // ✅ 이 state 및 아래의 다른 state는 key 변경 시 자동으로 재설정됩니다.
  const [comment, setComment] = useState('');
  // ...
}
```

<br/>

## prop이 변경에 따라 일부 상태만 조정해야하는 경우

- items가 변경 => 리렌더링 => selection 변경 => 리렌더링

```javascript
function List({ items }) {
  const [isReverse, setIsReverse] = useState(false);
  const [selection, setSelection] = useState(null);

  // 🔴 피하세요: Effect에서 prop 변경 시 state 조정하기
  useEffect(() => {
    setSelection(null);
  }, [items]);
  // ...
}
```

- 렌더링을 줄일 수는 있지만 데이터 흐름을 이해하고 디버깅 하기에는 더 어려워짐

```javascript
function List({ items }) {
  const [isReverse, setIsReverse] = useState(false);
  const [selection, setSelection] = useState(null);

  // 더 좋습니다: 렌더링 중 state 조정
  const [prevItems, setPrevItems] = useState(items);
  if (items !== prevItems) {
    setPrevItems(items);
    setSelection(null);
  }
  // ...
}
```

- item을 저장하는 것이 아닌 id를 저장함으로써 해결

```javascript
function List({ items }) {
  const [isReverse, setIsReverse] = useState(false);
  const [selectedId, setSelectedId] = useState(null);
  // ✅ 최고예요: 렌더링 중에 모든 것을 계산
  const selection = items.find((item) => item.id === selectedId) ?? null;
  // ...
}
```

<br/>

## 연쇄적으로 state를 조정해야하는 경우

- setCard => 리렌더링 => setGoldCardCount => 리렌더링 => setRound => 리렌더링 => setIsGameOver => 리렌더링

- 매우 비효율적이고 새로운 요구사항에 대처하기도 힘듬

```javascript
function Game() {
  const [card, setCard] = useState(null);
  const [goldCardCount, setGoldCardCount] = useState(0);
  const [round, setRound] = useState(1);
  const [isGameOver, setIsGameOver] = useState(false);

  // 🔴 피하세요: 서로를 트리거하기 위해서만 state를 조정하는 Effect 체인
  useEffect(() => {
    if (card !== null && card.gold) {
      setGoldCardCount(c => c + 1);
    }
  }, [card]);

  useEffect(() => {
    if (goldCardCount > 3) {
      setRound(r => r + 1)
      setGoldCardCount(0);
    }
  }, [goldCardCount]);

  useEffect(() => {
    if (round > 5) {
      setIsGameOver(true);
    }
  }, [round]);

  useEffect(() => {
    alert('Good game!');
  }, [isGameOver]);

  function handlePlaceCard(nextCard) {
    if (isGameOver) {
      throw Error('Game already ended.');
    } else {
      setCard(nextCard);
    }
  }
```

- 렌더링 중에 계산 가능한 상태는 분리

```javascript
function Game() {
  const [card, setCard] = useState(null);
  const [goldCardCount, setGoldCardCount] = useState(0);
  const [round, setRound] = useState(1);

  // ✅ 렌더링 중에 가능한 것을 계산합니다.
  const isGameOver = round > 5;

  function handlePlaceCard(nextCard) {
    if (isGameOver) {
      throw Error('Game already ended.');
    }

    // ✅ 이벤트 핸들러에서 다음 state를 모두 계산합니다.
    setCard(nextCard);
    if (nextCard.gold) {
      if (goldCardCount <= 3) {
        setGoldCardCount(goldCardCount + 1);
      } else {
        setGoldCardCount(0);
        setRound(round + 1);
        if (round === 5) {
          alert('Good game!');
        }
      }
    }
  }
```
