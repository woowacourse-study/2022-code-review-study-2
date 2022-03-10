## 🎯 Level-1 lotto Step2(114, 105, 95, 94, 93, 98, 88, 91) - 안

- 분석 담당 코드

  - [#114](https://github.com/woowacourse/javascript-lotto/pull/114) 안 o
  - [#105](https://github.com/woowacourse/javascript-lotto/pull/105) 코이 o

  - [#95](https://github.com/woowacourse/javascript-lotto/pull/95) 나인 o
  - [#94](https://github.com/woowacourse/javascript-lotto/pull/94) 비녀 o

  - [#93](https://github.com/woowacourse/javascript-lotto/pull/93) 후이 o
  - [#98](https://github.com/woowacourse/javascript-lotto/pull/98) 콤피 o

  - [#88](https://github.com/woowacourse/javascript-lotto/pull/88) 블링 o
  - [#91](https://github.com/woowacourse/javascript-lotto/pull/91) 태태 o

## ✅ 피드백 정리

- [[#114 - 유효성 검사]](https://github.com/woowacourse/javascript-lotto/pull/153#discussion_r820127380)
  부정문은 가급적 지양헤야 한다!!
  Not이 들어가게 되어 새로운 혼란을 야기하는 원인이 된다는 측면에서 바람직하지 않다.

```js
isUnderMinimum;
isOverlap;
isOutOfRange;
isNotNumber; // 'not' 어쩔수 없으면 사용 가능
```

- [[#144 - 피드백 팁]](https://github.com/woowacourse/javascript-lotto/pull/144#pullrequestreview-901555876)
  피드백 받을때 커밋 번호를 같이 남겨주면 읽기 좋타!! 🍯

- [[#145 - 줄 간격]](https://github.com/woowacourse/javascript-lotto/pull/145#discussion_r820227818)
  의미있는 줄 간격을 사용하여 읽기 편하다

```js
checkValidWinningNumberInput(
  winningNumbers.concat(bonusNumber).filter((number) => number)
);

const winningLotto = new WinningLotto().generate(winningNumbers, bonusNumber);

this.#WinningLottoCounter.setWinningLotto(winningLotto);
this.#WinningLottoCounter.calculateWinningCounts(this.#LottosModel.lottos);
this.#ResultModalView.showResultModal();
this.#ResultModalView.renderHitCount(this.#WinningLottoCounter.winningCounts);

const profitRate = this.#WinningLottoCounter.getProfitRate(
  this.#LottosModel.chargedMoney
);

this.#ResultModalView.renderProfitRage(profitRate);
```

- [[git 브랜치 배우기]](https://learngitbranching.js.org/?locale=ko)
  ⬅️ 사이트 - 작은 단위를 커밋하는 습관 기르기!

- [[#124 - switch문]](https://github.com/woowacourse/javascript-lotto/pull/124#discussion_r820046647)
  case 3, case 4 이런식으로 하는게 먼가 어색해서 나는 if문으로 작성하였다.<br>
  if문은 한눈에 count === 3 으로 확인이 가능하다.

```js
// if
#getLottoStatus(count, bonus) {
  if (count === 3) {
    this.winningStatus[0]++;
  }
  if (count === 4) {
    this.winningStatus[1]++;
  }
  if (count === 5 && bonus === 0) {
    this.winningStatus[2]++;
  }

// switch
switch (count) {
  case 3:
    this.winningStatus[0]++;
    break;
  case 4:
    this.winningStatus[1]++;
    break;
  case 5:
    if (count === 5 && bonus === 0) {
      this.winningStatus[2]++;
      break;
    }
```

- [[#124 - 질문]](https://github.com/woowacourse/javascript-lotto/pull/124#issuecomment-1059713765)
  <br>
- MDN 문서에서 자바스크립트와 같은 대부분의 고수준 언어에서는 암묵적으로 필요가 없어지면 메모리에서 해제한다. 라고 하였는데요
  그렇다면 js에서는 생성된 인스턴스에 대한 메모리를 원할 때 해제하는 방법이 없나요?

  - 메모리를 직접 해제 시킬 수는 없고 메모리에 할당된 인스턴스의 참조를 개발자가 null 값을 할당해서 참조를 끊어 주는게 다일것이다.

- jest는 UI 단위 테스트를 할 수 없나요?

  - ui를 테스트하는건 다른 test 툴을 이용하는 것 같네요. 🙂

- [[#134 - 포코]](https://github.com/woowacourse/javascript-lotto/pull/134#pullrequestreview-901166053)
  학습을 위한 요구사항 구현인지 로또 앱 요구사항을 위한 코드 적용인지 항상 잘 고민해보시고 어느정도 선까지 타협할 것인가..생각해보세요.
  때로는 학습을 위한 챌린지보다 요구사항 그 자체를 잘 구현하는게 더 많은 성장을 가져다줄 수 있습니다.

- [[#134 - input 속성]](https://github.com/woowacourse/javascript-lotto/pull/134#discussion_r820330666) `const bonusNumber = Number(this.bonusNumberInput.value);`일일이 형변환하는 코드가 계속 반복된다.
  valueAsNumber 라는 속성도 있다!!

- [[#134 - 논리 로직]](https://github.com/woowacourse/javascript-lotto/pull/134#discussion_r820462092)
  단축 평가와 비슷하게 생각하는게 좋아요.
  &&와 || 두 경우 논리의 흐름에 따라 어느게 더 빠른 판정이 나올 수 있는지 다른 것처럼 말이죠.
  네이밍 컨벤션이나 다양한 부분을 고려할 수 있지만 논리 로직으로 불필요한 리소스 소모를 줄일 수 있다

- [[#134 - 메소드 네임]](https://github.com/woowacourse/javascript-lotto/pull/134#discussion_r820361434)
  on과 handle 을 보통 이벤트를 받는 함수엔 많이 사용하는데요,
  두 개의 네이밍 차이는 뭘까요?
  보통 on는 어떤 이벤트가 연결될지, handle는 어떤 이벤트가 발생했을 때 어떤 것이 호출 될지를 의미한다

- [[#134 - 뎁스]](https://github.com/woowacourse/javascript-lotto/pull/134/files/1174ab77e3602dd229ea64a3d6f5c84c3460a386#r820362523)

```js
  #moveToNextInput(winningInput, bonusInput) {
    const { nextElementSibling } = winningInput;

    if (winningInput.value.length >= LOTTO_NUMBER.DIGIT_MAX && nextElementSibling) {
```

if (winningInput.value.length >= LOTTO_NUMBER.DIGIT_MAX) 를 가장 밖으로 묶고,
내부에 if (nextElementSibling) else 형태로 가는게 더 깔끔하지 않을까요?
뎁스를 깊게하지 않으려고 고민을 많이 한 흔적인데요!
나름 깊은것도 괜찮을때가 있답니다!


## 🚀 로또 미션 회고

- 커스텀 이벤트를 공부해 봐야겠다
- 바닐라 js가 제일 중요하다!!!
- 요구사항을 다했다고 끝이 아니라 -> 지속적인 리팩토링!
- 정답은 없다. '무조건 ~하면 안된다' 가 아니라 때론 사용할 필요가 있기 때문에 이유가 있으면 사용한다!
