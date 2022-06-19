```TS
let age:number = 30;
```

이런식으로 타임을 명시해야되지만 명시하지 않아도 타입스크립트는 age의 타입을 number로 추론하기도한다.

true,false 값을 명시할때는 boolean 타입을 명시해주어야한다.

```TS
let isAdult:boolean = true;

```

배열을 명시할때는 해당 배열의 자료형을 명시하거나
Array<해당자료형>의 형태로 명시한다.

```TS
let a : number[] = [1,2,3];
let a2 : Array<number> = [1,2,3];
```

Tuple

```ts
let b: [string, number];
```

index별로 타입이 다를 때 이용할 수 있다.
저배열안의 0번째 index는 string이고 1번째 index는 number라는 것을 알 수 있다.

void,never

void는 함수에서 아무것도 반환하지 않을떄 사용한다.
간단히 hello world!를 출력하는 함수를 예로 들어보겠다 .

```TS
const printLog ():void => console.log('hello world');
```

never는 항상 에러를 반환하거나 영원히 끝나지 않는 함수를 얘기한다.

```TS
const showError = ():never => {
    throw new Error();
}

const infLoop():never => {
    while(true){
        //do something;

    }
}
```

enum

비슷한 값들끼리의 집합이라고 생각하면 된다.

```TS
enum Os {
    window = 'win',
    Ios = 'Ios',
    Android = 'Android'
}
```

enum에 수동으로 값을 주지 않으면 자동으로 0부터 1씩주면서 할당한다. 만약 window에 12를 주면 Ios는 13 Android는 14가 된다. enum에는 number가 아닌 string도 할당가능하다.

```TS
let myOS:Os
```

위와 같이 선언해두면 Os안에 있는 객체만 입력할 수 있다. 특정 값만 강제하고 싶을떄, 또는 공통점이 있을떄 enum을 사용하면 좋다.
