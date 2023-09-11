# 9월 6일 수요일 타입 제한

1.

```ts
type Animal = {
  name: string;
  legs?: number;
};
function addLeg(animal: Animal) {
  animal.legs = animal.legs + 1; // 오류가 발생합니다.
}
```

legs 타입을 해결하려면 어떻게 해야하나요? 

답: animal이 가지는 legs 속성의 값이 undefined인지 검사하는 if문을 추가합니다.

```ts
function addLeg(animal: Animal) {
  if (animal.legs !== undefined){
    animal.legs = animal.legs + 1;
  }
}
```

2.

실습코드
https://codesandbox.io/s/type-assertions-efsyc

```ts
const button = document.querySelector(".go");
```

button의 타입은 무엇인가요?

답: button의 타입은 Elment 또는 null입니다.

버튼을 비활성화하는 코드를 추가해주세요. (disabled = true)
타입 오류가 발생하는 이유가 무엇인가요? 

```ts
const button = document.querySelector(".go");
button.disabled = true;
```

답: 첫째, button 변수는 null일 가능성이 있기 때문에 button의 disabled 속성으로 접근하고자 할 때에 안전하지 않습니다. 둘째, Element 타입은 disabled 속성을 가지지 않습니다. 따라서, 두 경우 모두 타입 오류가 발생합니다. button 변수에는 변수가 null일 가능성이 있다는 오류가, disabled 속성에는 Element 타입에 disabled 속성이 존재하지 않는다는 오류가 발생합니다.

3.

위의 실습에서 타입 어셜션의 <> 표현을 사용해
button 타입을 HTMLButtonElement로 만들어 주세요.

```ts
<TypeName>expression;
```

```ts
const button = <HTMLButtonElemnt>document.querySelector(".go");
```

답: 위와 같이 표현하여 HTMLButtonElement로 확정할 수 있습니다. 하지만 사용이 권장되지 않는 방법이라고 합니다. 홑화살낫표의 사용이 주로 제네릭 타입에 사용되고 있다는 점으로 미루어 보아 타입 단언에도 홑화살낫표를 사용하게 되면 개발자가 코드를 읽으면서 둘을 구분하여야 하는 부담이 추가될 수 있다는 생각이 듭니다.

As 키워드를 사용하여 타입을 수정해주세요.

```ts
expression as TypeName;
```

```ts
const button = document.querySelector(".go") as HTMLButtonElement; 
```

답: as 키워드의 사용을 통하여 button을 HTMLButtonElement 타입으로 간주하도록 합니다.

공통적으로 타입 단언은 실제 데이터가 null일 가능성이 사라지는 것이 아니라 타입 검사 과정에만 개입하여 조작하는 것이므로 항상 주의하여야 합니다.

출제 레퍼런스: https://learntypescript.dev/07/l1-type-assertions