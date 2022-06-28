## 객체의 키 접근법

자바스크립트 객체를 다음과 같이 만들었다.
출력값을 입력하시오. (출력값은 공백을 넣지 않습니다. )

```js
var d = {
  height: 180,
  weight: 78,
  weight: 84,
  temperature: 36,
  eyesight: 1,
};

console.log(d['weight']);
```

여기서 어떻게 접근해야할까. 결과는 84가 나온다.
객체에 접근할때 . 접근자와 []접근자를 사용한다.
[] 접근자로 가져올떄는 키값이 중복 되었을 경우 키값을 입력했을때 동일한 키값의 가장 마지막 키값이 가져와진다.