## Level-1 자판기 Step2 - 안

#### 분석 담당 코드

- [#64](https://github.com/woowacourse/javascript-vendingmachine/pull/64) 안 v
- [#51](https://github.com/woowacourse/javascript-vendingmachine/pull/51) 우연 v
- [#49](https://github.com/woowacourse/javascript-vendingmachine/pull/49) 샐리 v
- [#61](https://github.com/woowacourse/javascript-vendingmachine/pull/61) 준찌 v
- [#78](https://github.com/woowacourse/javascript-vendingmachine/pull/78) 위니 v
- [#71](https://github.com/woowacourse/javascript-vendingmachine/pull/71) 티거 v
- [#74](https://github.com/woowacourse/javascript-vendingmachine/pull/74) 후이 v
- [#62](https://github.com/woowacourse/javascript-vendingmachine/pull/62) 꼬재 v

## 피드백 정리

- [#51](https://github.com/woowacourse/javascript-vendingmachine/pull/51#discussion_r845100836) cypress-wait-until plugin

```js
// before

cy.get("#password-input").type(password);
cy.get("button").click();

cy.wait(1000);

// after

import "cypress-wait-until";

Cypress.Commands.add("login", (email, password) => {
  cy.get("#email-input").type(email);
  cy.get("#password-input").type(password);
  cy.get("button").click();

  cy.waitUntil(() =>
    cy.location("pathname").should("eq", "/dist/manager.html")
  );
});
```

- [#51] 스토리지 객체

```js
// before

export const getLocalStorage = (key) => {
  return JSON.parse(localStorage.getItem(key));
};

export const setLocalStorage = (key, value) => {
  localStorage.setItem(key, JSON.stringify(value));
};

// after

const storeFactory = (storage) => ({
  get(key) {
    return JSON.parse(storage.getItem(key));
  },
  set(key, value) {
    storage.setItem(key, JSON.stringify(value));
  },
  remove(key) {
    storage.removeItem(key);
  },
});

export const localStore = storeFactory(localStorage);
export const sessionStore = storeFactory(sessionStorage);
```

- [#78](https://github.com/woowacourse/javascript-vendingmachine/pull/78#discussion_r846564907) validator 추상화

```js
// before

if (isUnderMinPrice(price)) {
  throw new Error(ERROR_MESSAGE.IS_UNDER_MIN_PRICE);
}
if (isOverMaxPrice(price)) {
  throw new Error(ERROR_MESSAGE.IS_OVER_MAX_PRICE);
}
if (cannotDividedByTen(price)) {
  throw new Error(ERROR_MESSAGE.PRICE_CANNOT_DIVIDED_BY_TEN);
}

// after

const validator = (conditions) => {
  conditions.forEach(({ checker, errorMsg }) => {
    if (checker()) throw new Error(errorMsg);
  });
};

validator([
  {
    checker: () => isBlank(name),
    errorMsg: ERROR_MESSAGE.IS_BLANK_PRODUCT_NAME,
  },
  {
    checker: () => isOverMaxProductNameLength(name),
    errorMsg: ERROR_MESSAGE.IS_OVER_MAX_PRODUCT_NAME_LENGTH,
  },
```

- [#71](https://github.com/woowacourse/javascript-vendingmachine/pull/71#discussion_r846652945) 사용자 경험

로그인 화면에서는 아이디(이메일), 비밀번호 유효성 검사를 하고 에러 메세지로 친절하게 뭐가 틀렸다 라고 알려주지 않는 편입니다. 본인 외에 다른사람이 로그인 시도시 일말의 힌트를 주는 상황이 될 수 있어서 보통은 로그인 정보가 올바르지 않다 라고 표현하는 편이에요! 그러나 이것도 회사마다 정책이 있기 때문에 제 이야기는 그냥 참고만 하시면 될 것 같네요.

- [#62](https://github.com/woowacourse/javascript-vendingmachine/pull/62/files/f77f039f41166e45d67c107569d51bd5bf633cf0#r847362869)

> 우리가 생각하는 것보다 소프트웨어는 빨리 녹이 슨다.
