# 7월 7일 금요일 getOwnPropertyNames에 관한 퀴즈입니다.

```
var languages = {
  name: ["elixir", "golang", "js", "php", { name: "feature" }],
  feature: "awesome",
};

let flag = languages.hasOwnProperty(Object.values(languages)[0][4].name);

(() => {
  if (flag !== false) {
    console.log(
      Object.getOwnPropertyNames(languages)[0].length <<
        Object.keys(languages)[0].length
    );
  } else {
    console.log(
      Object.getOwnPropertyNames(languages)[1].length <<
        Object.keys(languages)[1].length
    );
  }
})();
```

A: 8

B: NaN

C: 64

D: 12

<br><hr><br>

정답 C: 64

```
let flag = languages.hasOwnProperty(Object.values(languages)[0][4].name);
```

우선 `Object.values(languages)[0][4].name`은 `'feature'`가 되고, `'feature'` 또한 `languages`의 key 중 하나이므로 `true`가 반환됩니다.

그러므로 즉시 실행 함수에서 `if (flag !== false)` 조건을 만족하므로 해당 if문의 코드 블록이 실행됩니다.

`Object.getOwnPropertyNames(languages)[0]`, `Object.keys(languages)[0]` 모두 `'name'`을 반환할 것이라고 예상하면 둘 다 `length`는 4가 됩니다.

4 << 4 는 4에 2를 4번 곱한 것과 같습니다. 비트는 왼쪽으로 갈 수록 2씩 커지니까요.

<< 연산자는 비트를 왼쪽으로 한 칸 미는 연산자입니다.

따라서, 답은 **64**입니다.


참고

- Object.prototype.hasOwnProperty()

    hasOwnProperty 메서드는 인자로 전달된 문자열을 속성으로 가지고 있는지 확인하여 boolean 타입을 반환합니다.

    https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty

- Object.getOwnPropertyNames()

    getOwnPropertyNames 메서드는 인자로 전달된 객체의 속성을 배열 형태로 반환하되 숫자 형태의 속성이 먼저 입력되고, 문자열 형태의 속성은 그 다음 순서로 하여 반환합니다.

    https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames


