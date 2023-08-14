# 7월 5일 수요일 [Object].prototype에 관한 퀴즈입니다.

```
String.prototype.lengthy = () => {
  console.log("hello");
};

let x = { name: "Vuong" };

delete x;

x.name.lengthy();
```

A: "Vuong";

B: "hello";

C: "undefined"

D: "ReferenceError"

<br><hr><br>

정답 B: 'hello'

String의 프로토타입에 'hello'를 출력하는 lengthy라는 화살표 함수를 새로이 할당하였습니다.

이후 x라는 객체를 생성한 뒤 다시 delete를 통하여 x를 제거하고자 하지만 let으로 선언된 변수 x는 delete 키워드의 영향을 받지 않습니다.

x.name은 String 타입이므로 String.prototype의 메서드로 정의한 lengthy를 사용할 수 있습니다.

lengthy를 호출한 결과 hello가 출력됩니다.

<br><hr><br>

선택한 오답 D: ReferenceError

x에 객체를 할당한 뒤 다시 delete를 통하여 x를 제거하였으므로 x라는 변수가 제거될 것이라고 예상하였습니다.

위의 예상에 따라, 변수 x에 대한 참조는 사라지고 x에 접근하려고 할 때 ReferenceError가 발생할 것이라고 판단하였습니다.


참고

- Object Prototypes

    https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes

- var, let, const 키워드를 통해 선언한 변수는 delete를 통해 삭제할 수 없습니다.

    https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete

- var, let, const 키워드 없이 사용한 변수는 delete를 통해 삭제할 수 있습니다.
- [코드 실행 결과 - 변수 선언 키워드 유무 비교](230705code.md)