# 7월 18일 Promise-Catch 문제 입니다.

1\)

```
var p = new Promise((resolve, reject) => {
  reject(Error('The Fails!'))
})
p.catch(error => console.log(error.message))
p.catch(error => console.log(error.message))
```

A: error.message 가 한번 출력

B: error.message 가 두번 출력

C: UnhandledPromiseRejectionWarning

D: 프로세스가 중단됨

<br><hr><br>

정답 B: `error.message`가 두 번 출력

위의 코드는 연속된 체이닝을 통해 구현한 형태가 아니라 `p`라는 Promise 객체에 대하여 서로 다른 체인을 두 가지 형성한 형태입니다. 따라서 두 `catch` 메서드는 서로 다른 체인에 해당하며, 두 `catch` 메서드 모두 실행되어 `error.message`가 두 번 출력됩니다.

아래와 같이 두 `catch` 메서드를 동시에 체이닝한 경우에는 `error.message`가 한 번만 출력됩니다.

```
new Promise((resolve, reject) => {
  reject(Error('The Fails!'))
})
.catch(error => console.log(error.message))
.catch(error => console.log(error.message));
```

선택한 오답 A: `error.message`가 한 번 출력

Promise 객체의 콜백 함수를 실행하던 중 reject되어 과정을 종료하면 `catch` 메서드에서 오류를 제어합니다. `catch` 메서드를 여러 개 사용하더라도 순서상 가장 처음 읽히는 catch문을 실행하고 Promise 체이닝을 종료하므로, `error.message`가 한 번만 출력됩니다.

<hr>

2\)

```
var p = new Promise((resolve, reject) => {
  return Promise.reject(Error('The Fails!'))
})
p.catch(error => console.log(error.message))
p.catch(error => console.log(error.message))
```

A: error.message 가 한번 출력

B: error.message 가 두번 출력

C: UnhandledPromiseRejectionWarning

D: 프로세스가 중단됨

<br><hr><br>

정답 D: 프로세스가 중단됨

`return Promise.reject(Error('The Fails!'))` 코드를 실행하는 과정에서 에러가 throw됩니다. 표현식에 즉시 체이닝하여 오류에 대한 예외처리를 수행하지 않는 한 오류가 발생합니다.

프로세스가 중단되는 이유를 분석해 보면 다음과 같습니다.

- `var`로 선언한 변수 `p`에 Promise 객체를 할당하고자 합니다.
- 이 객체는 `Promise.reject` 메서드를 사용하여 결과가 항상 `rejected`가 되는 Promise를 결과로 하는 Promise를 반환합니다. (결과가 Promise 객체인 Promise 객체)
- 결과로 반환되는 `Promise.reject`의 실행 결과는 `Error('The Fails!')`입니다.
- 결과로 반환되는 `Promise.reject`에 대한 오류 예외처리 메서드를 사용하지 않았습니다.
- 오류에 대하여 예외처리를 하지 않았으므로 `Promise.reject(Error('The Fails!))`에 대하여 반드시 오류를 발생시킵니다.
- reject에 대한 예외처리가 되어 있지 않은 채로 Promise를 반환하면 꼭 Error 객체가 아닌 다른 타입의 값을 반환하더라도 오류가 발생합니다.

위 문제의 실행 결과는 단순하게 다음 코드를 실행한 결과와 같습니다.

`Promise.reject(Error('The Fails!'))`

<br>

선택한 오답 B: error.message가 두 번 출력

1번 문제에서의 코드와 다른 점은 `reject` 메서드를 호출할 때 `Promise.reject`로 직접 호출했다는 점입니다. 콜백 함수로 전달되는 `reject`는 Promise가 가지는 `reject`와 동일하므로 결과는 동일합니다.

`Promise.reject` 메서드는 Promise의 콜백 함수로 전달되는 `reject`와 달리 단순한 결과값이 아닌 새로운 Promise 객체를 반환합니다.


참고

- Promise

  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise

- Promise.reject()

  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject

