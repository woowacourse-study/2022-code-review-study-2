# Level2 장바구니 미션 Step2 - 코카콜라

- [#128, 코카콜라](https://github.com/woowacourse/react-shopping-cart/pull/128)
- [#135, 안](https://github.com/woowacourse/react-shopping-cart/pull/135)
- [#125, 해리](https://github.com/woowacourse/react-shopping-cart/pull/125)
- [#139, 무비](https://github.com/woowacourse/react-shopping-cart/pull/139)
- [#140, 위니](https://github.com/woowacourse/react-shopping-cart/pull/140)
- [#133, 아놀드](https://github.com/woowacourse/react-shopping-cart/pull/133)
- [#121, 결](https://github.com/woowacourse/react-shopping-cart/pull/121)

---

## 피드백 정리

### prettier 일괄적용

- [#128, 코카콜라](https://github.com/woowacourse/react-shopping-cart/pull/128)

```javascript
{
    ...
    "scripts": {

        "prettier": "npx prettier --write '**/*.{jsx,js,css,html}'"
    }
    ...
}
```

```javascript
// 터미널 입력
npx prettier -w "**/*.js"
npx prettier -w "**/*.jsx"
```

prettier가 일회성으로 설치되면서 지정한 확장자에 대해 포맷팅을 일괄적으로 실행해준다.

---

### Redux Toolkit

- [#133, 아놀드, immer](https://github.com/woowacourse/react-shopping-cart/pull/133)

```javascript
...
    state.loading = false;
    state.error = false;
    state.data = action.payload;
    ...
```

> state.loading, state.error... 이렇게 직접 접근해서 프로퍼티값을 바꿔주는것은 mutable 조작입니다 toolkit에서 이렇게 조작이 가능하게 된 이유는 무엇일까요?

immer가 mutable하게 조작하지 않아도 내부적으로 바뀐 부분만 새로운 오브젝트로 갈아끼워주기 때문에 편하게 조작할 수 있었습니다!

**immer.js 란?**

- react에서 불변성을 유지하는 코드를 작성하기 쉽게 해주는 라이브러리입니다.

```javascript
// immer 쓴 reduce 코드
const initialState = [{ name: "nkh", address: { city: "seoul" } }];

export default function auth(state = initialState, action) {
  produce(state, (draft) => {
    switch (action.type) {
      case SET_INFO:
        draft[0].name = action.data.name;
        draft[0].address.city = action.data.city;
        break;
      case ADD_INFO:
        draft.push({ name: "hhh", address: { city: "zzz" } });
      default:
        return draft;
    }
  });
}
```

[immer.js예시](https://kyounghwan01.github.io/blog/React/immer-js/#redux%E1%84%8B%E1%85%A6%E1%84%89%E1%85%A5-immer-%E1%84%8A%E1%85%B3%E1%84%80%E1%85%B5)
[immer docs](https://redux-toolkit.js.org/usage/immer-reducers)

---

### html tag

- [#133, 아놀드](https://github.com/woowacourse/react-shopping-cart/pull/133)

```javascript
// src/pages/ProductPage/index.jsx
   dispatch(getCart(productId));
  }, [dispatch, productId]);

  if (productLoading || cartLoading) return '로딩';
```

> body div가 있어서 문자열 return이 가능한거 같긴하지만 조금 더 안전하게 태그로 감싸서 return 하면 좋을듯 같네요:)

---

### Redux

- [#133, 아놀드, 상태관리](https://github.com/woowacourse/react-shopping-cart/pull/133)

리뷰어:

> 모든 remote 데이터를 redux 상태로 관리하게 되는건가요?? 정하기 나름이긴하겠지만 모든 remote 데이터를 reducer 그리고 redux로 관리하는게 맞는지 redux를 어떤 역할로 사용할것인지 고민해봐도 좋을것 같습니다

아놀드:

> 페이지 컴포넌트에서만 로컬 스테이트로 가져도 되긴 합니다!
> 하지만 리덕스 썬크랑 연동하여 사용하기 때문에 리덕스에 관리시켰습니다!
> 그리고 리덕스의 원칙중 한 가지가 '모든 근원은 하나다' 이기 때문에 원칙을 지키려 했습니다.

**Q.상태는 어디서 관리 해야 할까? redux 상태? 컴포넌트에서 local state???**
