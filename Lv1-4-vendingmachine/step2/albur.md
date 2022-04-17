# Level-3 유튜브 Step2 - 앨버

- 분석 담당 코드

  - [#48](https://github.com/woowacourse/javascript-vendingmachine/pull/48)
  - [#53](https://github.com/woowacourse/javascript-vendingmachine/pull/53)

  - [#66](https://github.com/woowacourse/javascript-vendingmachine/pull/66)
  - [#57](https://github.com/woowacourse/javascript-vendingmachine/pull/57)

  - [#56](https://github.com/woowacourse/javascript-vendingmachine/pull/56)
  - [#75](https://github.com/woowacourse/javascript-vendingmachine/pull/75)

  - [#67](https://github.com/woowacourse/javascript-vendingmachine/pull/67)
  - [#47](https://github.com/woowacourse/javascript-vendingmachine/pull/47)

## 다른 크루들 코드 분석

#### 라우터 구현방법 (라우터 함수?)

- [[#66](https://github.dev/woowacourse/javascript-vendingmachine/pull/66)]

  - Whitelist를 상수로 선언해줘서 허용된 url들을 관리해주었다.
  - Router 클래스에 싱글톤 패턴을 적용시켜서 해당 클래스를 전역에서 사용해주는 방식으로 해주었다.
  - url이 바껴야할 때마다 `Router.pushState()`를 호출해주고 이에 따라서 모든 컴포넌트에 `notify()`를 호출해주는 방식으로 라우터를 구현하였다.

    ```javascript

    class Router {
      static _instance?: Router;

      private listeners: Array<RouteComponent> = [];

      constructor() {
        if (Router._instance) {
          return Router._instance;
        }
        window.addEventListener('load', this.onLocationChange);
        window.addEventListener('pushstate', this.onLocationChange);
        window.addEventListener('popstate', this.onLocationChange);
      }

      static get instance() {
        if (!Router._instance) {
          Router._instance = new Router();
        }
        return Router._instance;
      }

      static pushState(url: string) {
        history.pushState({}, '', url);
        window.dispatchEvent(new Event('pushstate'));
      }

      addListener(component: RouteComponent) {
        this.listeners.push(component);
      }

      getCurrentPath() {
        const { pathname } = window.location;
        return pathname;
      }

      isNotFound() {
        const currentPath = this.getCurrentPath();
        return Object.keys(WhiteList).every(
          (key) => WhiteList[key as keyof typeof WhiteList] !== currentPath
        );
      }

      onLocationChange = () => {
        if (this.isNotFound()) {
          location.href = location.origin;
          return;
        }
        this.notify();
      };

      notify() {
        this.listeners.forEach((component) => component.onLocationChange());
      }
    }

    export default Router;


    ```

- switch문으로 routing

- [#47](https://github.com/woowacourse/javascript-vendingmachine/pull/47)

  ```javascript
  window.addEventListener('popstate', () => {
    this.convertTemplate(location.hash || '#product');
    // ...생략
  });

  convertTemplate = (path: string) => {
    const routes = {
      '#login': () => this.login.render(),
      '#signup': () => this.signup.render(),
      '#editMember': () => this.editMember.render(),
      '#product': () => this.product.render(),
      '#charge': () => this.charge.render(),
      '#purchase': () => this.purchase.render(),
    };

    this.menuTab.render(path);
    routes[path]();
  };

  // this.menuTab.render(path)
  render(path: string) {
    if (path === "#login" || path === "#signup" || path === "#editMember") {
      this.vendingmachineHeader.replaceChildren();
      return;
    }

    if (this.vendingmachineHeader.children.length === 0) {
      this.vendingmachineHeader.insertAdjacentHTML(
        "beforeend",
        `${this.renderVendingmachineHeader(JSON.parse(localStorage.getItem("USER_NAME")))}`
      )
    }
  }
  ```

#### api 내부 에러핸들링

- 대부분 `!response.ok`를 활용해서 에러 핸들링을 해주었다.

#### class를 위한 interface 모습?

- interface를 따로 작성하지 않는다.
- class를 위한 interface를 interface.ts에 모아둔다.
- class를 위한 interface는 class 선언부 위에 위치시킨다.

## 피드백 정리

#### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)

<br>

- [[#48](https://github.com/woowacourse/javascript-vendingmachine/pull/48/files/f5da7a76650a36f476d9aea57dac9e91a1fa4d0f#discussion_r846557211) - 렌더링 최적화]

  ```javascript
  if (this.#isRendered) {
    this.#updateThumbnail();

    return;
  }
  ```

  이미 화면에 렌더링이 되어 있는 상태일때는 전체를 다시 렌더링 하는 것이 아니라 변경된 부분만 렌더링하면 렌더링 적으로 최적화를 이뤄낼 수 있다.

<br>

- [[#66](https://github.com/woowacourse/javascript-vendingmachine/pull/66#discussion_r845252803) - import 절대경로]

  ```javascript
  import Component from '../../abstract/component';
  import { ACTION } from '../../constants';
  ```

  위의 상대경로를 [babel-plugin-module-resolver](https://www.npmjs.com/package/babel-plugin-module-resolver)을 활용해서 절대경로로 사용해줄 수 있다.

<br>

- [[#57](https://github.com/woowacourse/javascript-vendingmachine/pull/57#discussion_r845991012) - DOM에 의존하는 로직]

  ```javascript
  onClickLoginConfirmBtn = () => {
    const [$email, $password] = this.querySelectorAll('input');
  ```

  - 무언가의 이유로 template 이 변경된다면 불필요하게 사이드이펙트가 발생하게 될 것 같아용. 보통 input 은 고유하니 id 를 부여해 가져오는 게 좋을 것 같습니다!

<br>

- [[#56](https://github.com/woowacourse/javascript-vendingmachine/pull/56#discussion_r846597202) - 명시적 타입 추론은 언제 안해줘도 되는지?]

  - 타입스크립트를 사용하다 보면, 자동으로 타입을 추론해줄 때가 있다. 어떨 때 해주고 어떨 때 해주지 않는지 헷갈리기 때문에 명시적으로 타입을 설정해주는 시기가 애매해진다.그럴때는 vscode의 힘을 빌리면 된다. 함수나 변수에 마우스를 호버하면 타입이 표기되기 때문이다.

<br>
