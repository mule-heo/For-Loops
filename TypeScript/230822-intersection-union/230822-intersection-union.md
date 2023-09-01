# 8월 22일 화요일 & | - 타입의 교집합과 합집합

1. & | 타입의 교집합과 합집합

   ```
   type OrderStatus = "pending" | "completed";
   type DeliveryStatus = "completed" | "shipped";
   type Status = OrderStatus | DeliveryStatus;
   ```

    다음 Status 타입 결과를 알려주세요.

    ```
    type Status = OrderStatus | DeliveryStatus;
    ```

   - 답

      `"pending" | "completed" | "shipped"`

      completed의 중복이 제거되고 세 가지 상태만 남게 됩니다.

    다음 Status 타입 결과를 알려주세요.

    ```
    type Status = OrderStatus & DeliveryStatus;
    ```

   - 답

      `"completed"`

      두 타입에 공통으로 해당하는 completed만 남게 됩니다.

2. 타입 축소에 대해서 알려주세요.

   참고: https://www.typescriptlang.org/docs/handbook/2/narrowing.html

   답: 타입 축소란 어느 객체가 해당할 수 있는 타입의 후보군을 좁히는 것을 말합니다. 예를 들어 a의 타입이 string | number라면 현재 a가 가질 수 있는 타입은 string 또는 number입니다. 이러한 상황에서 string의 프로토타입이 가지는 메서드를 사용하고자 한다면 a가 string이라는 근거를 제공하여야 합니다. 이전에 살펴 보았듯 typeof, instanceof 연산자 또는 type predicate를 사용하여 특정 변수의 타입을 축소할 수 있습니다.

   typeof를 사용하면 if-else문 안에서 축소된 타입으로 값을 조작할 수 있습니다. if문을 통과하면 string, 그렇지 아니한 경우 number 타입으로 간주됨을 확인할 수 있습니다.

   ```
   function addThree(num: string | number){
      num; // -> string | number
      
      if (typeof num === 'string'){
         num; // -> string
         return num + 3;
      } else {
         num; // -> number
         return num + 3;
      }
   }
   ```

   아래는 type predicate의 예시입니다. 반환되는 값은 boolean 타입으로 한정되며, 함수의 결과로써 true를 반환할 시 반환 타입의 is문의 앞에 사용된 전달인자를 is 뒤에 명시된 타입으로 추론하도록 합니다.

   ```
   function isPerson(person: any): person is Person {
      return person.name && person.age;
   }
   ```

출제 레퍼런스: https://learntypescript.dev/04/l9-type-compatibility

참고

- type predicate
   
   https://learntypescript.dev/07/l6-type-predicate