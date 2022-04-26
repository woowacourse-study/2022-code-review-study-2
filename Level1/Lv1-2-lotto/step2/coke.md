# Level1 로또 미션 Step2 - 코카콜라

- [#149, 우연](https://github.com/woowacourse/javascript-lotto/pull/149)
- [#139, 소피아](https://github.com/woowacourse/javascript-lotto/pull/139)
- [#108, 돔하디](https://github.com/woowacourse/javascript-lotto/pull/108)
- [#155, 민초](https://github.com/woowacourse/javascript-lotto/pull/155)
- [#127, 아놀드](https://github.com/woowacourse/javascript-lotto/pull/127)
- [#152, 빅터](https://github.com/woowacourse/javascript-lotto/pull/152)
- [#122, 하리](https://github.com/woowacourse/javascript-lotto/pull/122)
- [#137, 코카콜라](https://github.com/woowacourse/javascript-lotto/pull/137)
- [#148, 록바](https://github.com/woowacourse/javascript-lotto/pull/148)

---

## 로또 미션 회고

- MVC 패턴 같은 디자인패턴에 매몰되어 있었던거 같았다.
- 지금은 이것저것 시도를 해보는 과정이니 vanila javascript에 빠져 봐야겠다.
- 코드를 작성 할 때, 가장 중요한 점은 네이밍인거 같다!

---

## 피드백 정리

### 네이밍

- [#110, 우연](https://github.com/woowacourse/javascript-lotto/pull/149)
  네이밍, 이름이 동사 + 동사인 것 같아요!

```javascript
// before
this.#setEvent();

// refactor
this.#bindEvent();
```

- [#152, 빅터](https://github.com/woowacourse/javascript-lotto/pull/152)
  과거보다 미래의 변화를 예측할 수 있는 이름이 더 좋지 않을까요?

```javascript
// before
renderAfterFareSubmit(lottoList, remainFare) {

// refactor
renderLottoListMatchSection(...
```

- [#148, 록바](https://github.com/woowacourse/javascript-lotto/pull/148)
  isNotDividedIntoUnit 어떨까요? ThousandUnit이라는 변수명은 요구사항이 변경되면 함께 수정해야 하니 좋지 않은 것 같아요

```javascript
// before
export const isNotThousandUnit = value => {

// refactor
export const isNotDividedIntoUnit = value => {
```

### 주석

- [#122, 하리](https://github.com/woowacourse/javascript-lotto/pull/122)
  수학적 계산같은 공식은 주석을 써주자

```javascript
const results = getRanks(this.lottos, numbers);
const totalReward = calculateTotalReward(results);
// 수익률 = (총 상금 / 구매 금액)을 퍼센트 환산
// 즉, 원금 상환 === 수익률 100%
const rewardRate = totalReward / this.lottos.length / 10;
```

### 패턴

- [#137, 코카콜라](https://github.com/woowacourse/javascript-lotto/pull/137)
  옵저버 패턴
  디자인 패턴중에 옵저버 패턴(Observer Pattern) 이 있는데요, 예로써 흔히 addEventListener 로 등록하는 이벤트들이 옵저버 패턴으로 관리되고 있어요!
  https://hoya-kim.github.io/2021/10/26/JavaScript-observer-pattern/
  위의 예시에서

```javascript
class EventManager {
  ...
  listeners: [],

    notify() {
      this.listeners.forEach(listener => listener(this.state));
    },
  ...
}
```

이런 식으로 이벤트를 관리하는 주체가 하나 있는거죠! 보통은 싱글턴으로 인스턴스는 하나만 둡니다.

보통 dispatch 하는 주체는 view 로 두지는 않아서 말씀드린 내용이었어요!
