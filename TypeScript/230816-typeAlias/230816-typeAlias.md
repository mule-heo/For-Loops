# 8월 16일 타입 별칭

1. 세 가지 객체에 사용할 수 있는 타입을 선언해주세요.

    ```
    const tomScore  = {
      name: "Tom",
      score: 70,
    };
    const bobScore = {
      name: "Bob",
      score: 80,
    };
    const janeScore= {
      name: "Jane",
      score: 90,
    };
    ```

    답: name과 score를 프로퍼티로 가지는 객체가 반복되고 있습니다. 공통 타입은 다음과 같이 선언할 수 있습니다.

    `type Score = { name: string; score: number; }`

2. `type TypeAliasName = ExistingType;` 과 같이 타입을 재할당(지정)할 수 있나요?

    답: 네. 동일한 타입 이름을 사용하여 타입을 중복하여 선언하는 것이 아니라면 이미 선언된 타입을 다른 타입에 재할당하는 것도 가능합니다.

3. 원시값(primitives)에 타입 별칭을 사용하는 것에 대한 의견을 알려주세요.

    string, number, boolean과 같은 경우 간단하게 타입을 명시할 수 있고, 타입 별칭을 사용하는 경우 커서를 올려 해당 타입 이름이 가지는 정확한 타입을 확인해야 하므로 번거로운 작업이 한 단계 추가됩니다. 개인적으로 다른 타입과 조합하기 위하여 따로 관리해야 하는 경우가 아니라면 원시값에 타입 별칭을 사용하지는 않을 것 같습니다.

4. 다음 함수 시그니처의 타입(Log)을 만들어주세요.

    ```
    const log = (message: string) => {
      console.log(message);
    };
    ```

    답: 함수에 대한 타입 별칭을 선언하는 방법은 다음과 같습니다.

    ```
    type Log = (message: string) => void;

    const log:Log = (message) => {
      // ...
    }
    ```

    > 그런데 함수 안에서 다른 값을 return해서 void가 아니게 되어도 별다른 오류는 발생하지 않네요. 다른 타입을 반환 타입으로 명시하면 정상적으로 오류 메시지를 출력하지만 void의 경우 다른 타입을 반환해도 오류 메시지가 출력되지 않습니다. 실행 환경은 [타입스크립트 플레이그라운드](http://www.typescriptlang.org/play), 타입스크립트 버전 5.2.2입니다. 코드샌드박스에서도 마찬가지였습니다. 이것에 대해 알게 되면 추후 수정하겠습니다.


(심화) 제네릭 타입을 보신 분들이라면 여기에 있는 내용을 보시고 설명해주세요. https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases

  > (제네릭 학습 후 추가 예정)

출제 레퍼런스: https://learntypescript.dev/04/l3-type-aliases