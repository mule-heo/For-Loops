# 8월 11일 금요일 unknown 타입

1. 실습 링크를 열고 타입에러를 확인하세요.

    https://codesandbox.io/s/unknown-type-o9fpn

    any 타입과 다르게 unknown 타입 에러가 발생합니다. 타입을 고치지 말고, 함수 본문에 타입 가드 (type guard)를 사용해 해결해주세요. 타입 에러가 사라지도록 해주세요.

    ```
    function add(a: unknown, b: unknown) {
      return a + b;
    }
    ```

    답: 코드를 다음과 같이 변경합니다. typeof 연산자를 사용하여 a, b의 타입을 확인하는 과정을 추가합니다.

    ```
    function add(a: unknown, b: unknown) {
      if (typeof a === 'number' && typeof b === 'number'){
        return a + b;
      }
    }
    ```

  - 타입 가드에 대해 살펴보세요.

    타입 가드란 객체의 타입 범위를 좁혀서 사용하는 것을 말합니다. 객체가 특정 타입에 해당하는지 확인하기 위하여 typeof 연산자를 사용하거나, 특정 클래스의 인스턴스인지 확인하기 위하여 instanceof 연산자를 사용할 수 있습니다. 타입스크립트는 이러한 연산자를 사용한 조건문을 통과했을 때, 해당 조건문의 코드 블록 내에서는 해당 객체의 타입을 조건문의 타입으로 간주합니다.

    객체 안에 특정한 key가 있는지 확인하는 in 연산자 또한 타입 가드로 활용할 수 있습니다.

2. 타입-안전한 데이터 가져오기

    ```
    async function getData(path: string): Promise<unknown> {
      const response = await fetch(path);
      return await response.json();
    }

    type Person = {
      id: string;
      name: string;
    };

    async function getPerson(id: string): Promise<Person | null> {
      const person = await getData("/people/1");
      if (person) {
        return person; // 타입에러 발생
      }
      return null;
    }
    ```

    - 타입 에러가 발생하는 이유가 무엇인가요?

      답: 타입 에러가 발생하는 이유는 `if (person)`의 조건문이 확인하는 것은 데이터 페칭의 결과로 얻어진 person의 타입이 아니라 person의 값이 truthy한지 falsy한지이기 여부이기 때문입니다. getPerson 함수는 Person 또는 null을 결과로 하는 프로미스 객체를 반환해야 하지만 위와 같은 조건문으로는 타입을 특정할 수 없기 때문에 그대로 unknown 타입을 반환하게 됩니다. 따라서, 타입 에러가 발생합니다.

    - 이를 해결하기 위해서 타입 명제(type predicate)를 사용해야합니다. isPerson 이라는 함수를 만들어주세요. person 변수가 Person의 타입을 가졌는지를 확인합니다.

      답: isPerson 함수를 정의하여 활용합니다. 반환 타입의 자리에 data is Person을 명시하면 결과가 true일 때 함수에 전달된 data의 타입을 Person으로 간주합니다.

    ```
    const isPerson = (data):data is Person => {
      return 'id' in data && 'name' in data;
    }

    async function getPerson(id: string): Promise<Person | null> {
      const person = await getData("/people/1");
      if (isPerson(person)) {
        return person; // 타입에러 발생
      }
      return null;
    }
    ```

    타입 명제를 적용해본 결과, 함수의 반환 타입으로써 타입 명제를 적용한 함수는 boolean 타입을 반환해야만 하였습니다.

출제 레퍼런스: https://learntypescript.dev/03/l7-unknown

참고

- 타입 가드

  https://www.typescriptlang.org/docs/handbook/2/narrowing.html