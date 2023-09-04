# 8월 24일 금요일

1. 제네릭 타입 파라미터 네이밍 컨벤션에 대해서 알려주세요. 이에 대한 의견도 알려주세요.

    답: 제네릭 타입의 파라미터로써 다음의 다섯 가지 알파벳을 사용합니다.

    - T: Type
    - S: State
    - K: Key
    - V: Value
    - E: Element

    처음 보았을 때는 각 알파벳이 무엇을 의미하는지 정확히 몰랐으나 축약된 단어의 원형을 보니 단번에 이해가 되었을 정도로 직관적이라고 생각합니다. 일반 변수와 구분되도록 첫 글자만 따서 대문자로 표현하는 것도 가독성을 높입니다.

    레퍼런스에서는 T로 사용될 타입이 여럿인 경우 T1, T2와 같이 네이밍하였으나 타입스크립트 핸드북의 예제에서는 T, U와 같이 알파벳 순서로 네이밍한 것을 확인하였습니다. 또한 축약형 T가 아닌 Type과 같이 표시된 예제도 존재합니다. 이를 통해 축약형의 사용을 강제할 정도로 네이밍 컨벤션이 엄격하게 적용되지는 않음을 느꼈습니다.



2. 제네릭 타입을 사용한 폼 객체

    contactForm 이라는 객체가 있습니다.

    ```
    const contactForm = {
      values: {
        name: "",
        email: "my-email@hello.com",
      },
      errors: {
        name: 'Name is required'
      }
    };
    ```

    values는 input 필드로서 name, email 가집니다. 항상 문자열을 가집니다. (입력 필드가 비어있다면 빈 문자열입니다)  errors 객체는 오류가 있는 필드에 메시지를 보여줍니다.  유효한 폼은 error에 빈 객체를 가집니다. (erros: {}) 
    제네릭 타입을 사용해 contactForm 타입을 명시해주세요. type aliases 를 사용하셔도 되고 interface 를 사용하셔도 됩니다.

    답
    
    ```
    interface Contact {
      name: string;
      email: string;
    }

    interface Form<T> {
      values: T

      // T가 가진 key 전체에 대하여 optional한 string으로 타입 정의
      errors: {
        [K in keyof T] ?: string
      }
    }

    const contactForm: Form<Contact> = {
      values: {
        name: 'mule',
        email: 'abc123@abcd.efg',
      },
      errors: {}
    }
    ```

출제 레퍼런스: https://learntypescript.dev/06/l3-generic-interfaces