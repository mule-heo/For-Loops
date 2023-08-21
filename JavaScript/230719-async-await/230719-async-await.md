# 7월 19일 수요일 asnyc-await 문제입니다.

```
async function f() {
  let result = 'first!';
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve('done!'), 1000);
  });

  result = await promise;

  console.log(result);
}

f();
```

A: first!

B: done!

C: JavaScript error

D: Something else

<br><hr><br>

정답 B: done!

async 키워드가 사용된 함수 안에서는 Promise에 대하여 await 키워드를 사용할 수 있습니다. await 키워드를 사용한 Promise는 Promise 이행/거절에 대한 결과를 가진 Promise 객체 자체가 아닌 결괏값만을 반환합니다.

또한, await 키워드를 사용한 경우, 해당 코드 블록이 처리되기 전까지 동기적인 처리가 일시적으로 중단되어 해당 Promise가 처리되기 전까지 대기합니다. 이러한 작동을 통하여 처리 순서가 보장되어야 하는 비동기 처리에 대하여 동기적인 처리가 가능해집니다.


참고

- async 함수

  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async_function

- await

  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/await

- async-await
  
  https://ko.javascript.info/async-await