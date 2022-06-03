# Level2 장바구니 Step2 - 병민

코드 리뷰 리스트
- [병민](https://github.com/woowacourse/react-shopping-cart/pull/143), [민초](https://github.com/woowacourse/react-shopping-cart/pull/134)
- [티거](https://github.com/woowacourse/react-shopping-cart/pull/123), [밧드](https://github.com/woowacourse/react-shopping-cart/pull/120)
- [돔하디](https://github.com/woowacourse/react-shopping-cart/pull/142), [후이](https://github.com/woowacourse/react-shopping-cart/pull/124)
- [블링](https://github.com/woowacourse/react-shopping-cart/pull/104), [준찌](https://github.com/woowacourse/react-shopping-cart/pull/127)

## 병민

### [동일성 확인](https://github.com/woowacourse/react-shopping-cart/pull/143#discussion_r882195379)

```
동일성을 확인하는 로직들이 자주 보이는데요 이런 동일성을 확인해야 되는 경우가 자주 발생한다면  
어플리케이션의 규모가 커질수록 성능상 이슈가 발생할 가능성도 높아지고 안정성도 떨어질 것 같아요  
어쩔 수 없이 �동일성을 확인해야 되는 경우가 아니라면 이런 방식은 최소화하는 방향으로 개선해보면 좋을 것 같아요  
```

#### 나의생각
동일성을 확인하는것이 정말 성능에 안좋을까?  
물론 useSelector로 받는 값의 depth가 얕으면 얕을수록 좋지만,  
어쩔 수 없이 객체를 받아야 하는 경우에는 동일성을 확인하는 함수를 써서 re-render를 줄이는게 좋다고 생각합니다.  
전문 : https://github.com/woowacourse/react-shopping-cart/pull/143#discussion_r884129868

### [Checked 속성](https://github.com/woowacourse/react-shopping-cart/pull/143#discussion_r884138012)

[Checkbox 오류 해결하기 - 블로그](https://develoger.kr/frontend/react-checkbox/)
[Checkbox 오류 해결하기 - md문서](./bm-link-1.md)

### [structuredClone](https://github.com/woowacourse/react-shopping-cart/pull/143#discussion_r886304621)

deepclone을 해주는 함수가 브라우저에도 있습니다!  
[structuredClone](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)

주의사항
- set, map은 복사되지 않습니다
- function은 오류가 나옵니다

### [Compound Component](https://github.com/woowacourse/react-shopping-cart/pull/143#discussion_r886307191)
```
<Modal>
  <Modal.Head>
  </Modal.Head>
  <Modal.Body>
  </Modal.Body>
</Modal>
```
이런식으로 Grouping해서 사용할 수 있습니다!


## [티거](https://github.com/woowacourse/react-shopping-cart/pull/123)

### [절대경로](https://github.com/woowacourse/react-shopping-cart/pull/123#issuecomment-1136141937)

```
일관성을 유지하기 위해 모든 경로에는 절대 경로를 사용하였습니다  
같은 폴더 안에, 혹은 가까이에? 위치한다면 상대 경로를 사용하는 게 더 낫겠다는 생각도 듭니다  
율리는 보통 어떻게 하시나요~?
```

```
같은 폴더 안에 있다면 상대 경로로 사용해도 무방하다고 생각합니다.
```

### [리듀서 다이어트](https://github.com/woowacourse/react-shopping-cart/pull/123#discussion_r880614793)

리듀서 case안에서 다 처리하는게 아니라 함수로 뺐다!  
[개선된 코드 확인하기](https://github.com/daaaayeah/react-shopping-cart/blob/step2/src/redux/cart/cartReducer.js)

## 밧드

### [dispatch in loop](https://github.com/woowacourse/react-shopping-cart/pull/120#discussion_r880469849)

dispatch를 loop안에서 해도 될까...?  
```
이런 구조는 다소 위험해 보이는데요 여러 개의 데이터를 삭제할 때  
이런 순차적인 구조로 삭제하면 중간에 오류가 발생한 경우 일부는 삭제되고  
일부는 삭제되지 않는 상황이 발생할 수 있는 구조네요
```

중간에 오류..?

잘 모르겠다. re-render가 너무 많이 발생해서 그런건가?

### [범용적인 Pagination Component](https://github.com/woowacourse/react-shopping-cart/pull/120#discussion_r880543481)


## 돔하디

### [redux store VS 컴포넌트 내 상태관리](https://github.com/woowacourse/react-shopping-cart/pull/142#issuecomment-1136034424)

"다만, 모든 상태를 스토어에서 관리해야하냐?는 절대 아니라고 생각합니다."

개인적인 생각 : re-render가 너무 자주 일어나는 부분이 아니라면, 가급적 store에 관리하는게 유지보수에 좋을것 같다!

## 후이

### [${userId}/${id}](https://github.com/woowacourse/react-shopping-cart/pull/124#discussion_r879264042)

"유저 정보는 보통 url 에 나타내지 않습니다!"

### [전역상태 vs local 상태](https://github.com/woowacourse/react-shopping-cart/pull/124#issuecomment-1140374365)

"redux 를 사용한다고 해서 모든 정보를 전역으로 관리할 필요는 없습니다!  
전반적인 컴포넌트에서 모두 알아야할 정보 (유저정보 라던지?) 들만을 전역에 두고,  
컴포넌트에서 state 로 충분히 활용 가능한 정보들은 각자의 컴포넌트들이 가지고 있으면 됩니다.  
이 때문에 custom hook 으로 api 레이어를 관리하는게 중요할 것 같네요!  
그 친구가 일을 수행한 후에 컴포넌트로 응답을 반환해주던지,  
redux 에 저장하는 일까지 맡을 것인지 요런 것들을 고민해보면 되지 않을까 싶습니다~"

## 블링

### [axios intercept](https://github.com/woowacourse/react-shopping-cart/pull/104#discussion_r878655926)

https://velog.io/@subanggu/axios-interceptor-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0

매 request마다 알아서 호출된다!
```
instance.interceptors.request.use(
  function (config) {
    config.headers["Content-Type"] = "application/json; charset=utf-8";
    config.headers["Authorization"] = " 토큰 값";
    return config;
  },
  function (error) {
    console.log(error);
    return Promise.reject(error);
  }
);
```

### [불필요한 Memoization](https://github.com/woowacourse/react-shopping-cart/pull/104#discussion_r878813590)

### [Image onError](https://github.com/woowacourse/react-shopping-cart/pull/104#discussion_r883132211)

[MDN 문서](https://developer.mozilla.org/ko/docs/Web/HTML/Element/img#%EC%9D%B4%EB%AF%B8%EC%A7%80%EB%A5%BC_%EA%B0%80%EC%A0%B8%EC%98%AC_%EC%88%98_%EC%97%86%EC%9D%84_%EB%95%8C)

## 준찌

### [fetch prefix](https://github.com/woowacourse/react-shopping-cart/pull/127#discussion_r884146723)

