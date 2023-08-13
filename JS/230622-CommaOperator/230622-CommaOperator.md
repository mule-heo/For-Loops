# 6월 22일 목요일 Comma Operator(,)  퀴즈입니다.

console.log 에서 무엇을 출력할까요?

```
let x = 5;

function addFive(num) {
  return num + 5;
}
x = (x++ , x = addFive(x), x *= 2, x -= 5, x += 10);
console.log(x)
```

<br><hr><br>

- let x = 5 -> 5
- x++ -> x = x + 1 -> 현재 평가에는 반영되지 않으므로 5, 다음 평가부터는 6
- x = addFive(x) -> 6 + 5 = 11
- x *= 2 -> 11 * 2 = 22
- x -= 5 -> 22 - 5 = 17
- x += 10 -> 17 + 10 = 27

괄호 안의 `(x++, x = addFive(x), x *= 2, x-= 5)`를 차례로 평가하고 할당하는 과정을 거친 뒤 최종적으로 반환된 27을 다시 `x`에 할당합니다.

최종 결과는 27이 됩니다.

만약 괄호 안에 있는 식에 할당 연산자를 사용하지 않았다면 그 부분은 누적되지 않습니다.

```
let x = 5;

function addFive(num) {
  return num + 5;
}
x = (x++ , addFive(x), x * 2, x - 5, x + 10);
console.log(x)
```

최종 결과는 16이 됩니다!

- let x = 5 -> 5
- x++ -> x = x + 1 -> 현재 평가에는 반영되지 않으므로 5, 다음 평가부터는 6
- addFive(x) -> 6 + 5 = 11 (x에 재할당되지 않음)
- x * 2 -> 6 * 2 = 12 (x에 재할당되지 않음)
- x - 5 -> 6 - 5 = 1 (x에 재할당되지 않음)
- x + 10 -> 6 + 10 = 16

괄호의 식 중 최종적으로 평가된 것은 `x + 10`입니다. 따라서, `x = (...)`의 식에서 괄호 안의 평가 결과는 16이 되어 `x = 16`으로 재할당됩니다.

추가

- 증감식 `++x`와 `x++`의 차이
  - `++x`는 `x + 1`로 재할당한 뒤 평가를 진행합니다. `++x`는 식 안에서 `x + 1`이 됩니다.
  - `x++`는 평가를 먼저 진행한 후 `x + 1`로 재할당합니다. `x++`는 식 안에서 `x`가 됩니다.

자세한 정보는 여기

- Comma Operator

    https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comma_operator

    > Comma Operator는 왼쪽부터 오른쪽으로 식을 평가하고, 최종 식의 결과를 반환합니다.

    할당보다도 낮은 연산 우선순위를 가집니다.