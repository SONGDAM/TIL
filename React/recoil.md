<h1>Recoil로 상태관리하기</h1>

<br>

날씨에 따른 룩을 추천하는 페이지를 팀원과 함께 만들고 있는데 유저정보나 이미지 실시간 날씨 데이터들을 모든 컴포넌트에서 혹은 조금 멀리(?) 있는 컴포넌트에서 사용해야하는 상황이었다.

이미지는 firebase storage에서 가져오고 그 외에도
외부에서 fetching하는 데이터가 많기 때문에 자연스럽게 페이지의 성능이 떨어지는 게 눈에 보였다.

Context API를 사용중이지만 wrapper가 늘어날 수록 더 성능이 느려졌다.

그래서 결국은 상태관리 라이브러리를 도입해야된다고 생각하게 되었고 가장 많이 사용하는 Redux도 고민했지만 그중에 상대적으로 러닝커브가 낮고 코드양이 상대적으로 적은 리코일을 생각하게 되었다.

Recoil을 관통하는 개념은 크게 보면 Atom과 Selector가 있는데 각각의 Atom에서 State를 가져다가
Hooks처럼 사용할 수 있다.

그전에 index.js에 RecoilRoot를 import 해야한다.

```JavaScript
import ReactDOM from 'react-dom/client';
import { atom, RecoilRoot, selector, useRecoilState, useRecoilValue } from 'recoil';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <RecoilRoot>
    <App />
  </RecoilRoot>
);

```

<br>

Recoilroot를 최상위 컴포넌트 위에 감싸면 Recoil을 사용할 수 있다.

Recoil에서는 아래의 그림과 같이 각각의 상태의 단위인 atom을 사용하는데,

<br>

<img src="https://velog.velcdn.com/images%2Fjuno7803%2Fpost%2F4ffbf062-fd53-4b33-9441-d1127c9033ef%2Fimage.png" width='600' height='400' align='center'>

<br>

```javascript
import { atom } from 'recoil';

export const countState = atom({
  key: 'countState',
  default: 0,
});
```

<br>

위와 같이 atom에는 각각의 unique한 키와 default한 값이 있다.
atom을 import 하면 어느 컴포넌트에서든 상태를 사용할 수 있다. 해당 컴포넌트에서 atom이 업데이트 되면, 해당 atom을 구독하고 있던 모든 컴포넌트들의 state가 새로운 값으로 리렌더된다. 단, 같은 페이지내에서만 상태의 변화가 구독된다.

아래는 간단한 카운터를 만드는 코드이다.

<br>

```jsx
import { useRecoilState } from 'recoil';
import Another from './Another';
import { countState } from './atom/counterState';

function App() {
  const [count, setCountState] = useRecoilState(countState);

  const onClickPlus = () => {
    setCountState((prev) => prev + 1);
  };

  const onClickMinus = () => {
    setCountState((prev) => prev - 1);
  };

  return (
    <div className='App'>
      <button onClick={onClickPlus}>increase</button>
      {count}
      <button onClick={onClickMinus}>decrease</button>
      <Another />
    </div>
  );
}

export default App;
```

React의 useState와 같이 첫번쨰는 상태의 값, 두번째는 상태를 업데이트 할 수 있는 함수가 있다.
useRecoilState라는 메서드를 활용하고 atom을 사용하여 state를 관리한다.

또한 업데이트함수만 사용할 수 있는 메서드인 useSetRecoilState 메서드도 존재한다.

<hr>

<br>

**selector**

> A selector represents a piece of derived state

<br>

selector는 공식문서의 설명과 같이 파생된 state를 저장하고 있다.

<br>
공식문서의 소개글이다.

핵심은
selector는 순수함수 여야 한다는 것 입니다.
순수함수란, 같은 입력이 들어오면, 해당 입력에 대한 출력은 항상 같은 함수라는 뜻을 가지고 있다.

```js
import { selector } from 'recoil';
import { countState } from '../atom/counterState';

export const countNumberSelector = selector({
  key: 'countNumberState',
  get: ({ get }) => {
    const countSubscribe = get(countState);
    const AddcountSubscribe = countSubscribe + 100;
    return {
      countSubscribe,
      AddcountSubscribe,
    };
  },
  set: ({ set }, newValue) => {
    const divideCountState = newValue / 10;
    set(countState, divideCountState);
  },
});
```

또한 selector는 readonly 한 RecoilValueReadOnly 객체로서 값을 새로 작성할 수 없다.
하지만 set함수를 정의하면 writeable한 객체로 useRecoilState를 통해 상태를 관리할 수 있다.

get과 set의 개념이 아직 익숙하지 않아서
get과 set의 동작을 정의하는 코드를 짜보았다 ㅠ

get을 통해 countState을 가져와서 구독하고 Addcountsubscribe를 통해 기존 countState에 100을 더하고 return을 통해 새로운 상태를 리턴한다.

또 set을 통해서 newValue를 set하는 함수를 정의해주었고

```js
const [, setDivideNumber] = useRecoilState(countNumberSelector);

const divide = () => setDivideNumber(Value);
```

위와 같은 형식으로 selector를 사용할 수 있다.

recoil의 비동기 상태는 react의 suspense를 통해 이루어지는데

```js
import { selector, useRecoilValue } from 'recoil';

const myQuery = selector({
  key: 'MyDBQuery',
  get: async () => {
    const response = await fetch(getMyRequestUrl());
    return response.json();
  },
});

function QueryResults() {
  const queryResults = useRecoilValue(myQuery);

  return <div>{queryResults.foo}</div>;
}

function ResultsSection() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <QueryResults />
    </Suspense>
  );
}
```

fallback이라는 property를 통해서 비동기처리가 완료될떄까지 fallback에 있는 컨텐츠를 보여주고 비동기처리가 완료되면 QueryResult를 불러온다.

비동기처리의 방식이 조금 제한적이라 다른 라이브러리도 더 찾아봐야겠다는 생각이든다. 그래서 react-query를 사용하는걸지도...

하지만 난 리코일이 직관적이라 너무 좋다..
