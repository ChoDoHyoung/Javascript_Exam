# JSON과 메서드
> 복잡한 객체를 다루고 있다고 가정해 본다면, 네트워크를 통해 객체를 어딘가에 보내거나 로깅 목적으로 객체를 출력해야 한다면, 객체를 문자열로 전환해야 한다.
> 이때 전환된 문자열엔 원하는 정보가 있는 객체 프로퍼티 모두가 포함되어야만 한다.
> 아래와 같은 메서드를 구현해 객체를 문자열로 전환.
    ~~~
    let user = {
        name: "John",
        age: 30,

        toString() {
            return `{name: "${this.name}", age: ${this.age}}`;
        }
    };

    alert(user); // {name: "John", age: 30}
    ~~~
- 그런데 개발 과정에서 프로퍼티가 추가되거나 삭제, 수정될 수 있다.
- 이렇게 되면 위에서 구현한 toString을 매번 수정해야 하는데 이는 아주 고통스러운 작업이 된다.
- 프로퍼티에 반복문을 돌리는 방법을 대안으로 사용할 수 있는데, 중첩 객체 등으로 인해 객체가 복잡한 경우 이를 문자열로 변경하는 건 까다로운 작업이라 이마저도 쉽지 않다.
- 다행히 자바스크립트엔 이런 문제를 해결해주는 방법이 있다. 관련 기능이 이미 구현되어 있어서 우리가 직접 코드를 짤 필요가 없다.