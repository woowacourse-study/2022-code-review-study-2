# Level1 로또 Step1(83,89,97,99,100,101,102,109) - 시지프

분석 담당 코드

- [#10, 시지프](https://github.com/woowacourse/javascript-vendingmachine/pull/10)
- [#12, 하리](https://github.com/woowacourse/javascript-vendingmachine/pull/12)
- [#30, 동키콩](https://github.com/woowacourse/javascript-vendingmachine/pull/30)
- [#17, 록바](https://github.com/woowacourse/javascript-vendingmachine/pull/17)
- [#3, 자스민](https://github.com/woowacourse/javascript-vendingmachine/pull/3)
- [#4, 호프](https://github.com/woowacourse/javascript-vendingmachine/pull/4)
- [#25, 태태](https://github.com/woowacourse/javascript-vendingmachine/pull/25)
- [#34, 빅터](https://github.com/woowacourse/javascript-vendingmachine/pull/34)
- [#21, 온스타](https://github.com/woowacourse/javascript-vendingmachine/pull/21)
- [#22, 밧드](https://github.com/woowacourse/javascript-vendingmachine/pull/22)

## unit 테스트는 메소드 단위로? 로직 단위로?

- [#10] 메소드 단위로 하자
  테스트 코드 자체가 명세가 되기도 하고,
  유지보수의 대상이기 때문에,
  테스트 코드가 읽기 쉬어야 한다는 점, 좋은 의견인 것 같습니다.
  현재는 validateProductInfo 하나로 검증하고 있기 때문에, 어디에서 에러가 났는지 명확히 확인이 어려울 것 같습니다.

## 타입스크립트 잘 쓰기

- [#4]

  typescript 를 배웠다면 여기 상수들도 변경될 수 없도록 type 을 설정해봤으면 좋겠는데요, 지금은 충분히 ERROR_MESSAGE. DUPLICATED_NAME = '~~~' 로 메세지를 수정할 수 있겠죠?
  typescript 를 이용해서 어떻게 수정되지 않도록 type 을 설정할 수 있을까요?

  `as const`

- [#21]

  이걸 조금 더 타입스크립트를 활용해서 강력하게 고정을 시킬 수 있는 방법이 없을까요? 지금은 "타입 추론"을 이용해서 타입을 정의함과 동시에 데이터를 선언하셨는데요! 어떤 일종의 양식을 만들어서 고정할 수 있겠어요.

  예를들면, ID.APP은 지금은 #이 들어가야한다는 것을 알지만, 추후에 바빠서 ID에 ".app"등의 classname도 추가할 수 있겠어요.
  그걸 타입스크립트적으로 못적도록 강제할 수 있을까요?

  ```typescript
  export const SELECTOR: SelectorType = {
    ID: {
      APP: "#app",
      CONTENT: "#content",
      CHARGE_MONEY_FORM: "#charge-money-form",
      CURRENT_MONEY: "#current-money",
      ADD_ITEM_NAME: "#add-item-name",
      ADD_ITEM_PRICE: "#add-item-price",
      ADD_ITEM_QUANTITY: "#add-item-quantity",
      ADD_ITEM_FORM: "#add-item-form",
    },
    CLASS: {
      CHARGE_MONEY_INPUT: ".charge-money-input",
      COIN_TABLE: ".coin-table",
      NAV_CONTAINER: ".nav-container",
      NAV_BUTTON: ".nav-button",
      ITEM_TABLE_BUTTON_CONTAINER: ".item-table-button-container",
      TABLE_CONTAINER: ".table-container",
      ITEM_TABLE_CONFIRM_BUTTON: ".item-table-confirm-button",
      ITEM_TABLE_DELETE_BUTTON: ".item-table-delete-button",
      ITEM_TABLE_CHANGE_BUTTON: ".item-table-change-button",
    },
  };
  // 온스타 - index signatures 이용
  type IdType = `#${string}`;

  type classType = `.${string}`;

  export type SelectorType = {
    ID: { [idName: string]: IdType };
    CLASS: { [className: string]: classType };
    ID_STRING: { [idStringName: string]: string };
    CLASS_STRING: { [classStringName: string]: string };
  };

  // Vallista - Utility Type - Record + Generic 활용
  type IdType = `#${string}`;

  type classType = `.${string}`;

  type SelectorObjectType<T = string> = Record<string, T>;

  export interface SelectorType {
    ID: SelectorObjectType<IdType>;
    CLASS: SelectorObjectType<classType>;
    ID_STRING: SelectorObjectType;
    CLASS_STRING: SelectorObjectType;
  }
  ```

```

```

## validate는 domain 에서? ui 에서?

- [#12] 도메인에서 하는게 맞다.

  저는 UI에서는 입력값이 정상적인 숫자로 들어왔는지만 검사하면 된다고 생각해요. 너무 많은 유효성검증을 하고있다고 생각해요.
  위의 스크린샷은 전부 도메인에 관한 요구사항이니 상품 도메인을 생성할 때 검증하면 된다고 생각해요.
  상품명의 중복같은 검증은 ProductManagementDomain에서 하는게 맞다고 생각이 들어요.

- [#30, 로이 정] 스스로 찾아보라

  도메인은 무엇이고 뷰는 무엇이죠? 그 둘을 어떤 기준으로 분리하고 계신건가요?
  try catch를 언제 어디서 감싸야 한다고 보시나요? throw는 어디에서 던지면 될까요? 전체 서비스 내에서 error handler를 최소화/공통화 하려면 어떻게 하면 좋을까요?
  이런 질문들에 고민하면서 스스로 답을 찾아가시기 바라요. 제 생각을 말씀드리는게 큰 의미가 있을것 같지 않아요 ^^a

## interface 네이밍 컨벤션

- [#12, 아사님] suffix - Props

  개인적인 취향인데 interface명에 Props를 붙이는걸 선호해요 👀
  이러한 케이스처럼 Impl이 suffix로 붙는게 싫기도하고 type에 props를 일관적으로 붙혀주니 유지보수할때 타입파일 찾기 쉬운면이 있었어요.

  ```typescript
  class Product implements ProductProps {
  ```

- [#10, 월터님] prefix - Connect~

  ```typescript
  class ConnectPopupError implements PopupError
  ```

## 멤버변수 선언을 constructor 안에서? 밖에서?

- [#12] constructor 안에서 선언하자

  생성자에서 초기화해보면 어떨까요?
  클래스에 대한 인터페이스에 대해 타입힌팅을 받을 수 있어요.

    <img width="636" alt="image" src="https://user-images.githubusercontent.com/24906022/160980029-5d24fc02-bf85-40c6-a7f9-1980bd379913.png">

## try/catch는 에러가 날 부분만 감싸야하나

- [#30, 로이 정]
  어느쪽이든 무관합니다. 회사 컨벤션에 따라 early return을 지양하는 팀이라면 (airbnb 등) 전자의 방식을 따르는게 맞겠죠. 다만 개인적인 생각으로는 '에러가 발생할 일이 없다고 판단'하는 로직에 대해서도 100% 확신하지 못한다면 try문 안에 넣는 편이 심리적 안정 측면에서 좋지 않나 싶군요. 반대로 '모든 판단이 종료된 후에야 비로소 수행되어야 하는' 로직이 있다면 try catch 밖에 놓는 편이 안심 될테고요.

## private vs \#

- [#30 로이 정] \#을 써라

  typescript에서의 'private' 선언은 컴파일 후에는 아무런 의미를 갖지 않아 개인적으로 추천하지 않습니다.
  나아가 \_ 대신 실질적인 private의 의미와 동작을 수행하는 #을 이용해 주세요.

## 커밋 단위

- UI + Domain을 하나의 기능으로?
- test 커밋은?

### JS

- [#12] 큰 정수를 입력할때 언더스코어를 이용하면 가독성이 좋아요!

  numeric underscore

  <img width="462" alt="image" src="https://user-images.githubusercontent.com/24906022/160979485-c17f6b44-b6fc-4b6f-9b34-ed6b0a8eb490.png">

## 타입스크립트 제대로 사용하기

- Quiz1 (인터페이스 상속, 유틸리티 타입)

  ```typescript
  interface A {
    itemName: string;
    itemPrice: number;
    itemQuantity: number;
  } // -> ItemInfoType

  const var1: A & { isAddMode: boolean } = {
    itemName: "콜라",
    itemPrice: 1000,
    itemQuantity: 20,
    isAddMode: true,
  };

  const var2: Omit<A, "itemQuantity"> = {
    itemName: "콜라",
    itemPrice: 1000,
  };
  ```

- Quiz2

  ```typescript
  export interface ProductInfo {
    name: string;
    price: number;
    quantity: number;
  }

  // target의 type을 선언하시오

  private focusOnInvalidInput(target: keyof ProductInfo, $inputs: Inputs) {
    switch (target) {
      case 'name':
        $inputs.name.focus();
        break;
      case 'price':
        $inputs.price.focus();
        break;
      case 'quantity':
        $inputs.quantity.focus();
    }
  }

  // 타입스크립트가 왜 안정성이 높다고 하는가?
  ```

- Quiz3

  ```typescript
  // 위의 정답을 통해 $inputs의 타입을 선언하시오.
  type A = { [P in keyof ProductInfo]: HTMLInputElement };

  const $inputs = {
    name: $formElements.namedItem("name") as HTMLInputElement,
    price: $formElements.namedItem("price") as HTMLInputElement,
    quantity: $formElements.namedItem("quantity") as HTMLInputElement,
  };
  ```

- Quiz4

  ```typescript

  const coinType = [10,50,100,500];
  type CoinUnionType = typeof coinType[number];

  type Coins = { [type in CoinUnionType]: number };


  // coins의 type을 어떻게 선언했나요?
  const coins: Coins = {
    10: 0
    50: 0,
    100: 0,
    500: 0,
  }
  ```

- Quiz5

  ```typescript
  // 에러를 해결하시오
  $("abc").addEventListener("click", (e) => {
    if (!(e.target instanceof HTMLElement)) return;
    console.log(e.target.value); // Property 'value' does not exist on type
  });
  ```
