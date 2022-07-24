## concat을 활용한 문제풀기

concat을 활용하여 출력에 맞는 데이터 만들어내기

출력
2019/04/26 11:34:27

1. 내가 풀었던 문제 방식

```js
var year = '2019';
var month = '04';
var day = '26';
var hour = '11';
var minute = '34';
var second = '27';

var result = console.log(result); //빈칸을 채워주세요

let yymmdd = [];

const ymd = yymmdd.concat(year, month, day).join('/');


let time = [];

const hms = time.concat(hour, minute, second).join(':');

const result = `${mmyydd hms}`
```

정답은 concat 하나로 해결하는 것이다.

```js
var year = '2019';
var month = '04';
var day = '26';
var hour = '11';
var minute = '34';
var second = '27';
//concat() 메서드는 매개변수로 전달된 문자열을 메서드를 호출한 문자열에 붙여 새로운 문자열로 반환합니다.
var result = year.concat('/', month, '/', day, ' ', hour, ':', minute, ':', second);

console.log(result);
```
