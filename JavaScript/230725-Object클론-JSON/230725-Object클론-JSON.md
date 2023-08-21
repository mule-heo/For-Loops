# 7월 25일 화요일 Object 클론에 대한 퀴즈입니다.

```
const a = { 
  stringField: 'Joe',
  nestedField: {field: 'Nested'}
};
const b = JSON.parse(JSON.stringify(a));
b.stringField = 'Bob';
b.nestedField.field = 'Changed';
console.log(
  a.stringField,
  a.nestedField.field
);
```

A: Joe Nested

B: Bob Changed

C: Joe Changed

D: Bob Nested

<br><hr><br>

정답 A: Joe Nested

JSON.stringify 메서드는 원시 자료형, 참조 자료형 상관없이 하나의 문자열로 변환하는 메서드입니다. 이 문자열에 저장된 객체나 배열은 다시 객체나 배열로 되돌리기 위한 표현 형식을 유지하고 있을 뿐 기존 객체, 배열에 대한 참조를 가지고 있는 것은 아닙니다.

이렇게 JSON 문자열로 변환되었던 것을 JSON.parse 메서드를 사용하여 원래의 자료와 동일한 형태로 복원합니다. 하지만, 기록된 문자열을 통해 형태만 복원한 것일 뿐 기존 객체나 배열에 대한 참조는 유지하고 있지 않기 때문에 전부 새로운 객체, 배열로써 반환됩니다.

따라서, a와 b는 실제 데이터의 내용만 같고 서로 같은 참조를 가지고 있는 부분은 단 하나도 없으므로 b에서 어떠한 수정을 가해도 원본인 a에는 영향을 미치지 않습니다.


참고

- JSON.stringify()

  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify

- JSON.parse()

  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse