# 8월 21일 월요일 인터페이스 v 타입 별칭

인터페이스와 타입 별칭을 사용에 대한 의견을 알려주세요.

예시는 아래를 참고하셔도 되고 안하셔도 됩니다. (자유)

1. 배열 표현

    ```
    type Names = string[];
    interface Names {
      [index: number]: string;
    }
    ```

    답: interface를 활용하여 key, value를 지정하는 것보다 type을 활용하여 정의하는 것이 편리합니다.

2. 튜플 표현

    ```
    type Point = [number, number];
    ```

    답: type을 활용하여 정의하여야 합니다. interface를 사용하고자 하면 다음과 같이 정의할 수 있습니다.

    ```
    interface Point {
      0: number,
      1: number
    }
    ```

3. 함수 표현

    ```
    type Log = (message: string) => void;
    interface Log {
      (message: string): void;
    }
    ```

    답: type을 활용하여 정의하는 것이 편리합니다.


4. 유니온 타입

    ```
    type Status = "pending" | "working" | "complete";
    ```

    답: 유니온 타입은 type을 활용하는 것이 편리합니다.

5. 객체 표현

    ```
    type Person = {
      name: string;
      score: number;
    };
    interface Person {
      name: string;
      score: number;
    }
    ```

    답: 재선언 병합과 같은 향후 변경 가능성을 제외한다면 객체의 표현 자체는 동일한 수준의 노력을 필요로 합니다.

6. 객체 재구성

    ```
    type Name = {
      firstName: string;
      lastName: string;
    };
    interface PhoneNumber {
      landline: string;
      mobile: string;
    }
    type Contact = Name & PhoneNumber;
    ```

    답: &, | 연산자를 사용하여 유니온, 인터섹션 타입을 활용하기 위해서는 type을 활용하여야만 합니다. 이러한 타입을 정의하기 위해 이미 정의된 인터페이스를 활용할 수도 있습니다.

7. 라이브러리 타입 재선언

    답: interface가 type을 이길 수 있는 유일한 문항 - 라이브러리의 타입을 재선언하기 위해서는 interface를 활용하여야만 합니다. type은 한 번 선언되면 내용을 변경할 수 없습니다.

정리

타입 관리의 대부분은 타입 별칭을 활용하되 객체의 구조를 정의하는 경우 인터페이스를 활용하는 것을 고려하고, 다른 라이브러리의 타입을 수정하여야 하는 경우가 있다면 인터페이스가 가지는 재선언 병합의 특성을 기억하고 활용하면 되겠습니다.

출제 레퍼런스: https://learntypescript.dev/04/l7-interfaces-v-type-aliases