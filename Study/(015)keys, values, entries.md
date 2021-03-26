# Object.keys, values, entries
- 이 메서드들은 포괄적인 용도로 만들어졌기 때문에 메서드를 적용할 자료구조는 일련의 합의를 준수해야 한다.
- 커스텀 자료구조를 대상으로 순회를 해야 한다면 이 메서드들을 쓰지 못하고 직접 메서드를 구현해야 한다.

- keys(), values(), entries()를 사용할 수 있는 자료구조는 다음과 같다.
    - Map
    - Set
    - Array

- 일반 객체에도 순회 관련 메서드가 있긴 한데, keys(), values(), entries()와는 문법에 차이가 있다.
- 일반 객체엔 다음과 같은 메서드를 사용할 수 있다.
    - Object.keys(obj) – 객체의 키만 담은 배열을 반환
    - Object.values(obj) – 객체의 값만 담은 배열을 반환.
    - Object.entries(obj) – [키, 값] 쌍을 담은 배열을 반환.

- Map, Set, Array 전용 메서드와 일반 객체용 메서드의 차이를 (맵을 기준으로) 비교하면 다음과 같다.
 |맵|객체
|호출 문법|map.keys()|Object.keys(obj)(obj.keys() 아님)
반환 값|iterable 객체|‘진짜’ 배열
- 첫 번째 차이는 obj.keys()가 아닌 Object.keys(obj)를 호출
- 이렇게 문법이 다른 이유는 유연성 때문
- 자바스크립트에선 복잡한 자료구조 전체가 객체에 기반
- 객체 data에 자체적으로 data.values()라는 메서드를 구현해 사용하는 경우가 있을 수 있다.
- 커스텀 메서드를 구현한 상태라도 Object.values(data)같은 형태로 메서드를 호출할 수 있으면 커스텀 메서드와 내장 메서드 둘 다를 사용할 수 있다.
- ※ Object.keys, values, entries는 심볼형 프로퍼티를 무시.

## 객체 변환하기
- 객체엔 map, filter 같은 배열 전용 메서드를 사용할 수 없다.
- 하지만 Object.entries와 Object.fromEntries를 순차적으로 적용하면 객체에도 배열 전용 메서드 사용.

1. Object.entries(obj)를 사용해 객체의 키-값 쌍이 요소인 배열을 얻음
1. 1.에서 만든 배열에 map 등의 배열 전용 메서드를 적용.
1. 2.에서 반환된 배열에 Object.fromEntries(array)를 적용해 배열을 다시 객체로 되돌림.

- 이 방법을 사용해 가격 정보가 저장된 객체 prices의 프로퍼티 값을 두 배로 늘려보기
    ~~~
        let prices = {
            banana: 1,
            orange: 2,
            meat: 4,
        };

        let doublePrices = Object.fromEntries(
        // 객체를 배열로 변환해서 배열 전용 메서드인 map을 적용하고 fromEntries를 사용해 배열을 다시 객체로 되돌립니다.
            Object.entries(prices).map(([key, value]) => [key, value * 2])
        );

        alert(doublePrices.meat); // 8
    ~~~