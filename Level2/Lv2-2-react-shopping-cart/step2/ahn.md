## Level2 장바구니 Step2 - 안

### 분석 담당 코드

- [#135, 안](https://github.com/woowacourse/react-shopping-cart/pull/135)
- [#128, 코카콜라](https://github.com/woowacourse/react-shopping-cart/pull/128)
- [#110, 태태](https://github.com/woowacourse/react-shopping-cart/pull/110)
- [#109, 소피아](https://github.com/woowacourse/react-shopping-cart/pull/109)
- [#129, 록바](https://github.com/woowacourse/react-shopping-cart/pull/129)
- [#122, 샐리](https://github.com/woowacourse/react-shopping-cart/pull/122)
- [#117, 나인](https://github.com/woowacourse/react-shopping-cart/pull/117)
- [#111, 도리](https://github.com/woowacourse/react-shopping-cart/pull/111)

## 질문사항

- 장바구니 상품 체크 어떻게 구현 하였는가?

1. 상품 체크 상태를 저장한다
2. 장바구니 페이지에 오면 자동으로 모든 상품을 체크한다
   <br>

- useEffect dependency eslint 경고

1. 변경되지 않는 부분은 포함하지 않는다
2. 경고 때문에 포함한다

## 피드백 정리

[#135](https://github.com/woowacourse/react-shopping-cart/pull/135/files/df131e37c8a40f7f3d63d439f85376d2dd0bb68b#r880573503)

> 수량을 params로 보내는 것과 body로 보내는 것

id를 params 보내서 quantity도 똑같이 사용하였는데,
처리 결과 값을 넘겨 주기 때문에 body로 보내는 것이 더 맞다고 생각된다.

```js
// 전
rest.put(`${SERVER_PATH.CART}/:id/:quantity`, (req, res, ctx) => {
  const id = +req.params.id;
  const quantity = +req.params.quantity;
  const cartItemIndex = cartList.findIndex((cartItem) => cartItem.id === id);

  cartList[cartItemIndex].quantity = quantity;
  return res(ctx.status(200), ctx.json(cartList));
}),

// 후
const { data } = await axios.put(`${SERVER_PATH.CART}/${id}`, { quantity });

// mock handlers
const quantity = +req.body.quantity;
...
```

<br>

[#110](https://github.com/woowacourse/react-shopping-cart/pull/110#issuecomment-1134830115)

> JS 테스트 구현 시 단위테스트가 가장 기본이 되는 함수들을 테스트하는걸로 시작하는 것처럼 리액트를 구성하는 기본요소들인 state나 props를 기준으로 컴포넌트 테스트를 작성해보는건 어떨까요? 예를 들어 props나 state가 변했을 때 어떤 결과가 나와야하는지? 혹은 state나 props가 변했을 때 영향을 받는 다른 컴포넌트들은 어떤 결과가 나와야하는지? 와 같은 경우가 있겠네요.
> 또는 장바구니의 상품 개수와 체크 유무에 따라 주문정보가 변경되는 결과도 테스트 해볼 수 있지 않을까요? 😲 단순 렌더링 결과는 스토리북으로 대체하고, 즉각적인 로직 테스트나 상태 변화에 따라 결과값이 달라지는 내용에 대해서는 별도의 단위 테스트로 만들어 볼 수 있을 것 같아요!

- state나 props를 기준으로 컴포넌트 테스트
- 장바구니의 상품 개수와 체크 유무에 따라 주문정보가 변경되는 결과
- 단순 렌더링 결과는 -> 스토리북으로 대체
- 즉각적인 로직 테스트, 상태 변화에 따라 결과값이 달라지는 내용 -> 단위 테스트

<br>

[#110](https://github.com/woowacourse/react-shopping-cart/pull/110#discussion_r879422239)

개별적으로 주지않고 한꺼번에 변경가능

```jsx
// 전
font-size: ${({ theme: { fontSize } }) => fontSize.small};
text-align: center;
color: ${({ theme: { color } }) => color.gray01};
background-color: ${({ theme: { color } }) => color.main};
border: 1px solid ${({ theme: { color } }) => color.gray03};
cursor: pointer;

// 후
${({ theme: { fontSize, color } }) => `
  width: 120px;
  height: 50px;
  padding: 8px 16px;
  font-size: ${fontSize.small};
  text-align: center;
  color: ${color.gray01};
  background-color: ${color.main};
  border: 1px solid ${color.gray03};
  cursor: pointer;
`}
```

<br>

[#110](https://github.com/woowacourse/react-shopping-cart/pull/110#discussion_r882682443)

```js
const response = await fetch(url, {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
  },
});
```

header 값은 다양한 형태의 값이 올 수 있기 때문에 인자로 받아 spread 형태로 적용하는 것이 좋을 것 같습니다. 🙂
( 자주 쓰이는 키의 경우 Authorization, 커스텀 등록 헤더 (x-...) 등이 있습니다~! 혹시 접하지 못해보셨다면 한번쯤 찾아 보시는 것도 좋을 것 같아요. 🙂 )

<br>

[#109](https://github.com/woowacourse/react-shopping-cart/pull/109#pullrequestreview-980954123)

- 리액트 testing-library에 대해서는 개인적으론 여전히 다소 부정적인 입장을 가지고 있습니다. 눈으로 확인하는게 훨씬 정확한 경우가 많다는 생각이에요. 그래서 소피아님 말씀대로 스토리북이 좀더 낫지 않나 싶은데, 전 한 발 더 나아가서 스토리북도 사실 큰 가치를 못느끼겠어요 ㅎㅎ 스토리북에서 발견될 오류는 작업중에도 얼마든지 발견할 수 있고, 작업중에 발견 못한 오류는 스토리북에서도 똑같이 발견 못하기 일쑤인것 같아서.. 이건 제 역량이 부족하기 때문일 가능성이 높으니 어디까지나 '저런 사람도 있구나' 하는 참고 정도로만 받아들이시기 바라요.

<br>

[#109](https://github.com/woowacourse/react-shopping-cart/pull/109#discussion_r878856276)

styled componets와 일반 components 구분

```jsx
import * as S from "./Logo.styled";

<S.LogoContainer>
  <S.IconImg src={shoppingCartIconWhite} alt="장바구니 아이콘" />
  <S.Title>TAEPHIA SHOP</S.Title>
</S.LogoContainer>;
```

<br>

[#109](https://github.com/woowacourse/react-shopping-cart/pull/109#discussion_r878856967)

> 전역상태관리 리덕스를 쓰는 많은 이유들 중에는 디버깅이 용이하다는 점도 있습니다.
> 위와 같이 어떤 조건에 따라 dispatch를 할지말지를 컴포넌트(hook)단에서 판단하면, 리덕스의 로그에는 남지 않게 되어 문제상황을 찾아내기가 조금 더 어려워지는 경향이 있는 것 같아요. 비지니스 로직에 대한 판단 중 많은 부분을 리덕스에 넘기면, 그만큼 역할 분리가 보다 명확해 질거에요.

디버깅이 용이하다는 리덕스의 장점을 써보려면, 중간에 적당한 액션을 dispatch 해야겠다고 생각해서,
PENDING -> post 요청 조건 확인 -> 조건 미달 시 CANCLE 액션 dispatch와 같은 흐름으로 작성

- action이 많아지는게 단점

<br>

[#109](https://github.com/woowacourse/react-shopping-cart/pull/109#discussion_r881139780)

optional chaining!!!

```jsx
const isAllSelected =
  baseList &&
  baseList.length !== 0 &&

// 후
const isAllSelected =
  baseList?.length !== 0 &&
  ...

```

<br>

[#109](https://github.com/woowacourse/react-shopping-cart/pull/109#discussion_r878865874)

```jsx
//전
const targetValue = Number(target.value);
if (targetValue % step !== 0) return;
if (targetValue > max) {
  setValue(max);
  return;
}
if (targetValue < min) {
  setValue(min);
  return;
}
setValue(targetValue);

// 후
if (Number.isInteger(targetValue)) return;

const newValue = Math.max(Math.min(targetValue, max), min);
setValue(newValue);
```

<br>

[#109](https://github.com/woowacourse/react-shopping-cart/pull/109#discussion_r881143935)

> ES6의 전체 기조가 function 키워드를 전혀 쓰지 않아도 되게끔 온갖 장치들을 마련했습니다. 그 이유는 function 키워드로 작성한 함수는 오남용될 가능성(constructor로 활용)이 있으며 이를 위해 prototype 프로퍼티를 들고 있는 등 메모리도 많이 차지하기 때문이죠. 그래서 각 목적에 맞게끔, 함수로서만 사용할 땐 arrow function을, 메소드로서만 사용할 땐 concised method 선언방식, 클래스로서 사용할 땐 class 등을 도입하였습니다.
> 그래서... 개발자들이 앞으로는 어떤 경우에도 function 키워드를 전혀 사용하지 않도록 유도하는 것이 tc39의 의도였다고 이해하고 있어요. 이렇게 받아들이는 개발자들은 저 말고도 많이 있답니다.
> 물론 반대의견도 있어요. function 이라고 하는 명시적인 표현을 할 수 있어 좋다거나, hoisting의 매력을 놓칠 수 없다는 등...
> 이런 가독성/개인취향의 문제도 있기 때문에 뭐가 정답이다! 라고 딱잘라 말씀드릴 수는 없지만, 그래도 기왕이면 arrow 함수로 통일하는것이 어떨까 하는 의견 드립니다

<br>

[#109](https://github.com/woowacourse/react-shopping-cart/pull/109#discussion_r879135644)

```jsx
grey_100: "#DDDDDD",
grey_200: "#CCCCCC",
grey_300: "#BBBBBB",
grey_400: "#AAAAAA",
grey_700: "#333333",
```

명칭이 애매합니다. 아까 저는 700이 bold이겠거니 하고 유추를 했었는데, 이제보니 black에 가까울수록 숫자가 커지도록 임의로 지정하신 것 같군요. 의도를 파악할 수 있는 네이밍을 고민해보시면 좋겠어요.
(primary_light의 경우는 어떤 의도인지 정확히 알 수 있어서 상대적으로 좋은 명칭입니다. 주된 색상으로부터 좀 더 밝은 색상임을 쉽게 유추할 수 있으니까요.)

<br>

[#129](https://github.com/woowacourse/react-shopping-cart/pull/129#discussion_r882964884)

- 최적화 아티클

<br>

[#129](https://github.com/woowacourse/react-shopping-cart/pull/129#discussion_r879442534)

```js
- 200 ok- 요청 성공

- 201 created- 요청 성공해서 새로운 리소스가 생성됨

- 204 no content - 서버가 요청을 성공적으로 수행했지만, 응답 payload 본문에 보낼 데이터가 없음

- 400 bad request - 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음

- 404 not found - 요청 리소스를 찾을 수 없음
```
