# 6월 15일 목요일 자바스크립트 퀴즈입니다.

```
function hello() {
  try {
    bar('Hi, there!')
  }
  catch (error1) {
    console.log(error1.message)
  }
}

// hello 함수를 호출하는 부분까지 있어야 합니다!!!
hello();
```
다음 보기 중 하나를 고르세요. 그 이유도 알려주세요.

a. 'Hi, there!'

**b. 'bar is not defined'**

c. TypeError: Cannot read properties of undefined (reading 'message')

try문 내부에서 bar를 호출합니다. 하지만, bar는 정의된 적이 없으므로 오류가 발생하게 되고, 해당 오류 객체는 catch문으로 전달됩니다.

catch문에 전달된 오류 객체의 message 속성에 해당하는 'bar is not defined'를 콘솔에 출력합니다.


bar는 호출할 수 있는 변수가 아니라는 오류가 발생할 것으로 예상하였지만 선택지에 없었습니다. bar를 호출하기 이전에 그 어떠한 형태로도 정의된 적이 없으면 bar is not defined 오류가 발생한다고 이해하였습니다.

- 정의된 적이 없으면 'bar is not defined'
- 정의되었으나 함수로 정의되지 않았다면 'bar is not a function'

<hr>

## 다음 문제입니다.

아래 코드는 무엇을 출력할까요?

```
function hello() {
  try {
    bar('Hi, there!')
    console.log('Hello, I am here!')
  }
  catch (error1) {
    console.log('hello')
    console.log(error1)
    console.log(error1.message)
    console.log(error1.error)
    console.log(error1.name)
  }
}

// 호출
hello();
```

흐름상 bar를 호출하려고 시도하지만 bar를 정의한 적이 없으므로 실패합니다. bar 호출에 실패한 후 다음 line은 건너뛰고 catch문으로 넘어갑니다.

콘솔에는 다음의 내용들이 순서대로 출력됩니다.

- 'hello'
- 오류 객체(error1.name + ': ' + error1.message)
- 'bar is not defined'
- Error 객체에 대한 자료 참고 - Error 객체에 error 속성은 없으므로 undefined
- Error 객체에 대한 자료 참고 - 오류 이름 - ReferenceError

참고

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Error