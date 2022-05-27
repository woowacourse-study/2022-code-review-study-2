# Leve2-2 React-Shopping-Cart Step2 - 앨버

## 다른 크루들 코드 분석

[앨버](https://github.com/woowacourse/react-shopping-cart/pull/115)
[자스민](https://github.com/woowacourse/react-shopping-cart/pull/106)
[빅터](https://github.com/woowacourse/react-shopping-cart/pull/94)
[우연](https://github.com/woowacourse/react-shopping-cart/pull/138)
[콤피](https://github.com/woowacourse/react-shopping-cart/pull/131)
[유세지](https://github.com/woowacourse/react-shopping-cart/pull/113)
[동키콩](https://github.com/woowacourse/react-shopping-cart/pull/136)
[꼬재](https://github.com/woowacourse/react-shopping-cart/pull/83)

## 리액트 렌더링 Q&A

#### Q. 꼭 렌더링 최적화를 해야 하나?

- A. 꼭 할 필요는 없습니다. 필요할때만 하면 됩니다~

<br>

#### Q. 렌더링 최적화는 어떻게 해야 하는거야?

- 먼저, profiler를 활용하여 렌더링이 비효율적으로 일어나는 곳을 파악합니다.
- 이후, 여러 기법과 코드 구조를 개편하여 렌더링 최적화를 해줍니다.

<br>

#### Q. 상태값이 변하면 리렌더링이 된다고 했는데 그 상태값이 useState의 값인지?

- state의 값이 변하면 리렌더링이 됩니다.
- useRef는 매번 렌더링을 할 때 동일한 ref 객체를 제공하고 리렌더링을 유발시키지 않습니다.

<br>

#### Q. useSelector로 가져온 store의 state의 값인지? store의 하나의 상태값이 변경되어도 그 외 다른 상태값을 사용하는 컴포넌트도 리 렌더링이 되는지

> The useSelector hook from react-redux doesn’t have this issue — components only re-render when their selected piece of state changes, even when other slices of the store are updated.

- useSelector의 경우에는 특정 state 값이 변하게 되면 이를 사용하고 있는 모든 컴포넌트에서 리렌더링이 발생한다고 합니다.

<br>

#### Q. 상태값이 변하면 리렌더링이 된다고 했는데 그 상태값이 무엇인지? 그 상태값이 누구의 상태값인지?

- 컴포넌트에서 리렌더링이 발생되는 이유는 아래와 같습니다.

  - 자기 자신이 setState를 호출했을때
  - 부모가 렌더링 되었을때
  - No any context value consumed by your component changed

## 피드백 정리

#### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)

<br>

- [[앨버](https://github.com/woowacourse/react-shopping-cart/pull/115#discussion_r878970600) - url에 종속적인 pagination 컴포넌트]

  > Pagination이 url의 page값에 종속되게 되어있네요. 현재는 상품리스트만 있지만 만약에 다른 페이지네이션이 필요한 화면이 생긴다면 수정이 필요해보이는 구조네요!

<br>

- [[콤피](https://github.com/woowacourse/react-shopping-cart/pull/131#discussion_r881312700) - 없어도 될 훅]

  ```javascript
  const { useDispatch, useSelector } = require('react-redux');

  function useReduxState(key) {
    const state = useSelector((reduxState) => reduxState[key]);
    return { dispatch: useDispatch(), state };
  }

  export default useReduxState;
  ```

<br>

- [[유세지](https://github.com/woowacourse/react-shopping-cart/pull/113#discussion_r882783163) - forEach 중간 return]

  > forEach를 사용할때 return을 이용해서 불필요한 순회를 중간에 종료해주려고 했는데,
  > 이러한 시도가 잘못된 접근인 줄 몰랐네요 😥😥

  <img src='https://user-images.githubusercontent.com/64825713/170607432-a62c1b1c-18cd-41aa-98c4-8a3b56d443e8.png'/>

<br>

- [[동키콩](https://github.com/woowacourse/react-shopping-cart/pull/136#pullrequestreview-982932136) - 선택과 집중]

  > 말씀드릴 내용이 참 많은것 같은데 저와 동키콩님의 몸은 하나뿐이고 시간이 한정적이라... 일단 제 생각에 좀더 시급해 보이는 것들 위주로 말씀드렸어요. 이 중에서 가능한 빨리 해결될 이슈들만 해결해 주시고 나머지는 '염두에만 둔 채 넘기'는 고급 스킬을 구사해주시면 좋을 것 같습니다! ㅎㅎ

<br>

- [[동키콩](https://github.com/woowacourse/react-shopping-cart/pull/136/files/a1459431f15893db636193e06dd3a52bd3789efb#r880326058) - closure를 활용한 hook 활용]

  ```javascript
  // hook - before
  function useCart() {
    //...생략

    const handleUpStockButton = () => {
      changeCartStock(cartId, cart.stock + 1);
    };
  }

  // 사용처 - before
  function Component() {
    const { handleUpStockButton } = useCart();

    const someFunction = () => handleUpStockButton({ cartId, cart });
  }
  ```

  ```javascript
  // hook - after
  function useCart({ cartId }) {
    //...생략

    const handleUpStockButton = () => {
      changeCartStock(cart.stock + 1);
    };
  }

  // 사용처 - after
  function Component() {
    const { handleUpStockButton } = useCart();

    const someFunction = () => handleUpStockButton(cart);
  }

  function AnotherComponent() {
    const { handleUpStockButton } = useCart();

    const someFunction = () => handleUpStockButton(cart);
  }
  ```

  - cartId 인자를 줄 필요가 없어졌다. 근데, 이렇게 하는게 어떤 장점과 단점이 있을까?

<br>

- [[동키콩](https://github.com/woowacourse/react-shopping-cart/pull/136#discussion_r880331209) - 저도 참 좋아하는데요❤]

  > S. 구분자 저도 참 좋아합니다. 반갑네요 ㅎㅎ

<br>

- [[동키콩](https://github.com/woowacourse/react-shopping-cart/pull/136#discussion_r880616036) - 관련있는 컴포넌트 디렉토리 그룹화]

  > 그러고보니 ProductList 하위에 Item이 없고 다른 디렉토리에 있군요..
  > 폴더구조를 통해 각 컴포넌트의 상관관계를 유추하기가 불가능한 구조이네요.
  > 관련된 스타일드컴포넌트도 위 각 폴더에 넣어준다거나, 혹은 스타일드컴포넌트만 별도로 모아본다거나 등등...
  > 그룹화를 시도해 보시면 좋겠어요.

  ```markdown
  components

  - product
    - list.tsx
    - item.tsx,
    - detail.tsx
    - itemSkeleton.tsx
  - cart
    - index.tsx
    - item.tsx
    - order.tsx
  - ...
  ```

<br>

- [[꼬재](https://github.com/woowacourse/react-shopping-cart/pull/132#pullrequestreview-982693617) - 컴포넌트 파일 구조 대한 고민]

  > 지금 구조는 deps를 좀 더 가져갔는데, 그렇게 해도 됩니다. 정답은 없습니다. 반대로 deps를 1-2로 제한할수도 있고요. 저도 폴더구조의 깊이를 어떻게 가져가야하는지 계속 고민이여서 이렇게도 해보고 저렇게도 해보는 상황입니다. 중요한것은 누군가가 왜 그렇게 구성하였는가 질문했을때 선택한 이유와 느꼈던 장단점을 답변할 수 있어야 합니다.

<br>

- [[꼬재](https://github.com/woowacourse/react-shopping-cart/pull/132#discussion_r883232813) - on과 props의 의미]

  > - 보통 이벤트에 관련 로직 메소드를 작성하는 부분에는 handle prefix를 붙이고, component의 props는 외부에서 사용하기에 on을 붙이는 편이에요

  > - props는 인터페이스 역할을 합니다. 사용하는측에게 handlePutInShoppingCart라는 구체적인 행위(저수준)를 요구하고 있는데 만약 shoppingcart를 업데이트하는것이 아닌 다른 로직을 수행한다면 이름과 행위가 일치하지 않을듯합니다. ProductDetails는 사용하는 측에서 로직을 정해서 주입하도록 열어놓기만 하면되죠. 그럼 이름을 handlePutInShoppingCart 같이 구체적인 로직을 암시하는 이름보다 onClick이나 onCartClick 같은 'on + 타겟 + 이벤트' 이름으로 props를 열어놓으면 좋을것 같습니다:)

<br>

- [[꼬재](https://github.com/woowacourse/react-shopping-cart/pull/132) - await]

  > axios 리턴타입이 promise이니 async가 없어도 충분할듯 하네요
