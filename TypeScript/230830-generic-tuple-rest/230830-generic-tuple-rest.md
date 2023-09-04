# 8월 30일 수요일 튜플 타입과 rest 연산자 사용한 제네릭타입 만들기

타입스크립트 4 이상에서만 가능합니다.

1. 아래 타입을 설명해주세요.

    ```
    type Scores = [string, ...number[]];
    ```

    답: Scores 타입이 표현하는 배열은 첫 요소가 반드시 있어야 하며 타입은 string입니다. 나머지 요소는 생략할 수 있으며, 요소가 있다면 그러한 요소의 타입은 모두 number이어야 합니다.

2. 아래 타입을 설명해주세요.

    버전1

    ```
    type NameAndThings<T extends unknown[]> = [string, ...T];
    ```

    답: T는 배열 형태를 만족해야 하며, NameAndThings 타입의 첫 요소는 string으로, 생략할 수 없으며 나머지 요소에 대한 타입은 NameAndThings 타입을 적용할 때 결정할 수 있습니다.

    버전2

    ```
    type NameAndThings<T extends unknown[]> = [name: string, ...things: T];
    ```

    위 타입에서 name과 things를 라벨은 어떤 역할을 하나요?

    답: 버전1에 label을 추가한 형태입니다. 타입을 사용할 때에 첫 요소의 string이 name으로 사용될 것이라는 점을 확인할 수 있으며, 나머지 배열 요소는 things에 해당함을 확인할 수 있습니다.

    NameAndThings 타입을 사용한 예시를 알려주세요.

    ```
    const arr: NameAndThings<boolean[]> = ['mule', true, false];
    ```

3. 아래 타입을 설명해주세요.

    ```
    function logThings<T extends unknown[]>(name: string, ...things: T) {
      console.log(things);
    }
    ```

    답: 함수의 첫 번째 인자는 string이며, 나머지 요소는 입력에 따라 자동으로 추론됩니다. 따라서 name을 제외한 인자는 모든 타입을 사용할 수 있습니다.

    logThings 함수의 사용 예시를 알려주세요.

    ```
    // 첫 인자만 string 타입으로 고정되며 나머지 인자는 자유롭게 사용할 수 있습니다.

    logThings('mule', 1, true, [1, 2], { name: 'mule' });
    // -> [1, 2, true, false, 1, Array(3), Object]

    // 제네릭 타입을 전달하면 나머지 인자를 원하는 타입으로 한정할 수 있습니다.
    logThings<boolean[]>('mule', true, false);
    // -> [true, false]
    ```

출제 레퍼런스: https://learntypescript.dev/06/l8-generic-rest