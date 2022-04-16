# Level1 자판기 미션 Step1 - 코카콜라

- [#42, 코카콜라](https://github.com/woowacourse/javascript-vendingmachine/pull/42)
- [#59, 유세지](https://github.com/woowacourse/javascript-vendingmachine/pull/59)
- [#46, 소피아](https://github.com/woowacourse/javascript-vendingmachine/pull/46)
- [#77, 콤피](https://github.com/woowacourse/javascript-vendingmachine/pull/77)
- [#65, 도리](https://github.com/woowacourse/javascript-vendingmachine/pull/65)
- [#60, 우디](https://github.com/woowacourse/javascript-vendingmachine/pull/60)
- [#69, 아놀드](https://github.com/woowacourse/javascript-vendingmachine/pull/69)
- [#55, 해리](https://github.com/woowacourse/javascript-vendingmachine/pull/55)
- [#79, 돔하디](https://github.com/woowacourse/javascript-vendingmachine/pull/79)
- [#68, 마르코](https://github.com/woowacourse/javascript-vendingmachine/pull/68)

---

## 피드백 정리

### 함수/클래스

- [#42, 코카콜라, KeyboardEvent 사용되지 않는 속성](https://github.com/woowacourse/javascript-vendingmachine/pull/42)

- KeyboardEevet.keycode (x) -> KeyboardEvent.key || KeyboardEvent.code
- KeyboardEevet.returnValue (x) -> KeyboardEevet.preventDefault();

```javascript
// before
const { keyCode } = e;
const isSpacebar = keyCode === 32;

if (isSpacebar) e.returnValue = false;

// refactor
const isSpacebar = e.key === " ";
// const isSpacebar = e.code === 'Space'

if (isSpacebar) e.preventDefault();
```

---

### 네이밍

- [#77, 콤피](https://github.com/woowacourse/javascript-vendingmachine/pull/77)

```javascript
// before
 if (isDone === true && isError === false) {
      routingEvent(DEFAULT_PAGE);
      ...
      }

// refactor
if (isDone === true && isError === false) {
      route(DEFAULT_PAGE);
      ...
      }
```

routingEvent() '동작'인데 이름이 너무 단순 명사처럼 보인다. 명백히 '동작'을 표현하는 route() 같은 동사로 바꾸자

---

- [#77, 콤피, 명확한 네이밍](https://github.com/woowacourse/javascript-vendingmachine/pull/77)

사소할 수도 있지만... isExpireSession, isLogin과 같은 경우 isExpiredSession, isLoggedIn 과 같은 이름은 어떻게 생각하시나요?
'로그인인지' vs '로그인 했는지'같은 차이가 있을 것 같아요

- isExpireSession(x), isExpiredSession(o)
- isLogin과(x), isLoggedIn(o)

---

### typescript

- [#77, 콤피, 타입 추론](https://github.com/woowacourse/javascript-vendingmachine/pull/77)

```javascript
// before
private getRandomCoinsFromAmount(amount: number): Array<number> {
    let leftAmount: number = amount;

// refactor
private getRandomCoinsFromAmount(amount: number): Array<number> {
    let leftAmount = amount;
```

### CSS

- [#68, 마르코](https://github.com/woowacourse/javascript-vendingmachine/pull/68)

CSS 파일을 사용하지 않고 내부 스타일 시트를 넣어준 이유가 무엇인가요???

```javascript
const loginTemplate = document.createElement("template");

loginTemplate.innerHTML = `
  <style>
    .modal-container {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100vw;
      height: 100vh;
      position: fixed;
      top: 0;
      left: 0;
      background: transparent;
    }

    .hide {
      display: none !important;
    }

    .dimmer {
        ...
  </style>

  <div class="modal-container" >
    <div class="dimmer"></div>
    <div class="modal-inner" role="dialog">
      <div class="x-shape">X</div>
      <section>
        <h1>로그인</h1>
        <form>
          <label>이메일</label>
          <input id="email-input" type="email" placeholder="woowacourse@gmail.com" />
          <label>비밀번호</label>
          <input id="password-input" type="password" placeholder="비밀번호를 입력해주세요" />
          <button type="submit">확인</button>
        </form>
        <span>아직 회원이 아닌가요? <span id="signup-span">회원가입</span></span>
      </section>
    </div>
  </div>
`;

class Login extends HTMLElement {
  emailInput: HTMLInputElement;
  passwordInput: HTMLInputElement;
  dimmer: HTMLDivElement;

  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
    this.shadowRoot.appendChild(loginTemplate.content.cloneNode(true));
    ...

  }
}
```

웹컴포넌트에서 shadow Dom 내에 있는 CSS의 scope는 해당 커스텀 엘리먼트에 제한되어 캡슐화되는 것으로 알고 있습니다. 이렇게 CSS, HTML, JS가 모여 있으면 나중에 해당 웹컴포넌트들을 재사용할 때 조금 더 유용하지 않을까 싶습니다.
그리고 웹컴포넌트 shadowDom 내부로 외부 CSS 파일을 import하여 사용하는 방법을 찾아본 결과, 인라인 스타일 내부에 @import 해당스타일파일.css 코드를 추가하면 됨을 알게 되었습니다.

[https://css-tricks.com/styling-a-web-component/](https://css-tricks.com/styling-a-web-component/)

---

### 테스트 코드

- [#68, 마르코, alias 활용](https://github.com/woowacourse/javascript-vendingmachine/pull/68)

[alias](https://docs.cypress.io/guides/core-concepts/variables-and-aliases#Sharing-Context)

```javascript
// before
    cy.get('#purchase-tab-coin-500').last().should('have.text', '1');
    cy.get('#purchase-tab-coin-100').last().should('have.text', '4');
    cy.get('#purchase-tab-coin-50').last().should('have.text', '1');
    cy.get('#purchase-tab-coin-10').last().should('have.text', '4');

// refactor
beforeEach(() => {
    // alias
    cy.get('#purchase-tab-coin-500').last().as('coin500');
    cy.get('#purchase-tab-coin-100').last().as('coin100');
    cy.get('#purchase-tab-coin-50').last().as('coin50');
    cy.get('#purchase-tab-coin-10').last().as('coin10');
  });

...
    cy.get('@coin500').should('have.text', '1');
    cy.get('@coin100').should('have.text', '4');
    cy.get('@coin50').should('have.text', '1');
    cy.get('@coin10').should('have.text', '4');

```
