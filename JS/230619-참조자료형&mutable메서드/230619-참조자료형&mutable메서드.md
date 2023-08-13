# 6월 19일 월요일 자바스크립트 퀴즈입니다.

```
const arr1 = ['a', 'b', 'c'];
const arr2 = ['b', 'c', 'a'];

console.log(
  arr1.sort() === arr1,
  arr2.sort() == arr2,
  arr1.sort() === arr2.sort()
);
```

a. true true true

**b. true true false**

c. false false false

d. true false true


참조 자료형과 mutable 메서드에 관한 문제입니다.

1. 
    arr1.sort() === arr1;

    sort 메서드는 원본에 직접적으로 수정을 가하는 mutable 메서드입니다. arr1.sort()와 arr1이 가진 참조는 동일하므로 **true**를 반환합니다.

    참고로 sort 메서드에 비교 함수를 전달하지 않은 경우 문자열을 기준으로 오름차순으로 정렬되므로 두 배열이 가진 값은 ['a', 'b', 'c']로 동일합니다.

2. 
    arr2.sort() === arr2;

    위의 경우와 마찬가지로 두 배열이 가진 참조는 동일하므로 **true**를 반환합니다.

    arr2.sort -> ['a', 'b', 'c']

    arr2 -> ['b', 'c', 'a']

3.
    arr1.sort() === arr2.sort();

    arr1, arr2는 서로 다른 배열에 대한 참조를 가지고 있으므로 **false**를 반환합니다.

    arr1.sort() -> ['a', 'b', 'c']
    
    arr2.sort() -> ['a', 'b', 'c']


참고

- 원본을 수정하는 메서드는 mutable 메서드입니다. (예: sort, reverse, splice)

- 원본을 수정하지 않고 새로운 배열 혹은 객체를 반환하는 메서드는 immutable 메서드입니다. (예: toSorted, toReversed, slice)

- 값을 새롭게 할당하지 않고도 기존의 값을 수정할 수 있는 배열과 객체의 사용에 있어서 유의하여야 합니다.


Mutable, Immutable 용어 설명

https://developer.mozilla.org/en-US/docs/Glossary/Mutable

https://developer.mozilla.org/en-US/docs/Glossary/Immutable

