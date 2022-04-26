# Level1 로또 Step2 - 시지프

분석 담당 코드

- [#151](https://github.com/woowacourse/javascript-lotto/pull/151)
- [#154](https://github.com/woowacourse/javascript-lotto/pull/154)
- [#146](https://github.com/woowacourse/javascript-lotto/pull/146)
- [#156](https://github.com/woowacourse/javascript-lotto/pull/156)
- [#142](https://github.com/woowacourse/javascript-lotto/pull/142)
- [#140](https://github.com/woowacourse/javascript-lotto/pull/140)
- [#123](https://github.com/woowacourse/javascript-lotto/pull/123)
- [#130](https://github.com/woowacourse/javascript-lotto/pull/130)

## 피드백 정리

### 컨벤션

### 클린코드

- [#142] 데이터가 변경되지 않는 이벤트에 대한 처리는 누가 담당하면 좋을지 궁금합니다.
  예를 들어, ResultModalView에서는 클로즈 버튼을 통해 감지한 이벤트는 데이터가 필요로 하지 않으며 modal을 hide하는 기능에 그칩니다. 이런 경우에도 기존에 구현한 코드처럼 커스텀이벤트를 통해 view에서 controller에게 이벤트가 발생했음을 알리고, 다시 controller가 view에게 지시를 해야하는 절차를 거쳐야 할지 고민이 됩니다. 일관성을 지키려면 그렇게 해야할 것 같긴 한데, 한편으로는 이처럼 데이터가 변경되지 않는 이벤트에 대한 처리의 경우에는 view에서 이벤트 처리까지 다 해줘도 될 것 같다는 생각이 듭니다. 율리님은 어떻게 생각하시는지 궁금합니다.

  > 이건 저는 뷰에서 하는게 더 좋을 것 같습니다. 커스텀 이벤트를 쓸 이유가 없다면 쓰지 않는게 맞죠.

- [#140] 인자가 3개 이상일 경우, 객체형태로 받아오는 것은 어떨까요? 추후에 Typescript를 접하실때 구조분해할당을 통해 원하는 속성만 사용하고 IDE에서 그 속성에 대한 타입힌트를 받을 수 있어 객체형태로 넘기는 연습을 미리 해두시면 좋을 것 같아요 😄

  [참고 - 클린코드 자료](https://github.com/qkraudghgh/clean-code-javascript-ko#%ED%95%A8%EC%88%98functions)

### JS

- [#130] Math.floor vs parseInt

  1. Math.floor('-3.3') vs parseInt('-3.3')
  2. Math는 수학식으로 계산한다는 이야기이기 때문에, parseInt와 같은 캐스팅과는 차이가 있습니다!
     parseInt는 명확하겐, string 형을 number로 만들어주는걸 뜻합니다.
     그러면 string -> number로 변환시 어떤 일이 일어날까요? 일반적으로 박싱과 언박싱이 일어납니다.

     메모리 계층에서 기존 메모리 타입인 string을 갖고 있다가, number 형태의 메모리 블록을 만들고, 그 이후 string을 number로 옮기면서 메모리의 비효율이 일어나게되고, 이는 가비지컬렉션에서 삭제해주어야겠죠.

     Math.floor는 타입 캐스팅은 하지 않고, 오롯 계산만 하기때문에 박싱과 언박싱에서 자유로울 수 있죠.

- [#140] DOM을 생성자에서 모두 할당해주셨네요 👍 저도 별도로 함수로 분리하지 않는편이 맞다고 생각해요!

- [#151] input number에 한글 입력 막는 방법
  keydown 이벤트에서 유효한 데이터의 경우 기억해뒀다가 input 이벤트에서 해당 입력창의 value가 숫자형태가 아니라면 이전에 저장해둔 입력창의값을 다시 넣어주는 식으로요!

- [#151] input에서 영어 입력 막았을 때, command나 control key를 가능하게 하는 방법

  - e.metaKey, e.ctrlKey

- [#146] 이벤트 위임

```javascript
  // before
  bindOnClickResetButton(callback) {
    this.$resetButton.addEventListener('click', (event) => {
      event.preventDefault();
      this.disappearView();
      callback();
    });
  }

  bindOnClickCloseButton(callback) {
    this.$closeButton.addEventListener('click', (event) => {
      event.preventDefault();
      this.disappearView();
      callback();
    });

  // after
  bindOnClickButtons({ resetCallback, closeCallback }) {
    this.$statisticSection.addEventListener('click', (event) => {
      switch (event.target) {
        case this.$resetButton:
          this.removeView();
          resetCallback();
          break;
        case this.$closeButton:
          this.removeView();
          closeCallback();
          break;
    }
    }
```

- [#142] reduce 사용하기

  ```javascript
    calculateProfitRatio() {
      // before
      let totalProfit = 0;
      for (let key in WINNING_PRIZE) {
        totalProfit += WINNING_PRIZE[key] * this.#winningLottoQuantity[key];
      }
      return (totalProfit / this.#cash) * 100;


      //after
      return (
        (Object.keys(WINNING_PRIZE).reduce(
          (prev, key) => prev + WINNING_PRIZE[key] * this.#winningLottoQuantity[key],
          0,
        ) /
          this.#cash) *
        100
      );
    }
  ```

### CSS

- [#140] scroll을 smooth 하게 만드는 방법

  `scroll-behavior: smooth`

  [참고 - 구현 화면](https://salgum1114.github.io/css/2019-04-28-scroll-behavior-smooth/#bottom)

- [#151] display:block 에 관련된 class를 별도로 사용하는게 좋아보여요. picked-numbers-form 네이밍은 필요없어보이고 block으로 display 한다는 정보를 이용해서 범용적으로 만드는게 좋다고 생각해요

  ```javascript
    .picked-numbers-form-display {
      display: block;
    }
  ```

- [#130] position static이 먼저 렌더링 되고, 나머지 속성들은 후에 렌더링 된다. 그러므로, absolute나 fixed와 같은 속성을, static 속성 보다 위에 존재하기 위해 z-index 설정을 따로 설정해줄 필요가 없다.

  [참고 - 쌓임맥락](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)

### 테스트 코드

- [#151] jest에는 함수의 반환값을 mocking할 수 있는데요.
  makeLottoNumbers라는 메서드가 lotto 번호를 생성하고 있으니 해당 메서드를 spyOn이라는 jest함수를 통해 개선해볼 수 있어보여요.
  당첨결과 확인 테스트케이스를 커버하고 싶으시다면 mockReturnValueOnce를 체이닝해서 사용하시면 호출시마다 원하는 로또 번호를 입력할 수 있어요

  ```javascript
  test("결과 확인하기 버튼을 누르면, 당첨 갯수와 수익률이 정확히 계산된다", () => {
    const lottoList = [
      [1, 2, 3, 4, 5, 6], // 3개
      [4, 5, 6, 7, 8, 9], // 6개
      [4, 5, 6, 7, 8, 10], // 5개+보너스볼
      [7, 8, 9, 10, 11, 12], // 3개
      [13, 14, 15, 16, 17, 18], // 0개
    ];

    const pickedNumber = [4, 5, 6, 7, 8, 9, 10];
    const lottoQuantity = 5;

    const model = new Model();
    model.setLottoList(lottoList);
    model.setCash(lottoList.length * LOTTO_PRICE);

    model.makeLottoNumbers = jest
      .fn()
      .mockReturnValueOnce([1, 2, 3, 4, 5, 6])
      .mockReturnValueOnce([4, 5, 6, 7, 8, 9])
      .mockReturnValueOnce([4, 5, 6, 7, 8, 10])
      .mockReturnValueOnce([7, 8, 9, 10, 11, 12])
      .mockReturnValueOnce([13, 14, 15, 16, 17, 18]);

    model.setCash(lottoQuantity * LOTTO_PRICE);
    model.buyLotto(lottoQuantity);
    model.setWinningLottoQuantity(pickedNumber);

    const winningLottoQuantity = model.getWinningLottoQuantity();
    expect(winningLottoQuantity["3개"]).toBe(2);
    expect(winningLottoQuantity["4개"]).toBe(0);
    expect(winningLottoQuantity["5개"]).toBe(0);
    expect(winningLottoQuantity["5개+보너스볼"]).toBe(1);
    expect(winningLottoQuantity["6개"]).toBe(1);
    expect(model.calculateProfitRatio()).toBe(40600200);
  });
  ```

## 기타 배울 점

- 저는 좋은 커밋 메시지를 '커밋 메시지만 봐도 커밋에 담긴 코드를 유추할 수 있거나 이해하는데 도움을 줄 수 있는 것'으로 정의하곤 합니다. 이를 위해서는 저는 커밋 메시지에 what 과 why 가 담겨있어야한다고 생각해요. title 에 what (무엇을 작성했는 지), 내용에 why (왜 이 커밋을 작성했는 지)

- 이건 PR 피드백을 주고받을 때 팁인데요, 피드백에 대한 반영을 확인할 때, 커밋이 많아지게 된다면 내 피드백이 적절히 반영되었는가? 어디서 반영되었는가?를 찾곤 하는데, 코멘트에 대해 커밋넘버를 남겨주면 리뷰할 때 도움이 많이 되더라구요! 저도 현업에서 꼭 커밋넘버 함께 답변을 남깁니다! 다음 리뷰부터 적용해보시면 리뷰어분이 좋아하시지 않을까 ㅎㅎ..

- 그리고 테스트 관련해서도, 테스트는 "성공 케이스보다 실패 케이스에 대해 더 많은 로직이 있어야 합니다" 그러므로 성공 케이스 뿐만 아니라, 실패 케이스도 함께 존재해야해요!
