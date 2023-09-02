# 8월 23일 수요일 제네릭 기본 타입

아래 제네릭 타입에 대해 예시를 알려주세요.

https://learntypescript.dev/06/l1-standard-generic-types

1. Array<T>

    ```
    Array<string> // = string[]
    Array<number> // = number[]
    ```

    타입이 T인 요소만을 가지는 배열을 의미합니다.

2. Promise<T>

    ```
    new Promise<SomeType>((res, rej) => {
        ...
    })
    ```

    Promise의 결과로써 타입이 T인 값을 반환합니다.

3. Record<K,V>

    ```
    type Animal = 'horse' | 'donkey' | 'mule';
    
    interface AnimalInfo {
        age: number;
        legs: number;
    }

    const animals: Record<Animal, AnimalInfo> = {
        horse: { age: 1, legs: 4 },
        donkey: { age: 10, legs: 4 },
        mule: { age: 7, legs: 4 },
    }
    ```

    Record<K, V>의 K는 객체의 key가 가지는 타입을 의미하며, V는 객체의 value가 가지는 타입을 의미합니다.

4. 유틸리티 타입 중 하나를 선택해 설명해주세요.

    https://www.typescriptlang.org/docs/handbook/utility-types.html

    Omit<Type, Keys>

    Omit은 특정 Type으로부터 Keys에 해당하는 속성들을 생략한 타입을 의미합니다. 예시는 다음과 같습니다.

    ```
        interface Contact {
            email: string;
            fax: string;
            telephone: string;
            address: string;
        }

        type ContactOmit = Omit<Contact, "address" | "fax">

        ContactOmit // -> { email: string; telephone: string; }
    ```

    이미 정의된 인터페이스, 타입의 일부 속성만 활용하고자 할 때 새로운 인터페이스, 타입을 정의할 필요없이 Omit을 통해 일부 속성만을 생략하여 활용할 수 있습니다.

출제 레퍼런스: https://learntypescript.dev/06/l1-standard-generic-types