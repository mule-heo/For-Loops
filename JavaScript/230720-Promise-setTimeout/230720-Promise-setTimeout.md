# 7월 20일 목요일 Promise-setTimeout 문제 입니다.

```
const f1 = () => console.log('f1');
const f2 = () => console.log('f2');
const f3 = () => console.log('f3');
const f4 = () => console.log('f4');

f4();

setTimeout(f1, 0);

new Promise((resolve, reject) => {
    resolve('Boom');
}).then(result => console.log(result));

setTimeout(f2, 2000);

new Promise((resolve, reject) => {
    resolve('Sonic');
}).then(result => console.log(result));

setTimeout(f3, 0);

new Promise((resolve, reject) => {
    resolve('Albert');
}).then(result => console.log(result));
```

A: f4, Boom, Sonic, Albert, f1, f3, f2

B: f4, f1, Boom, f2, Sonic, f3, Albert

C: f4, Boom, Sonic, Albert, f3, f1, f2

D: f4, Boom, Sonic, Albert, f1, f2, f3

<br><hr><br>

정답 A: f4, Boom, Sonic, Albert, f1, f3, f2

우선 f4는 동기적으로 처리되고 순서상 가장 앞서므로 의심의 여지없이 가장 먼저 출력됩니다.

나머지 f1, f2, f3은 setTimeout을 거쳐 처리됩니다. f1, f3이 각각 0 밀리초, f2는 2000 밀리초 뒤에 실행되므로 async-await을 통해 f2 호출 부분과 f3 호출 부분 사이에서 처리를 일시적으로 중단하거나 f2의 값을 현저히 줄이지 않는 이상 이들 간의 처리 순서는 f1, f3, f2입니다.

이들 비동기 처리의 순서는 이전에 [230711-콜스택](../230711-콜스택/230711-콜스택.md)에서 살펴보았듯 임의의 시점까지 실행되지 않고 싱글 스레드에서의 앞선 작업이 처리될 때까지 큐에 등록되어 대기합니다. 

Promise 처리 순서는 'Boom', 'Sonic', 'Albert'입니다. 각각의 Promise 객체는 이들 문자열을 결과로 반환한 뒤 then으로 체이닝하여 결과를 콘솔에 출력합니다. 이들의 처리는 setTimeout의 처리에 우선합니다. Promise 객체를 생성하였으나 비동기적으로 처리되는 코드 블록은 포함되어 있지 않기 때문에 동기적으로 작동합니다. Promise 객체는 비동기 처리에 유용한 수단을 제공할 뿐이지 비동기적으로 처리될 부분이 없으면 비동기적으로 처리되지 않기 때문입니다.

따라서, 순서는 f4 - Promise 객체 - setTimeout 순으로 처리되며 이는 다음과 같습니다.

f4, Boom, Sonic, Albert, f1, f3, f2

코드 살짝 바꿔보기

- [Promise 객체에도 setTimeout을 적용하면 결과가 어떻게 될까?](./230720code.md)

핵심

Promise를 활용하였더라도 비동기적으로 처리되는 작업이 없으면 동기적으로 처리됩니다.

참고

- Promise

    https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise

- setTimeout

    https://developer.mozilla.org/en-US/docs/Web/API/setTimeout