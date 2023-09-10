9월 4일 월요일 제네릭 타입 마지막 - 스프레드 연산자 

1

```ts
function merge(names: string[], scores: number[]) {
  return [...names, ...scores];
}
```

scores의 타입은 무엇인지 타입유추를 통해 알아보세요.

```ts
let scores = merge(["Bill", "Jane"], [8, 9]);
```

답: scroes의 타입은 string, number로 구성된 배열로 추론됩니다. `(string | number)[]`

2

타입을 더욱 강력히 제한하는 것에 대해 의견을 알려주세요.

```ts
[string, string, number, number]
```

답

- 위의 타입을 직접 입력하여 사용하는 경우

    위와 같은 형태로 string, number로 구성된 튜플 형태로 전달 인자의 타입 또는 함수의 반환 타입을 지정한다면 함수의 유연성이 떨어지므로 바람직하지 않습니다.

- 타입 추론을 통하여 위와 같은 반환 타입으로 추론되는 경우

    반환되는 배열의 정보가 더욱 상세해지므로 가독성이 향상됩니다.

```ts
["Bill", "Jane", 8, 9]
```

- 위의 타입을 직접 입력하여 사용하는 경우

    이전 예시에서는 string, number로 튜플을 구성하였지만 이번엔 리터럴 타입으로 튜플을 구성하였습니다. 위의 예시보다 경직된 타입을 가지게 되어 함수로써의 재사용성을 크게 해칩니다.

- 타입 추론을 통하여 위와 같은 반환 타입으로 추론되는 경우

    반환되는 배열의 정보가 string, number보다도 더욱 상세해지므로 가독성이 향상되고 함수의 실행 결과를 정확하게 예측할 수 있게 됩니다.



3

a.

```ts
function merge<Names extends string[], Scores extends number[]>(
  names: Names,
  scores: Scores
) {
  return [...names, ...scores];
}
```

답: `(string | number)[]`로 추론됩니다. 유의미한 차이를 보이지 않습니다.

b.

```ts
function merge<Names extends string[], Scores extends number[]>(
  names: [...Names],
  scores: [...Scores]
) {
  return [...names, ...scores];
}
```

타입을 고쳤을 때 scores의 타입은 어떻게 될까요?

```ts
let scores = merge(["Bill", "Jane"], [8, 9]);
```

답: b와 같이 제네릭 파라미터에 스프레드 문법을 적용하여 배열을 재생성하면 반환 타입이 리터럴 타입으로 추론됩니다. `['Bill', 'Jane', 8, 9]`

출제 레퍼런스: https://learntypescript.dev/06/l9-generic-spread