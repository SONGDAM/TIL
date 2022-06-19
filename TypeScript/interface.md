객체는 object라는 타입으로 정의할 수 있다.

```ts
let user: object;

user = {
  name: 'xx',
  age: 30,
};
```

이렇게 property를 정의해서 객체를 정의하고자 할 떄는 interface를 사용한다.

```ts
interface User {
  name: string;
  age: number;
}

let user: User = {
  name: 'xx',
  age: 30,
};
```

만약 여기서 user에 gender라는 속성이 추가된다면 타입스크립트는 오류를 표시한다. 이과정에서 ?를 사용해 optional하게 사용할 수 있는데

```TS
interface User {
  name: string;
  age: number;
  gender? :string;
}
```

interface를 gender?로 정의하면 더 이상 오류가 나오지 않는다.
읽기전용 속성으로 사용할 수도 있다.

```TS
interface User {
 name: string;
 age: number;
 gender? :string;
 readonly birthYear: number;
}

let user : User = {
   name: 'xx',
   age: 30,

}
```

함수도 정의 가능하다.

```TS
interface Add {
    (num1:number, num2:number): number;

}

const add : Add = (x,y) : number =>  {
    return x + y;
}

```

```ts
interface IsAdult {
  (age: number): boolean;
}

const a: IsAdult = (age) => {
  return age > 19;
};
```

인터페이스를 클래스로도 정의할 수 있다.
implements 키워드를 사용한다.
extends와는 조금 다른 개념인 것 같다.

```ts
interface Car {
  color: string;
  wheels: number;
  start(): void;
}

class Bmw implements Car {
  color;
  wheels = 4;

  constructor(c: string) {
    this.color = c;
  }

  start() {
    console.log('start~~');
  }
}

const b = new Bmw('color');
```

extends키워드를 사용해 상속도 가능하다.

```ts
interface Benz extends Car {
  door: number;
  stop(): void;
}

const benz: Benz = {
  color;
  wheels = 4;

  constructor(c: string) {
    this.color = c;
  }
  door: 5,
  stop() {
    console.log('stop');
  },
};
```
