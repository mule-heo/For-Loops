# 7월 24일 월요일 메모이제이션에 대한 주관식 퀴즈입니다.

레퍼런스: https://www.interviewbit.com/javascript-interview-questions/#memoization

메모이제이션은 함수의 반환 값이 매개변수에 따라 캐시되는 캐싱의 한 형태입니다. 해당 함수의 매개변수가 변경되지 않으면 함수의 캐시된 버전이 반환됩니다.

```
function addTo256(num){
  return num + 256;
}

addTo256(20); // Returns 276
addTo256(40); // Returns 296
addTo256(20); // Returns 276

아래는 addTo256을 메모화된 함수로 변환한 함수입니다.
function memoizedAddTo256(){
  var cache = {};

  return function(num){
    if(num in cache){
      console.log("cached value");
      return cache[num]
    }
    else{
      cache[num] = num + 256;
      return cache[num];
    }
  }
}
var memoizedFunc = memoizedAddTo256();

memoizedFunc(20); // Normal return
memoizedFunc(20); // Cached return
```

위의 코드 예시를 보고, 아래 물음에 기초해 답해주시면 됩니다. 

- 메모이제이션은 무엇인가요?

  메모이제이션이란 연산의 결과를 별도로 기록(메모)해 두는 것입니다. 결과를 따로 기록해 둠으로써 이미 계산한 결과가 다시 필요할 때 계산하는 과정을 생략하고 이미 계산한 결과를 즉시 활용할 수 있게 됩니다.

- 메모이제이션이 필요한 이유는 무엇인가요?

  단순 사칙연산과 같이 연산에 큰 비용이 들지 않는 경우가 있는 반면에, 어떤 결과를 얻기 위해 복잡한 연산을 거쳐야 하는 경우도 있습니다. 이러한 결과가 자주 바뀌지 않는다고 가정했을 때, 동일한 결과를 얻기 위해 매번 같은 연산을 거치는 것은 비효율적입니다. 이러한 낭비를 막고 프로그램 작동을 최적화하기 위하여 메모이제이션이 필요합니다.

- 매우 무거운 작업을 수행하는 함수를 메모이제이션 한다고 했을 때, 어떤 일이 발생할까요.

  우선 함수를 별도로 저장하는 공간을 추가로 점유합니다. react의 동작과 같이 동일한 코드의 실행이 반복적으로 일어나는 경우라면 함수를 정의하는 과정에서 발생하는 연산을 줄일 수 있습니다.

- 프론트엔드 프레임워크/라이브러리에서 메모이제이션 테크닉/솔루션 대해 들어본 적이 있나요?

  react(프레임워크)
  - useMemo: React 함수 컴포넌트 내에서 특정 state가 변경되기 전까지 캐시된 값을 그대로 사용하도록 하는 Hook입니다.
  - useCallback: React 함수 컴포넌트 내에서 특정 state가 변경되기 전까지 캐시된 함수를 그대로 사용하도록 하는 Hook입니다.

  <br>

  recoil(상태관리 라이브러리)
  - Recoil의 atom, selector를 사용한 상태관리는 자체적인 메모이제이션을 통한 최적화를 지원합니다.

  <br>

  react-query(API 특화 상태관리 라이브러리)
  - API 요청에 대한 응답으로 얻은 데이터를 캐시하여 활용할 수 있습니다. 응답 데이터를 캐시 가능한 시간이 경과하기 전까지는 동일한 요청에 대하여 캐시된 데이터를 반환합니다. 캐시 가능한 시간이 경과한 경우 해당 요청에 대하여 새롭게 API를 호출하여 데이터를 갱신합니다.
