# 9월 18일 월요일 타입 매핑

아래와 같이 기존 타입 정보를 매핑해 새로운 타입을 생성할 수 있습니다.

```ts
type MappedTypeName = { [K in UnionType]: ExistingType };
```

실습 링크: https://codesandbox.io/s/keyof-generics-gl2vm

```ts
interface Form<T> {
  values: T;
  errors: any;
}

const contactForm: Form<{ name: string; email: string }> = {
  values: {
    name: "Bob",
    email: "bob@someemail.com"
  },
  errors: {
    emailAddress: "Invalid email address"
  }
};
console.log(contactForm);
```

contactForm에서 개선할 점을 먼저 찾아보세요.

답: 현재 email 값의 오류 메시지를 표현하기 위해 errors 객체에 email이 아닌 emailAddress 속성을 사용하였습니다. errors의 key로써 values에 존재하는 key만을 사용한다면 일대일 대응이 이루어지므로 관리가 용이해집니다.

타입 에러가 발생하지 않은 이유는 무엇인가요?

답: 현재 errors의 타입이 any로 되어 있어 key, value 모두 자유롭게 사용하고 할당할 수 있습니다. errors 객체에 emailAddress라는 key를 사용하였음에도 불구하고 개발자의 의도를 배제한 프로그램 자체에는 오류가 없으므로 타입 오류를 발생시키지 않습니다.

errors 타입을 any을 매핑된 타입을 사용할 수 있도록 업데이트 해주세요. 이후 타입 오류를 살펴보세요.

```ts
interface Form<T> {
  values: T;
  errors: {[key in keyof T]?: string};
}
```

답: errors의 객체는 타입 T가 가지는 key만을 사용할 수 있으며, value로는 string 타입만을 사용할 수 있도록 하였습니다. 또한, 오류 메시지는 항상 존재하는 것이 아니라는 점을 감안하여 옵션 연산자를 포함하여 errors 객체의 값을 생략할 수 있도록 하였습니다.

새로운 프로퍼티를 자유롭게 추가해보세요. (values와 errors에 새로운 프로퍼티를 업데이트해야합니다)

전체 코드

```ts
interface Form<T> {
  values: T;
  errors: {[key in keyof T]?: string};
}

const contactForm: Form<{ name: string; email: string; phone: string }> = {
  values: {
    name: "Bob",
    email: "bob@someemail.com",
    phone: '01010101010'
  },
  errors: {
    email: "Invalid email address"
  }
};
```

Form 타입의 제네릭 파라미터로 전달된 타입에 따라 values의 형태와 errors가 가질 수 있는 key가 제한됩니다. errors 객체의 모든 요소는 옵셔널이므로 errors 객체는 빈 객체일 수 있습니다.

출제 레퍼런스: https://learntypescript.dev/08/l2-mapped-type