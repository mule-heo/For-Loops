# 8월 29일 화요일 제네릭 타입 파라미터 제약 extends 구문

실습링크: https://codesandbox.io/s/generic-parameter-contraints-v75k7?file=/src/index.ts

```
interface Logable {
  log: () => void;
}
function logItems<T>(items: T[]): void {
  items.forEach(item => item.log());
}
```

1. 제네릭 타입에서 `<T extends ConstrainingType>` 구문은 무엇을 뜻하나요?

    답: T는 ConstrainingType에서 정의된 모든 타입을 만족하여야 함을 의미합니다. T는 ConstrainingType과 완전히 동일하거나 이것의 상위 집합이어야 합니다. ConstrainingType이 가지는 타입의 일부라도 누락되거나 변경되어서는 안 됩니다.

2. T extends Logable 구문을 타입으로 위 실습링크의 오류를 해결해주세요.

    ```
    interface Logable {
      log: () => void;
    }
    function logItems<T extends Logable>(items: T[]): void {
      items.forEach(item => item.log());
    }
    ```

    답: T는 인터페이스 Logbale을 확장하는 타입임을 명시함으로써 배열의 모든 요소가 log 메서드를 가진다는 사실을 인지시킵니다. 이를 통해 확인되지 log 메서드를 사용함으로써 발생하는 타입 오류를 제거합니다.

3. 아래 코드를 붙이세요.
    ```
    const heading = {
      name: "Heading",
      props: { text: "Chapter 1" },
      log: () => console.log("Chapter 1 heading"),
    };
    const button = {
      name: "Button",
      props: { text: "Save" },
      trace: () => console.log("Save button"),
    };
    logItems([heading, button]);
    ```

    타입오류가 날 것 입니다. 타입을 고치지말고 말고 해당 문제가 되는 코드 부분을 고쳐주세요.

    답: logItems에 전달되는 배열의 요소는 모두 log 메서드를 가지고 있어야 합니다. button에는 정확히 같은 동작을 하는 메서드의 이름이 log가 아닌 trace로 명명되어 있습니다. 따라서, 이 부분을 trace에서 log로 수정합니다.

    ```    
    const button = {
      name: "Button",
      props: { text: "Save" },
      log: () => console.log("Save button"),
    };
    ```

4. 아래 폼 타입이 있습니다.

    ```
    interface Form<T> {
      values: T;
    }
    function getFieldValue<T>(form: Form<T>, fieldName: string) {
      return form.values[fieldName];
    }
    ```

    getFieldValue는 키를 가지고 폼 내부 값을 가져오는 set 함수입니다. 아래와 같이 타입을 확장해 완성해보세요. 

    ```
    function getFieldValue<T, K extends keyof T>(
      form: Form<T>, fieldName: K
    ){
      return form.values[fieldName];
    }
    ```

    이와 같이 수정했을때 장점은 무엇일까요?

    답: fieldName으로 사용할 수 있는 string의 범위를 실제 전달된 form에 존재하는 key로 제한함으로써 존재하지 않는 속성에 대한 접근을 사전에 방지할 수 있습니다.

    ```
    const contactForm = {
      values: {
        name: "Bob",
        email: "bob@someemail.com",
      },
    };
    console.log(getFieldValue(contactForm, "name"));
    console.log(getFieldValue(contactForm, "phone"));
    ```

    타입 오류가 발생하는 부분을 찾아주세요.

    답: fieldName으로 전달할 수 있는 인자는 contactForm이 가지는 key로 제한됩니다. contactForm은 name, email을 key로 가지므로 fieldName으로 전달할 수 있는 인자는 'name' 또는 'email'로 제한됩니다.
    
    두 번째로 함수를 호출하였을 때, 'name' 또는 'email'에 해당하지 않는 'phone'을 fieldName으로 하여 함수를 호출하였기 때문에 타입 오류가 발생합니다.

출제 레퍼런스: https://learntypescript.dev/06/l7-generic-parameter-constraints