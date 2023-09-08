# 9월 7일 목요일

실습링크 https://codesandbox.io/s/non-null-operator-u4p7j?file=/src/index.ts:0-228

※ 실습 링크의 코드로 수정하여 진행하였습니다. 본래 문제 페이지의 코드로는 타입 오류가 발생하지 않습니다.

```ts
function duplicate(text: string | null) {
  let fixString = function() {
    if (text === null || text === undefined) {
      text = "";
    }
  };
  fixString();

  return text.concat(text);
}
```

> 리턴 문에서 타입 오류가 발생하는 이유를 알려주세요. (엄격모드 strictNullChecks 에 대해 알려주세요)

답: 리턴 문에서 타입 오류가 발생하는 이유는 text가 null일 수 있기 때문입니다. if문에서 null과 undefined 여부를 검사하는 타입 가드를 거쳤지만 이는 조건문 안에서만 유효하므로 리턴 문에는 적용되지 않습니다.

핵심은 string의 값이 null 또는 undefined인 경우 text를 빈 문자열로 할당되어 있어 논리적으로 리턴 문에 다다랐을 때에는 null 또는 undefined일 수 있는 가능성이 없다는 점입니다.

추가적인 함수 호출없이 코드를 실행했을 때에는 리턴 문에서의 text가 string 타입으로 추론되었지만, 함수를 통해 처리하니 더이상 string 타입이 반영되지 않았습니다. 함수 내부에서 정의된 fixString 함수는 duplicate 함수의 전달인자인 text에 접근하여 작업을 수행하였지만 타입은 string으로 추론되지 않았음을 확인할 수 있었습니다.

```ts
function duplicate(text: string | null) {
  if (text === null || text === undefined) {
    text = "";
  }

  return text.concat(text); // 타입이 string으로 추론되어 타입 오류가 발생하지 않습니다.
}
```

```ts
function duplicate(text: string | null) {
  let fixString = function() {
    if (text === null || text === undefined) {
      text = "";
    }
  };
  fixString();

  return text.concat(text); // 타입이 string으로 추론되지 않아 타입 오류가 발생합니다.
}
```

fixString의 타입은 () => void이므로 이 함수의 호출이 특정 타입의 추론에 도움이 되지 않는다는 점, fixString은 자신의 전달인자가 아닌 클로저의 특성 상 접근 가능한 외부함수의 전달인자를 이용했다는 점을 중심으로 타입스크립트 자체적으로 이루어지는 타입 추론이 어느 정도 복잡한 수준까지 이루어지는지 공부해 보면 좋을 것 같습니다.

물론 공부를 할 수 있으면 좋지만 이와 같이 타입 추론이 불가능한 상황을 일일이 기억하는 것보다 개발자는 타입에 대한 정보를 정확하게 알고 있음에도 불구하고 타입 추론이 제대로 일어나지 않는 상황에 처했을 때 타입 단언을 사용하는 것이 효율적일 것임을 느꼈습니다.

타입스크립트의 strictNullChecks 옵션은 변수가 null 또는 undefined일 가능성이 있을 때(구체적인 값이 없을 때)에 해당 변수의 사용을 제한하므로 런타임 오류를 방지하는 데에 효과적입니다.

> null 혹은 undefined가 아님을 선언하려면 어떻게 해야할까요? (! 마크 사용)

답

```ts
function duplicate(text: string | null) {
  let fixString = function() {
    if (text === null || text === undefined) {
      text = "";
    }
  };
  fixString();

  return text!.concat(text!);
}
```

text를 사용하는 부분마다 text의 뒤에 !(null이 아님을 단언하는 연산자)를 사용합니다.


출제 레퍼런스: https://learntypescript.dev/07/l2-non-null-assertion-operator

참고

- strictNullChecks

    https://www.typescriptlang.org/tsconfig#strictNullChecks