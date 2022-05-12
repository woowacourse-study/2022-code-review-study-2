# Level2 페이먼츠 미션 Step1 - 코카콜라

- [#75, 코카콜라](https://github.com/woowacourse/react-payments/pull/75)
- [#92, 태태](https://github.com/woowacourse/react-payments/pull/92)
- [#80, 콤피](https://github.com/woowacourse/react-payments/pull/80)
- [#83, 티거](https://github.com/woowacourse/react-payments/pull/83)
- [#91, 호프](https://github.com/woowacourse/react-payments/pull/91)
- [#102, 샐리](https://github.com/woowacourse/react-payments/pull/102)
- [#72, 민초](https://github.com/woowacourse/react-payments/pull/72)
- [#76, 위니](https://github.com/woowacourse/react-payments/pull/76)

---

## 피드백 정리

### Hooks

- [#75, 코카콜라, useEffect 남용](https://github.com/woowacourse/react-payments/pull/75)

> 리뷰어: useEffect는 사이드 이펙트를 관리하기위해서 사용하는데요. 현재 전체적인 컴포넌트에서 useEffet를 과하게 사용하는 느낌이 있습니다. 최소한으로 useEffect를 사용하는 방법으로 리펙토링해 보시는건 어떨까요?

['useEffect를 남용하지 말자'](https://gusrb3164.github.io/web/2021/12/29/less-use-useeffect/)

> **side effect 종류**

- 데이터 가져오기
- 구독(subscription) 설정하기
- 수동으로 React 컴포넌트의 DOM을 수정하기
- ...

useEffect Hook은 = componentDidMount + componentDidUpdate + componentWillUnmount

- componentDidMount
  - 컴포넌트가 마운트된 직후, 즉 트리에 삽입된 직후에 호출된다.
- componentDidUpdate
  - 갱신이 일어난 직후에 호출된다.
- componentWillUnmount
  - 컴포넌트가 마우트 해제되어 제거되기 직전에 호출된다.

> **useEffect 부작용**

1. useEffect 여러개의 연쇄 작용, 무한 루프 리렌더링

```javascript
// useEffect 여러개 일 경우 다른 useEffect에 영향을 끼치는 것을 고려해야 한다.
// useEffect간의 연쇄 작용으로 무한루프 리렌더링을 유발 시키는 예시.

import React, { useState, useEffect } from "react";

const App = () => {
  const [foo, setFoo] = useState(0);
  const [bar, setBar] = useState(0);

  useEffect(() => {
    setBar((prev) => prev + 1); // 해당 비동기 로직이 실행되면 아래의 useEffect가 실행된다
  }, [foo]);

  useEffect(() => {
    setFoo((prev) => prev + 1); // 해당 비동기 로직이 실행되면 위의 useEffect가 실행된다
  }, [bar]);

  // return ...
};
```

2. 흐름 추적의 어려움

sideEffect로 useEffect가 실행되는 것은 useEffect의 deps을 따로 확인해야 함으로 거대해진 코드에서는 기능을 파악하기 힘들다.

---

### 컨벤션

- [#91, 호프, styled-component와 React의 컴포넌트를 구분 하기](https://github.com/woowacourse/react-payments/pull/91)

```javascript
// refactor

import * as styled from "./index.styled";
const SomeComponent = () => {
  return <styled.Container>....</styled.Container>;
};
```

---

### 스토리북

- [#91, 호프, 스토리북 Controls](https://github.com/woowacourse/react-payments/pull/91)

> 다른 storybook 관련 파일들도 마찬가지지만 **옵션값에 따른 UI 변경을 위해 꼭 필요한 영역만 Controls 영역에 노출되도록** 개선해 보시면 좋을 것 같습니다
> 지금은 스토리북 Controls에 변경해도 적용되지 않는 영역, 변경하면 안되는 영역 등 불필요한 영역의 값도 입력할 수 있고 일부값은 변경시에 에러가 발생하고 있어서 UI를 확인하는데 오히려 혼란을 주고 있는 것 같습니다
> **Controls에 꼭 필요한 영역만 표시되도록 개선해 보시면 좋을 것 같습니다**

---

### 렌더링

- [#91, 호프](https://github.com/woowacourse/react-payments/pull/91)

> **불필요한 Input onChange 렌더링을 막을 필요성**
> 실제로 Input값을 매번 State로 관리해야 되는지, 아니면 Ref로 해당 입력값을 직접 참조하는 방식이 나을지는 요구사항마다 다를 것 같은데요. 지금 요구사항은 입력된 값들 모두를 확인해야 되는 상황이고 실시간으로 입력값 검증을 하는 상황이라 State로 관리하는 방식이 조금 더 적합하다는 생각이 드네요. 그리고 State를 끌어올려서 하나의 컴포넌트에서 관리되는 방식인데 그러다보니 불필요한 props drilling이 발생하는 영역이 일부 보이네요. 이 부분은 Context API의 도입을 고민해 보시면 좋을 것 같습니다. (props drilling이 심한건 아니라서 선택적으로 적용해 보시면 될 것 같습니다). 참고로 모든 Input 컴포넌트가 다시 리렌더링 되는 부분은 리액트의 랜더링 최적화에 따라 render가 매번 호출된다고 해서 실제로 모든 화면을 다 다시 그리는건 아니기도 하고 현재 구현된 대상영역도 그리 많지는 않은 상황이라 아직은 고민하지 않으셔도 될 것 같습니다

- Input값을 매번 State로 관리해야 하나? vs Ref로 해당 입력값을 직접 참조 해야하나?
- 두 가지 방식 중 정답은 없다. 다만 요구사항에 따라 유연하게 구현하면 된다.
- 미션의 상황은 입력된 값들 모두 실시간으로 확인을 해야 하는 상황이라서 State로 관리 하는 방식이 적합하다.
- 또한 State를 끌어올려서 하나의 컴포넌트에서 관리를 하다 보니 **불필요한 props drilling이 발생** 하게 되는데, 해당 문제를 해결하기 위해 **Context API**를 도입해 보자.

---

### 상태 분리

- [#91, 호프](https://github.com/woowacourse/react-payments/pull/91)

> **상태 분리 관련**
> 입력값을 개별적인 state로 관리하는 현재 구조에서 object로 분리하는 작업을 수행하게 되면 물론 전달이나 참조가 편해지는 장점도 있지만 변경에 대해 확인하는 방식도 변경되야되서 이 부분은 조금 더 고민해 보시는게 필요할 것 같은데요. 개인적으로는 변경으로 인한 장점이 크지는 않을 것 같습니다.

---

### UI 단위로 컴포넌트 분리

- [#91, 호프](https://github.com/woowacourse/react-payments/pull/91)

> **UI 단위로 컴포넌트를 나누는게 맞을지?**
> 개인적으로는 Styled-component는 리액트 컴포넌트 단위의 style을 정의하기 위한 영역이고 그 2개가 조합된 리액트의 컴포넌트 전체를 다시 사용하는 경우가 적합하다고 보는데요. 이렇게 되려면 정말 작은 단위로 컴포넌트가 쪼개져야 가능하기도 합니다. 실제 구현하다보면 그렇게 하기 어려운 경우도 많고요. 다소 답변이 모호할 수 있는데 코드레벨에도 질문주실 때 고민하신 지점을 짚어주시면 조금 더 구체적인 말씀을 드릴 수 있을 것 같아요 :)

---

### 메서드

- [#102, 샐리, padStart()](https://github.com/woowacourse/react-payments/pull/102)

> String.prototype.padStart()
> str.padStart(targetLength [, padString])

padStart() 메서드는 현재 문자열의 시작을 다른 문자열로 채워, 주어진 길이를 만족하는 새로운 문자열을 반환합니다. 채워넣기는 대상 문자열의 시작(좌측)부터 적용됩니다.

```javascript
const str1 = "5";

console.log(str1.padStart(2, "0"));
// expected output: "05"

const fullNumber = "2034399002125581";
const last4Digits = fullNumber.slice(-4);
const maskedNumber = last4Digits.padStart(fullNumber.length, "*");

console.log(maskedNumber);
// expected output: "************5581"
```
