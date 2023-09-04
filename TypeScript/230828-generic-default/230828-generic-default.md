# 8월 28일 월요일 제네릭 파라미터 디폴트 표현 (타입 매개변수 디폴트)

1. 제네릭 타입에서 `<T = DefaultType>` 표현은 무엇을 뜻하나요?

    답: 제네릭으로 선언된 타입 T에 대하여 별도의 타입을 명시하지 않았고 타입스크립트에 의해 별도로 추론되지도 않는 경우 T의 타입이 DefaultType으로 결정됨을 의미합니다.

2.

```
interface Component<T1, T2> {
  name: T1;
  props: T2;
  log: () => void;
}

const button: Component = {
  name: "Button",
  props: {
    text: "Save",
  },
  log: () => console.log("Save button"),
};
```

Component 타입을 제네릭 타입으로 만들어주세요. 기본 디폴트 타입(`<T = DefaultType>` ) 을 사용해주세요.

```
console.log(button.props.text);
console.log(button.props.text2); // <---에러가 발생해야합니다.
```

```
interface Component<T1 = string, T2 = { text: string } > {
  name: T1;
  props: T2;
  log: () => void;
}
```

button.props.text2에 접근하였을 때에는 에러가 발생해야 하므로 Component 타입을 사용할 때에 전달한 타입이 없으면 T1에는 string, T2에는 { text: string }이 props의 타입으로 사용되도록 디폴트 타입을 추가하였습니다.

3.

```
function firstOrNull<T>(array: T[]): T | null {
  return array.length === 0 ? null : array[0];
}

const first = firstOrNull([1, 2, 3]);
console.log(first);
```

제네릭 타입을 사용하시되, 기본 디폴트 타입을 추가해주세요.

답

```
function firstOrNull<T = any>(array: T[]): T | null {
  return array.length === 0 ? null : array[0];
}
```

위의 경우는 입력된 인자의 타입으로부터 T의 타입이 자동으로 추론되는 상황이므로 T에 그 어떤 디폴트 타입을 전달하더라도 사용되지는 않습니다. 

인자로부터 추론된 타입이 디폴트 타입에 우선한다는 사실을 알게 되었습니다.

4. 디폴트 타입을 사용에 대한 의견을 알려주세요.

    일반 함수에서 유용한가요? 타입이 느슨해지는가요? 아니면 강력해진다고 생각하나요?

    답: 입력과 반환 타입이 명확한 일반 함수에서는 제네릭 타입의 디폴트 타입을 사용하는 것이 그다지 유용하지 않습니다. 제네릭 타입은 일반적으로 함수의 전달 인자로부터 추론되므로 디폴트 타입이 적용될 여지가 없습니다.

    디폴트 타입이 적용되도록 하기 위해 함수의 인자를 제거해 보았으나 함수의 인자가 없으면 전달 인자의 타입 유연성을 위해 사용되는 제네릭 타입을 적용할 이유가 없음을 확인했습니다.

출제 레퍼런스: https://learntypescript.dev/06/l6-generic-parameter-defaults