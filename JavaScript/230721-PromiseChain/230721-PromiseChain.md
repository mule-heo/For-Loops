# 7월 21일 금요일 promise chain에 대한 퀴즈입니다.

출력 결과를 알려주세요.

```
const promise = new Promise(res => res(2));
promise.then(v => {
        console.log(v);
        return v * 2;
    })
    .then(v => {
        console.log(v);
        return v * 2;
    })
    .finally(v => {
        console.log(v);
        return v * 2;
    })
    .then(v => {
        console.log(v);
    });
```

<br><hr><br>

정답: 2 4 undefined 8

- 처음 생성한 Promise 객체는 반드시 성공적으로 이행되며, 2라는 값을 결과로 가지고 있습니다.
- 2라는 결과를 가진 Promise를 변수 promise에 할당합니다.
- then: Promise가 가진 값을 출력한 뒤 2를 곱하여 반환합니다. -> 2 출력 후 4 반환
- then: 다시 Promise가 가진 값을 출력한 뒤 2를 곱하여 반환합니다. -> 4 출력 후 8 반환
- finally: 앞선 Promise 체인의 이행/거절 여부와 관계없이 실행되는 코드 블록입니다. 이행/거절 결과와 관계없이 실행되기는 하나 앞선 Promise의 처리 결과를 판단할 수 없습니다. then, catch 메서드와 달리 콜백 함수로 전달되는 값이 없으므로 v를 인자로 콘솔에 출력하고자 하였을 때 undefined가 출력됩니다.
- then: 8을 출력합니다.

<hr>

선택한 오답: 2 4 8 16

- finally는 이전 Promise의 실행 결과를 활용할 수 없으므로 값을 출력한 후 2를 곱하여 반환하는 과정이 한 단계 생략되고 undefined를 출력하는 과정으로 대체됩니다. 또한, finally의 콜백 함수가 반환하는 값은 Promise 체인에 반영되지 않습니다.


참고

- Promise.prototype.finally()

    https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/finally