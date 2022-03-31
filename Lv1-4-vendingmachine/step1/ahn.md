## Level-1 자판기 Step1(31, 23, 18, 36, 37, 24, 14) - 안

#### 분석 담당 코드

- [#31](https://github.com/woowacourse/javascript-vendingmachine/pull/31) 안
- [#23](https://github.com/woowacourse/javascript-vendingmachine/pull/23) 우연
- [#18](https://github.com/woowacourse/javascript-vendingmachine/pull/18) 샐리
- [#13](https://github.com/woowacourse/javascript-vendingmachine/pull/13) 준찌
- [#36](https://github.com/woowacourse/javascript-vendingmachine/pull/36) 위니
- [#37](https://github.com/woowacourse/javascript-vendingmachine/pull/37) 티거
- [#24](https://github.com/woowacourse/javascript-vendingmachine/pull/24) 후이
- [#14](https://github.com/woowacourse/javascript-vendingmachine/pull/14) 꼬재

## 피드백 정리

> [#31] 현재 ts interface 파일을 따로 분리하여 작성하였습니다. 하지만 굳이 interface 파일을 따로 분리할 필요가 있는지 아니면, 범용적으로 사용하는 부분만 따로 만들어서 사용을하고, 특정 클래스에서만 사용되는 부분은 클래스 파일 안에 사용해도 괜찮은지 궁금합니다.

말씀하신 것처럼 범용적으로 사용되는 경우만 하나의 공통의 파일에서 관리하고 특정 파일에만 적용되는 영역은 해당 파일에서 관리하는게 보다 나은 방식이라고 생각합니다
<br>

- [#23](https://github.com/woowacourse/javascript-vendingmachine/pull/23#discussion_r835850970)

```js
// before

on(SECTION_CONTAINER, "@render", this.#renderSavedData.bind(this));
on(SECTION_CONTAINER, "@manage", this.#handleProductInfo.bind(this));
on(SECTION_CONTAINER, "@modify", this.#modifySavedData.bind(this));
on(SECTION_CONTAINER, "@delete", this.#deleteSavedData.bind(this));
on(SECTION_CONTAINER, "@charge", this.#handleChargeCoin.bind(this));
```

```js
// after

on(SECTION_CONTAINER, [
  ['@render', this.#renderSavedData],
  ['@manage', this.#handleProductInfo],
  ...
])

// 2)
on(SECTION_CONTAINER, [
  { event: '@render', handler: this.#renderSavedData },
  { event: '@manage', handler: this.#handleProductInfo },
  ...
])
```

<br>

- [#23] 타입스크립트의 장점
  - 타입오류를 런타임 이전에 바로바로 잡아주고, 오류 발생 가능성을 크게 줄여줍니다. (과장 보태서 자바스크립트 개발자가 겪는 오류상황의 90%가 undefined / null error라는 얘기도 있을 정도라..)
  - ts가 프로젝트 내의 모든 파일 구성을 이미 알고 있어서 변수 import시 / 프로퍼티 호출시 바로바로 찾아서 제안해줍니다.

<br>

- [#23](https://github.com/woowacourse/javascript-vendingmachine/pull/23#discussion_r835852346)
  typescript에서의 'private' 선언은 컴파일 후에는 아무런 의미를 갖지 않아 개인적으로 추천하지 않습니다.

<br>

- [#14] 이벤트 위임

```js
// before

on(this.productTableTbody, "click", this.onClickEditButton);
on(this.productTableTbody, "click", this.onClickDeleteButton);
on(this.productTableTbody, "click", this.onClickEditSubmitButton);
```

```js
//after

onClickProductList (event) => {
  if (event.target.matches('.product-table__confirm-button')) {...}
  if (event.target.matches('.product-table__input--edit')) {...}
  if (event.target.matches('.product-table__delete-button')) {...}
};
```

- [#31] 적절한 중간값을 넣을 경우는 예외상황을 확인하기 어려운 경우가 많습니다. 항상 경계값을 가지고 테스트를 해보시고 특히 랜덤함수를 활용하는 로직이라면 같은 케이스에 대해서도 충분히 많은 횟수를 반복해서 테스트 해봐야 합니다 (예: 구입금액 10원 입력 후 잔돈으로 변환 \* n). 사람이 직접 하는건 효율성이 굉장히 떨어지므로 이런 경우에 테스트 코드의 활용이 필요해 집니다.
