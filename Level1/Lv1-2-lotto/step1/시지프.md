# Level1 로또 Step1(83,89,97,99,100,101,102,109) - 시지프

분석 담당 코드

- [#83](https://github.com/woowacourse/javascript-lotto/pull/83)
- [#89](https://github.com/woowacourse/javascript-lotto/pull/89)
- [#97](https://github.com/woowacourse/javascript-lotto/pull/97)
- [#99](https://github.com/woowacourse/javascript-lotto/pull/97)
- [#100](https://github.com/woowacourse/javascript-lotto/pull/100)
- [#101](https://github.com/woowacourse/javascript-lotto/pull/101)
- [#102](https://github.com/woowacourse/javascript-lotto/pull/102)
- [#109](https://github.com/woowacourse/javascript-lotto/pull/109)

## 아키텍쳐 분석

- [#109] 상태관리 + 클래스 상속을 통한 MVC 패턴

  <img src="https://user-images.githubusercontent.com/44823900/155480256-a05ea975-6283-4aaa-989a-a38bf87e22c9.png" />

- <b>특이점</b>

  - 상태관리
    - 상태가 변하면, View를 update 해주는 구조
  - 클래스 상속을 통한 MVC 패턴
    - View와 Controller에 동일한 메서드가 반복되기 때문에, Core/View , Core/Controller 추상 부모 클래스를 만들고, 자식 클래스가 이를 상속하도록 구현.

- <b>상태 관리는 어떻게 했는가?</b>

  - Model - state 멤버 변수가 있고, update 메서드가 있다.

    ```javascript
    state;

    update(newState) {
      this.state = { ...this.state, ...newState };
    }
    ```

  - View - state 멤버 변수가 있고, update, render 메서드가 있다. update 되면 render되게 구현했다.

    ```javascript
    state;

    update(newState) {
      this.state = { ...this.state, ...newState };
      this.render();
    }

    render() {
      this.beforeMounted();
      this.$target.innerHTML = this.template();
      this.afterMounted();
    }
    ```

  - <b>클래스 상속의 장점은 무엇인가?</b>

    - 비슷한 패턴의 메서드를 부모 클래스에 모아서, 중복을 방지하고 효율적인 코드를 짤 수 있다.
    - 자식 클래스가 어떤 클래스를 가질지 예측하기 쉽다.

  - 소견

    - 상태관리는 data 변경 -> view 변경으로 바로 이어지는 구조면 좋을 것 같다. 하지만 이 구조에서는 data의 상태를 변경한 후, 이를 view 상태에 대입해주고, view를 re-render 시켜준다. React적 상태관리는 MVC에서 효율적이지는 않은 것 같다.

  <br/>
  <br/>

## 피드백 정리

### 컨벤션

- [#100] 보통 클래스나, 인스턴스에서만 PascalCase를 사용한다. (cf, camelCase)

### 클린코드

- [#83] 함수 분리
  함수를 너무 잘게 분리하게 되면 코드라인이 길어지고 오히려 가독성을 해칠 수 있다. 그러므로
  1. 재사용될 가능성이 낮다.
  2. 함수 기능이 확장될 가능성이 낮다.
  3. 함수화하지 않아도 한줄 코드로 이해가 잘 간다.
     <br/>
     일 때는 분리하지 않는 것도 하나의 방법이다.

### 성능

- [#101] set vs array 성능 차이

  ```plain
  array보다 set가 성능적 이점이 있을 것 같아서, 로또 1,000개 구입 시나리오로 직접 console.time을 여러 번 찍어본 결과, 오히려 set가 array보다 대부분 느렸습니다(대략 set는 2.2ms , array는 1.7ms / 로또 번호 개수를 6개보다 훨씬 크게 해보는 등 테스트해보자 성능 차이는 수 배 이상으로 벌어짐)

  그 이유가 무엇일까 궁금하여 검색해본 결과, Array 데이터는 연속적 메모리 공간에 저장되고 이 때문에 CPU가 pre-fecthing하므로 set 등 다른 추상적 데이터 유형보다 데이터 접근을 더욱 빨리 할 수 있다는 사실을 알게 됐습니다. 아마도 그래서 제 코드에서도 Array가 Set보다 빠를 수 있었던 것 같습니다.
  ```

### 설계

- [#100] eventListener에서 핸들러 함수를 정의할 때 나중에 이벤트를 해제하기 위해 변수로 할당해서 사용해야 할까요?

  ```plain
    현업에서도 event listener 로 넘길 핸들러 함수를 정의할 때, 나중에 이벤트를 해제하기위해 이따금씩 변수에 할당해서 사용하곤 합니다!
    그런데 사실 지금 같은 경우는 removeEventListener 를 사용하지 않으신데 혹시나 하는 마음으로..🤔로 코드를 작성하는 건 좋진 않은 습관같습니다! YAGNI라고... "You Aren't Gonna Need It" 라는 말이 있는데요... 저는 처음부터 확장성이나 미래를 심히 고려해 오버엔지니어링하는 걸 경계하는 편이에요 🥲 물론 지금 상황은 확장성보다는 미래에 언젠가 필요하겠지하고 미리 개발을 해놓는 건데요. 대부분 높은 확률로 필요없더라고요ㅋㅋㅎ 나중에 봤을 때, "?? 이게 필요했나? 이젠 안쓰게된건가??(원래부터 안씀) 왜 이렇게 했지??" 라는 생각을 할 수도 있고요..ㅎ
  ```

  [참고자료](https://medium.com/front-end-weekly/es6-set-vs-array-what-and-when-efc055655e1a)

### JS

- [#100] 1부터 45까지의 배열을 만드는 방법

  - [...Array(46).keys()].slice(1)
  - Array.from({length: 46}, (\_, i) => 1 + i)

- [#99] 숫자에 3자리마다 comma를 넣어주는 내장함수
  [number.toLocaleString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)

### 변수명

- [#97] handleToggleButtonClick → handleClickToggleButton이 더 낫지 않을까요? 동사가 앞에 오는게 어떤 역할을 하는지 쉽게 확인할 수 있을 것 같아요.

- [#83] `on~` 네이밍은 이벤트 리스너의 콜백함수로 들어가는 네이밍 같다. 그러므로, 이벤트 핸들러를 연결해주는 함수는 `bind~`라고 이름을 붙여준다.

### 객체지향

- [#83] 은닉, 캡슐화<br/>
  private 접근자는 언제 사용하는가?
  - 외부에서 건드릴 수 없게 하기 위해서
  - 외부에서 알 필요가 없을 때

### HTML 웹 표준

- heading 태그는 건너뛰는 것을 피하세요.언제나 \<h1>로 시작해서, \<h2>, 순차적으로 기입하세요.
  <br/>
  [참고자료](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Heading_Elements)

- [#102] heading 요소를 `display: none;` 처리하는 이유가 궁금합니다. display none으로 숨기게 되면 영역에서 아예 사라지게 되는 스타일이라서 검색엔진이나 스키른 리더에서 접근이 불가합니다; 웹 접근성에 맞는 텍스트 숨기는 방법을 찾아보시면 좋을 것 같아요.

### CSS

- [#97] CSS - 0px 일때는 px 을 떼고 0으로 적자. px을 적지 않는게 성능상으로 유리하다.

- [#101]

  ```css
  input:focus {
  outline: none;
  ```

  위 코드에 대하여

  - focus시 outline을 왜 없애려고 하셨나요? 별다른 이유가 없다면 none 시키지 않는게 좋아요. 키보드의 tab으로 접근하는 경우에 현재 어느 요소에 접근했는지 알려주기 때문에 대체할만한 선택지 없이 지우는건 지양해야 할 것 같네요. 이건 접근성과도 연관되어 있는 부분이라서 알고 있으면 좋을 것 같아요. 디자인을 고려하기 위해서라면 :focus-visible 의사 클래스를 찾아보세요! 😀

  ```css
  /* 키보드로 버튼에 포커스 시 */
  button:focus-visible {
    outline: 3px solid var(--secondary);
  }

  /* 마우스, 터치로 버튼에 포커스 시 */
  button:focus:not(:focus-visible) {
    outline: none;
  }
  ```

  [https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible)

### 테스트 코드

- [#99] 테스트 코드도 변경에 유연해야 한다. <사용자가 입력한 금액만큼 로또가 구매된다.> 는 테스트를를 할 때,

  ```javascript
  test("사용자가 입력한 금액만큼 로또가 구매된다.", () => {
    const inputMoney = 5000;
    const lottoBundle = new LottoBundle();
    const getLottoCount = (money, pricePerTicket) => money / pricePerTicket;

    lottoBundle.createLottoBundle(
      getLottoCount(inputMoney, LOTTO.PRICE_PER_TICKET)
    );
    expect(lottoBundle.lottos.length).toBe(inputMoney / LOTTO.PRICE_PER_TICKET);
  });
  ```

  라고 하였다면, 로또 금액이 변경되면 에러가 발생할 수 있다.
  그러므로, inputMoney도 동적으로 할당해주면 좋다.
  <br/>
  `const inputMoney = PRICE_PER_TICKET * 로또_개수(아무 숫자)`

- toThrowError() 를 통해 어떤 에러 메시지를 보여주는지 확실하게 확인하자.

## 기타 배울 점

- `this.$ticketContainer.classList.replace('hidden', 'show');`

- disable 시켜서 UX 고려

- custom commitizen (#99, #101)
  [참고자료](https://velog.io/@sgd122/git-commitizen%EC%9D%98-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95-%EB%B0%8F-template%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
