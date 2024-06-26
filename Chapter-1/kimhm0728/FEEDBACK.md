### 책 읽으면서 어느부분까지 적용할것인지 고민해보기
- ex: 모델에 한해서는 책 내용을 모두 적용해보자.
- 책에서는 Controller는 도구다. Controller, Util 등은 객체가 아니다.

<br>

### model에서 getter는 없어야 한다. 
- 우리가 작성한 코드에 getter가 있는 이유는, view와 controller 때문이다.
- model만 놓고 봤을 때 getter가 있으면 안 된다.

<br>

### 책에서 말하는 주생성자와 코틀린에서의 주생성자는 약간 다르다.
- 코틀린에서 주생성자는 클래스 선언부에 있는 생성자를 말한다. 로직이 들어갈 수 없다.
- 반면에 책에서 말하는 주생성자는, `모든 인자를 초기화하는 로직`이 포함된 생성자를 말한다.

<br>

### 생성자에는 로직이 들어가면 안 된다. 그렇다면 생성자에서 검증을 해도 될까?
- `느린 실패` vs `빠른 실패` -> 책에서는 빠른 실패를 권장한다.
- 검증은 도메인이 완성되기 위한 전제조건이다.
- 메서드를 호출할 때 유효한 값인지 검사하는 것보다, 생성자에서 검사해서 `빠르게 실패`하자. (빠른 실패는 4장에서 더 자세히 다룬다.)

<br>

### 그렇지만 생성자에서 검증할 부분과 메서드에서 검증할 부분을 명확히 구분해야 한다.
```
1. Url(https://naver.com)
2. Url(https://www.abcdefghi.com)
3. Url("olive")
```
- 위 세개의 코드 중 Url 객체는 1, 2번만 해당된다. 3번은 url 형식이 아니기 때문에 객체가 될 수 없다. 그렇다면 2번은 왜 Url 객체일까?
- 2번 객체의 url이 유효한 링크인지 검사하기 위해서는, 실제 네트워크 연결을 해야한다. 또한 검증 시점에 따라 유효한 링크인지 아닌지 달라질 수 있다.
- `유효한 링크`인지에 대한 검사는, url을 직접 실행하는 메서드의 책임이다. Url 클래스의 생성자에서는 `url 형식이 맞는지만 검사`한다. 
