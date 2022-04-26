# Level1 자판기 Step2() - 시지프

분석 담당 코드

- [#45, 블링](https://github.com/woowacourse/javascript-vendingmachine/pull/45)
- [#63, 태태](https://github.com/woowacourse/javascript-vendingmachine/pull/63)
- [#61, 호프](https://github.com/woowacourse/javascript-vendingmachine/pull/61)
- [#61, 빅터](https://github.com/woowacourse/javascript-vendingmachine/pull/61)
- [#72, 록바](https://github.com/woowacourse/javascript-vendingmachine/pull/72)
- [#43, 하리](https://github.com/woowacourse/javascript-vendingmachine/pull/43)
- [#50, 밧드](https://github.com/woowacourse/javascript-vendingmachine/pull/50)

## 코드 분석

- 로그인 확인 어떻게 했는지

  - 매번 API call을 하면 낭비이다.

    - [#43, 하리]

    isSignin flag를 사용했음. 창을 다시 킬때마다 호출하게 됨.

- API 어떻게 정리했는지

  - 추상화 잘 한 사람이 있는가...

  - [#43] 아사님의 추상화

  ```typescript
  interface WoowaRequestProps {
    url: string;
    method?: "GET" | "POST";
    contentType?: "json" | "formData" | "html";
    requestBody?: string;
  }
  const contentTypeMapper: Record<WoowaRequestProps["contentType"], string> = {
    formData: "multipart/form-data",
    html: "text/html",
    json: "application/json",
  };

  async function woowaRequest<T>({
    url,
    contentType,
    method = "GET",
    requestBody,
  }: WoowaRequestProps): Promise<T | null> {
    try {
      const response = await fetch(url, {
        method,
        ...(requestBody && { body: requestBody }),
        headers: {
          ...(contentType && {
            "Content-Type": contentTypeMapper[contentType],
          }),
        },
      });

      if (!response.ok) {
        return null;
      }

      if (response.status !== 200 && response.status !== 201) {
        throw Error();
      }

      return response.json() as Promise<T>;
    } catch (error) {
      // Logging Error With Logging System
      return null;
    }
  }
  ```

- 에러 처리 어떻게 했는지 (try-catch)

- fetch, json()이 실패했을 때를 체크해주어야 한다. response.ok 로 확인하는것은 이미 정상적으로 통신했다는 가정 하에 코드를 짜는 것

  - 준
    한단계 추상화했을 뿐만 아니라, 객체의 책임과 관련된 부분까지 고민해서 작업한 점이 너무 인상적이에요 👍🏻
    그런데 const data = await response.json();이 부분에서 response.json()이 실패한 경우에 에러 처리는 어떻게 해줘야할지도 고민되는 것 같아요. fetch API 사용하는 로직은 앞으로도 계속 사용하는 부분이니 이 미션이 아니어도, 다음 미션에서 반영해보면 좋을 것 같아요!

  - 오스틴
    tryCatch 문법으로 되어있다면 가독성 측면에서 코드를 파악하기 쉽고, 위에 말씀 주신 오류 상황을 throw해서 view에서 해당 오류를 스낵바에 렌더링 해주는 것이 적절하다고 생각했기 때문입니다.을 처리를 할 수 있다고 생각해서 말씀드렸습니다.
    그리고 지금은 서버에서 응답이 온다는 가정하에 코드가 작성되어 있는데 예상치 못한 어떤 이슈가 발생해 스크립트가 중단되는 상황이 발생할 수 있습니다.
    tryCatch 문법을 사용하면 스크립트가 중단되는 것을 방지하고, catch을 통해 방어코드를 작성할 할 수 있습니다.

- SPA 구조 (라우팅 방법, 컴포넌트 구성)
- test API mocking

블링 - rAF

## 피드백 정리

### 컨벤션

### 클린코드

### 성능

### 설계

- [#45, 블링](https://github.dev/woowacourse/javascript-vendingmachine/pull/45) Authorization를 클래스로 만들어, 관련 코드를 모아둔 것

### JS

- [#63, 태태](https://github.dev/woowacourse/javascript-vendingmachine/pull/63) 고차함수를 이용

- 고차함수란? (Higher-Order-Function) : 고차 함수는 함수를 인자로 받거나 함수를 출력(output)으로 반환하는(return) 함수를 말합니다.

예를 들면, Array.prototype.map, Array.prototype.filter 그리고 Array.prototype.reduce가 언어 내부에 포함된 (built-in) 고차함수입니다. 클로저도 고차함수.

고차 함수는 외부 상태 변경이나 가변(mutable) 데이터를 피하고 불변성(Immutability)을 지향하는 함수형 프로그래밍에 기반을 두고 있다. 함수형 프로그래밍은 순수 함수(Pure function)와 보조 함수의 조합을 통해 로직 내에 존재하는 조건문과 반복문을 제거하여 복잡성을 해결하고 변수의 사용을 억제하여 상태 변경을 피하려는 프로그래밍 패러다임이다. 조건문이나 반복문은 로직의 흐름을 이해하기 어렵게 하여 가독성을 해치고, 변수의 값은 누군가에 의해 언제든지 변경될 수 있어 오류 발생의 근본적 원인이 될 수 있기 때문이다.

```typescript
const postServer = (baseUrl) => (path) => async (bodyData) => {
  const response = await fetch(`${baseUrl}/${path}`, {
    method: "post",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(bodyData),
  });

  return { ok: response.ok, body: await response.json() };
};

const postBaseServer = postServer(BASE_SERVER_URL);

export const postLoginServer = postBaseServer(SERVER_PATH.LOGIN);
export const postRegisterServer = postBaseServer(SERVER_PATH.REGISTER);
```

### 변수명

### TS

- [#76, 빅터](https://github.com/woowacourse/javascript-vendingmachine/pull/76/commits/db1e50baf7b4366dc36beb0c1b5f609aba7b5817) MouseEvent를 커스텀 타입으로 래핑해서, HTMLElement를 넣어보면 어떨까요?

  ```typescript
  export interface DOMEvent extends Event {
    target: HTMLElement;
    key?: string;
  }

  export interface DOMEvent<T extends HTMLElement> extends Event {
    target: T;
    [key: string]: any;
  }
  ```

### 객체지향

### HTML 웹 표준

### CSS

- [#76, 빅터](https://github.com/woowacourse/javascript-vendingmachine/pull/76/commits/5feac4f6a5bed7da56baa10060b3225c02b292bf) z-index를 layer로 따로 분리하여 표현하기

  ```css
  :root {
    --standard: 0;
    --foreground: 50;
    --snackbar: 100;
  }

  z-index: var(--snackbar);
  z-index: var(--foreground);
  ```

### 테스트 코드

- [#45, 블링](https://github.com/woowacourse/javascript-vendingmachine/pull/45) cypress Command 사용

```javascript
Cypress.Commands.add("addProduct", ({ name, price, stock }) => {
  cy.get("#product-tab-menu").click();
  cy.get("#product-name-input").type(name);
  cy.get("#product-price-input").type(price);
  cy.get("#product-stock-input").type(stock);
  cy.get(".submit-button").click();
});

beforeEach(() => {
  cy.addProduct(defaultProduct);
  cy.addChange(defaultChange);

  cy.get("#purchase-tab-menu").click();
});
```

- [#45, 블링](https://github.com/woowacourse/javascript-vendingmachine/pull/45) API mocking

  mocking을 하진 않고, 가로챈 다음에 따로 변수로 지정함. 그냥 API가 호출되지 않도록만 함.

  ```javascript
  Cypress.Commands.add("registerNewUser", (userData) => {
    cy.intercept({
      method: "POST",
      url: "**/users",
    }).as("registerRequest");

    const { email, name, password } = userData;

    cy.get("#login-link-button").click();
    cy.get("#register-page-link").click();

    cy.get("#email-input").type(email);
    cy.get("#name-input").type(name);
    cy.get("#password-input").type(password);
    cy.get("#password-confirm-input").type(password);

    cy.get(".submit-button").click();
    cy.wait("@registerRequest");
  });

  it("회원가입을 마치면 상품관리 페이지로 이동된다.", () => {
    const userData = createRandomUserData();
    cy.registerNewUser(userData);

    cy.get("#product-tab-title").should("exist");
  });
  ```

## 기타 배울 점

try-catch로 fetch 를 감싸야만 하는가?
<img width="547" alt="image" src="https://user-images.githubusercontent.com/24906022/163695570-91468a80-5b6f-4344-a0e6-c0a630082c89.png">
