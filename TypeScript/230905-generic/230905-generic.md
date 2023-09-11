# 9월 5일 화요일 제네릭 실전 종합문제

아래 문제별로 타입을 수정하거나 추가해주시면 됩니다.

1.

```ts
type Comment = {
  comment: string;
  email: string;
}
```

```ts
type ReadonlyComment = {
  readonly comment: string;
  readonly email: string;
}
```

이 ReadonlyComment 대신 제네릭타입 을 사용해 해결해주세요.

답

```ts
Readonly<Comment>
```

사전에 정의된 Readonly 제네릭 타입을 사용하면 인자로 전달된 타입이 가진 속성이 전부 읽기 전용 속성으로 설정됩니다.

2.

아래 함수 타입을 추가해주세요.

```ts
function countDistinct(itemToCount, array) {
  return array.filter(item => item === itemToCount).length;
}
```

답

```ts
function countDistinct<T>(itemToCount: T, array: T[]){
  return array.filter(item => item === itemToCount).length;
}
```

제네릭 파라미터를 활용하여 타입을 유연하게 결정하되 itemToCount의 타입과 array가 가지는 값의 타입을 같게 설정하는 것이 바람직해 보였습니다. 따라서 제네릭 파라미터를 활용하여 item에는 T를, array에는 T를 값으로 하는 배열을 타입으로 지정하였습니다. 반환 타입은 length 속성으로 인해 자동으로 number로 추론될 것입니다.

3.

이 함수 타입을 고쳐주세요.

```ts
function remove<ItemType>(itemToRemove: ItemType, array: Array<ItemType>): ItemType {
  return array.filter(item => item !== itemToRemove);
}
```

답

```ts
function remove<ItemType>(itemToRemove: ItemType, array: Array<ItemType>): ItemType[] {
  return array.filter(item => item !== itemToRemove);
}
```

array의 filter 메서드는 반환값으로써 배열의 특정 요소를 반환하지 않습니다. 대신에 필터링이 수행된 이후에 새롭게 생성된 배열을 반환합니다. 따라서, 반환 타입은 ItemType이 아닌 ItemType을 요소로 하는 배열이 되어야 합니다. (`ItemType[]` 또는 `Array<ItemType>`)

4.

```ts
interface User {
  id: any;
  name: string;
  email: string
}
```


User의 any 타입을 제네릭타입을 사용해 고쳐주세요. (id는 매개변수를 사용하여 지정합니다.)

답

```ts
interface User<T> {
  id: T;
  name: string;
  email: string;
}
```

User 타입을 사용할 때에 id에 대한 타입을 직접 지정하여 사용할 수 있도록 제네릭 파라미터를 사용하였습니다. 변경된 User 인터페이스의 사용 예시는 다음과 같습니다.

```ts
const user: User<number> = {
  id: 1,
  name: 'mule',
  email: 'devheo@ab.cd'
}
```

any의 적용 가능성을 그대로 유지하고자 한다면 다음과 같이 디폴트 파라미터를 지정할 수 있습니다.

```ts
interface User<T = any> {
  id: T;
  name: string;
  email: string;
}
```

위와 같이 any 타입을 T에 대한 기본값으로 지정한 경우, User에 타입을 지정하지 않고 호출하였을 때에 타입이 any로 지정됩니다.

```ts
const user: User = {
  id: 1, // -> 입력한 값은 number 타입이지만 제네릭 타입의 기본 타입으로 지정했던 any 타입으로 표시됩니다.
  name: 'mule',
  email: 'devheo@ab.cd'
}
```


5.

```ts
function logName(object: any) {
  console.log("My name is " + object.name);
}
```

객체를 출력하는 함수입니다. extends 타입 확장으로 가장 강력하게 타입을 지정해주세요.

답

```ts
function logName<T extends { name: string }>(object: T) {
  console.log("My name is " + object.name);
}
```

logName 함수 내부의 코드 블록을 정상적으로 실행하기 위해서는 반드시 object가 name 속성을 가져야 하며, 그 값의 타입은 string이어야 합니다. 제네릭 파라미터를 활용하여 object가 { name: string }의 형태를 만족해야 하도록 제한할 수 있습니다. 여기에서 형태를 만족한다는 것은 두 객체의 형태가 정확히 일치하는 것이 아닌, 전달된 인자의 타입이 제약 조건으로써 주어진 객체의 타입 정보를 전부 만족하고 있어야 함을 의미합니다.

함수 전달인자의 경우 logName을 호출할 때에 타입을 직접 입력하지 않아도 입력으로부터 타입이 자동으로 추론되며, 전달인자 object는 이제 { name: string }을 포함하고 있어야 합니다.

출제 레퍼런스: https://learntypescript.dev/06/l10-quiz

실수

제네릭 타입, extends를 적용하는 부분이 익숙하지 않아 `T extends { name: string }`, `T`를 서로 반대되는 위치에 작성

- 의도: 이 함수에서 T를 사용할 것인데 이 T는 object에 적용했을 때 { name: string }을 포함하고 있어야 함
- 실제: T는 { name: string }을 포함하고 있어야 하며, 이것을 object의 타입으로 할 것