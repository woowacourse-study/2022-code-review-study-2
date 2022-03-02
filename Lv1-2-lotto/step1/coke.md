# Level1 로또 미션 Step1 - 코카콜라

- [#110, 우연](https://github.com/woowacourse/javascript-lotto/pull/110)
- [#107, 소피아](https://github.com/woowacourse/javascript-lotto/pull/107)
- [#108, 돔하디](https://github.com/woowacourse/javascript-lotto/pull/108)
- [#104, 민초](https://github.com/woowacourse/javascript-lotto/pull/104)
- [#84, 아놀드](https://github.com/woowacourse/javascript-lotto/pull/84)
- [#106, 빅터](https://github.com/woowacourse/javascript-lotto/pull/106)
- [#115, 하리](https://github.com/woowacourse/javascript-lotto/pull/115)
- [#111, 코카콜라](https://github.com/woowacourse/javascript-lotto/pull/111)
- [#103, 록바](https://github.com/woowacourse/javascript-lotto/pull/103)

---

## 아키텍처 분석

- 이번 로또 미션에서 유행?한 MVC 패턴에 대해 생각해본다.(대부분이 MVC패턴을 사용하였기 때문에 PR번호는 없습니다.)

MVC(Model, View, Controller)은 역할 분리를 통해 효율적인 개발을 하는 방법론이다.

그런데 이번 미션을 하면서 개인적으로 불편했다. 데이터를 찾아서 데이터를 변경하고, 이벤트를 수정하고 연결 부분을 찾아서 연결하고 뭔가...참...이렇게 사용하는게 맞는건지 아무튼 불편했다.

그래서 찾아봤다 프론트엔드의 아키텍쳐가 어떻게 변화 되어 가는지! 다음 블로그 포스팅을 보면 어떤 불편함을 극복해서 이러이러한 패턴 같은 아키텍쳐가 나온지 알수 있다.

[프론트엔드에서 아키텍쳐란 무엇인가요? 블로그](https://velog.io/@teo/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C%EC%97%90%EC%84%9C-MV-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)

---

## 피드백 정리

### 아키텍처

- pr 번호, 내용
  - 상세 내용

### 함수/클래스

- [#115, 하리](https://github.com/woowacourse/javascript-lotto/pull/115) private method

객체지향 관점에서 외부로 노출될 메소드들만 public으로 지정해놓는게 좋고, 노출되지 않을 메소드는 private으로 만드는게 좋다!

- [#103, 록바](https://github.com/woowacourse/javascript-lotto/pull/103) 이벤트핸들러는 별도의 메서드로 둬야 한다!

이벤트핸들러를 추가 하는 거 뿐만 아니라 삭제도 가능해야 함으로 별도의 메서드로 둬야 한다. 익명함수로 이벤트핸들러를 구현하면 삭제할 수 없다.

```javascript
// before
addSubmitEvent(submitHandler) {
    this.form.addEventListener('submit', e => {
      e.preventDefault();

      const purchaseMoney = convertToNumber(this.input.value);

      submitHandler(purchaseMoney);
    });
}

// refactor
addSubmitEvent(submitHandler) {
		const event = (e) => {
			e.preventDefault();
			const purchaseMoney = convertToNumber(this.input.value);
	    submitHandler(purchaseMoney);
		}

    this.form.addEventListener('submit', event)
}
```

- [#103, 록바](https://github.com/woowacourse/javascript-lotto/pull/103) new CustomEvent()

MVC패턴에서 Controller와 View의 의존성을 끊기 위해서는 다양한 방법이 있는데, 웹에서는 흔히 customEvent를 활용합니다. View에서 이벤트핸들러를 등록하고, 그 핸들러 내부에서 위의 customEvent를 dispatch한다. Controller에서는 여러가지 customEvent를 수신해서 동작을 수행합니다.
[new CustomEvent() mdn](https://developer.mozilla.org/ko/docs/Web/API/CustomEvent/CustomEvent)

### 컨벤션

- [#104, 민초](https://github.com/woowacourse/javascript-lotto/pull/104) 네이밍, 전치사 사용을 자제하자

```javascript
// bad
const showNumberOfLottos = (length) => {

// refactor
const showNumberLottos = (length) => {
```

- [#111, 코카콜라](https://github.com/woowacourse/javascript-lotto/pull/111) css 파일명
  - CSS 파일 이름에는 az, 숫자 0-9, 밑줄 (\_) 및 하이픈 (-) 만 사용해야 한다.
  - 모두 소문자로 구성 되어야 한다.
  - 파일 이름은 문자로 시작해야 한다.

### DOM

- [#110, 우연](https://github.com/woowacourse/javascript-lotto/pull/110) insertAdjacentHTML 사용

innerHTML 보다 성능적으로 우수한 insertAdjacentHTML 을 사용하자.

- [HTML 요소 관련 읽으면 좋을 포스팅](https://velog.io/@apricotsoul/HTML-section%EC%9A%94%EC%86%8C-main-%EC%9A%94%EC%86%8C)

### CSS

- [#115, 하리](https://github.com/woowacourse/javascript-lotto/pull/115) global css variable 사용해 보자

전역으로 사용될 컬러를 따로 관리해 볼 것

```css
// global.css

:root {
  --main-bg-color: #e5e5e5;
  --app-bg-color: #ffffff;
  --input-color: #b4b4b4;
  --button-bg-color: #00bcd4;
  --button-text-color: #ffffff;
  --toggle-off-bar-color: rgba(0, 0, 0, 0.15);
  --toggle-off-button-color: rgba(33, 33, 33, 0.08);
  --toggle-on-bar-color: #80deea;
  --toggle-on-button-color: #00bcd4;
}

// index.css

@import "./global.css";

body {
  display: flex;
  justify-content: center;
  align-items: center;
  background: var(--main-bg-color);
}

#app {
  display: flex;
  flex-direction: column;
  width: 414px;
  min-height: 727px;
  padding: 0 16px 10px;
  background: var(--app-bg-color);
}
```

- [#115, 하리](https://github.com/woowacourse/javascript-lotto/pull/115) font-family, 최소 한 개의 generic family 추가하기

만약 Roboto 폰트를 로드 하지 못하면 대체 할, 최소 한 개의 generic family를 추가하기

```css
body section {
  font-family: Roboto, sans-serif;
  ...;
}
```

- [#115, 하리](https://github.com/woowacourse/javascript-lotto/pull/115) -webkit-등을 붙이는 것 보다는 autoprefixer 플러그인를 적용하자

웹팩을 사용하기 때문에 브라우저에 맞게 자동으로 수정해 주는 [autoprefixer](https://github.com/postcss/autoprefixer)를 사용하자

autoprefixer, postcss, postcss-loader 설치

```javascript
// webpack.config.js

module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader',
          'postcss-loader'
        ],
      },
...
    ],
```

### 테스트

- [테스트 관련 읽어 보면 좋은 포스팅](https://blog.kingbbode.com/52)

- [#110, 우연](https://github.com/woowacourse/javascript-lotto/pull/110) 테스트명에 상황과 결과에 대한 내용을 담는다.

```javascript
// before
it('구입 금액은 정수인 숫자로 입력해야한다.', () => {

// refactor
it('구입 금액이 정수인 숫자가 아닌 경우 에러 메세지를 띄워준다.', () => {

```

### 가독성

- [#110, 우연](https://github.com/woowacourse/javascript-lotto/pull/110) 정해진 횟수만큼 반복 시, while → for문으로 변경

```javascript
// before
let currentCount = 0;
while (currentCount < count) {
  this.#lottos.push(new Lotto());
  currentCount += 1;
}

// refactor
let currentCount;
for (currentCount = 0; currentCount < count; currentCount += 1) {
  this.#lottos.push(new Lotto());
  currentCount += 1;
}
```

### 함수 분리, 선언

- [#110, 우연](https://github.com/woowacourse/javascript-lotto/pull/110) 불필요한 함수 분리 및 선언 하지 말 것!

1. this.#numbers를 호출하는 함수 안에서 제어하자.
2. 불필요하게 함수로 분리하지 말자. 생성자 함수(constructor())에서 this.#numbers를 구현하자.
   - generateNumbersAutomatically()메서드가 생성자에서만 사용되고 외부로 노출 할 필요가 없기 때문에 분리 할 필요성이 없다.

```javascript
// before
class Lotto {
	#numbers;

	constructor() {
	  this.#numbers = this.generateNumbersAutomatically();
	...
	}

	generateNumbersAutomatically() {
		const pickNewNumbers = new Ser();
	...
		return pickNewNumbers;
	}

	get numbers() {
	    return this.#numbers;
	}
}
```

```javascript
// refactor - 1  this.#numbers를 호출하는 함수 안에서 제어하자.
class Lotto {
	#numbers;

	constructor() {
		this.generateNumbersAutomatically();
	...
	}

	generateNumbersAutomatically() {
		const pickNewNumbers = new Ser();
	...
		this.#numbers = pickNewNumbers;
	}

	get numbers() {
	    return this.#numbers;
	}
}
```

```javascript
// refactor - 2  불필요하게 함수로 분리하지 말자.
class Lotto {
	#numbers;

	constructor() {
		const pickNewNumbers = new Set();
	...
		this.#numbers = pickNewNumbers;
	}

	get numbers() {
	    return this.#numbers;
	}
}
```

- [#103, 록바](https://github.com/woowacourse/javascript-lotto/pull/103) constructor()은 initiation 이다

무의미한 메서드를 만들어서 초기화를 시켜주는 대신 constructor에 멤버변수로 초기화 해주자

```javascript
// before
constructor(){
...
}

#init() {
    this.#numberList = pickLottoNumber(RULES.LOTTO_NUMS);
}

// refactor
constructor(){
    this.#numberList = pickLottoNumber(RULES.LOTTO_NUMS);
...
}
```

### 기타

- [#103, 록바](https://github.com/woowacourse/javascript-lotto/pull/103) 굳이, 너무, 오버스팩, 과하게 만드는게 아닐까?

상수는 대문자로 쓴다는 일반적인 컨센서스가 있기 때문에, 어지간하면 이 값을 변경하고자 시도하는 사람은 없을 텐데 과하게 Object.freeze()를 사용해서 오버 했다. 정말 이 코드가 필요한지 생각하고 작성하자

```javascript
// src/js/constants/index.js

const RULES = Object.freeze({
  LOTTO_PRICE: 1000,
  LOTTO_NUMS: 6,
  MIN_LOTTO_NUMBER: 1,
  MAX_LOTTO_NUMBER: 45,
});
```
