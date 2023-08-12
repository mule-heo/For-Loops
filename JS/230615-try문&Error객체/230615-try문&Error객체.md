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
```
다음 보기 중 하나를 고르세요. 그 이유도 알려주세요.

a. 'Hi, there!'

b. 'bar is not defined'

c. TypeError: Cannot read properties of undefined (reading 'message')

<hr>

## 다음 문제입니다.

아래  코드는 무엇을 출력할까요?

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
```