### Level-1 lotto Step1(145, 137, 109, 122, 126, 115, 116) - 안, 돔하디, 록바, 무비, 꼬재, 블링, 소피아

- 분석 담당 코드

  - [#145](https://github.com/woowacourse/react-payments/pull/145) 안
  - [#137](https://github.com/woowacourse/react-payments/pull/137) 돔하디
  - [#109](https://github.com/woowacourse/react-payments/pull/109) 록바
  - [#122](https://github.com/woowacourse/react-payments/pull/122) 무비
  - [#126](https://github.com/woowacourse/react-payments/pull/126) 꼬재
  - [#115](https://github.com/woowacourse/react-payments/pull/115) 블링
  - [#116](https://github.com/woowacourse/react-payments/pull/116) 소피아

## context api vs redux

### 특징

#### context api

- React에서만 사용할 수 있습니다. (리액트 내장 기능)
- Entry 파일(root)에서 구성한 Provider를 내려 주는 형식입니다.
- 사용하고자 하는 컴포넌트에서 작성한 Dispatch와 State를 꺼내서 사용합니다.
- reducer를 여러 개 만들면 Provider에서 여러 단계로 만들어 사용할 수 있습니다.

#### redux

- React, Vue와 같은 프레임워크 환경에서 사용할 수 있습니다.
- 상태를 저장하는 Store를 따로 가지고 있습니다.
- thunk, saga와 같은 미들웨어를 추가적으로 사용하여 구성할 수 있습니다.
- Redux devtool extension을 사용하면 상태에 대한 디버깅이 가능합니다.
- 전역 상태 관리 외에도 로컬스토리지 상태저장, 버그리포트 첨부 기능 등의 기능들을 사용할 수 있습니다.

### 차이점

- Context API는 React를 사용할 때 추가 dependency 없이 사용할 수 있어서 가볍게 사용할 수 있다. 하지만 상태를 넘겨줄 때 상태가 여러 개라면 **Provider를 중첩**해서 내려 줘야 하기 때문에 그런 불편하다.

- Redux는 saga, thunk와 같은 미들웨어를 추가적으로 사용할 수 있어 비동기 처리를 따로 Util로 처리할 수 있다. 추가 설정을 통해 디버깅을 가시적으로 할 수도 있어 편하다. 하지만 미들웨어를 사용하기 위해 관련 개념을 이해해야 하기 때문에 어려운 점이 있다.

![image](https://velog.velcdn.com/images%2Fcada%2Fpost%2F2fe54f52-a384-444a-88ad-05fd2d10028c%2Fdas.PNG)

### 정리

- 오직 전역 상태 관리를 위한다면 Context API를 사용하라.
- 상태 관리 외에 여러 기능이 필요하다면 Redux 를 사용하라.
- high-frequency한 어플리케이션의 경우 Context API를 사용하면 성능상 이슈가 있을 수 있다.

## 피드백 정리

[#109]

```jsx
// case 1 관련된 (상태,함수) 같이
const [count, setCount] = useState(0);

const [hello, setHello] = useState("hello");
const handleHello = () => {
  setHello("hello hello");
};

const [bye, setBye] = useState("bye");
const handleBye = () => {
  setBye("bye bye");
};

// case 2 상태는 상태대로 함수는 함수대로
const [count, setCount] = useState(0);
const [hello, setHello] = useState("hello");
const [bye, setBye] = useState("bye");

const handleHello = () => {
  setHello("hello hello");
};

const handleBye = () => {
  setBye("bye bye");
};
```

> hook 관련해서 저도 case 2 형태로 다루고 있습니다 :) 그런데, 애초에 컴포넌트를 잘 만들면 케이스 1과 같은 상황이 발생하지 않습니다.. (이상적이긴 해도.. 저렇게 컨디션 별로 생기는게 사실 많이 없어야합니다.)
> <br>

[#122](https://github.com/woowacourse/react-payments/pull/122#discussion_r867475607)

> 초기값에 복잡한 연산이 들어갈때 Lazy initialization을 할 수 있는데요~
> 이 방법을 안쓰면 리렌더링이 일어날때마다(form의 Input 데이터를 변경할때마다) uuid를 새로 생성하고 initialCardInfo를 spread하는 연산이 추가적으로 발생해요
> <br>

[#115](https://github.com/woowacourse/react-payments/pull/115/files/1c9f388fbc53e50b854398a1742962c83063e671#r868937873)

귀찮더라도 이런건 callback함수를 별도로 작성해두시는 편이 좋아요.

- 매 렌더시마다 새로운 함수가 생성되지 않게 할 수 있습니다.
- 함수만 전달하더라도 자동으로 이벤트가 인자로 전달됩니다.

```jsx
const setNickname = useCallback(
  e => { setNicknameLength(e.target.value.length) },
  []
)
...
return (
  ...
  onChange={setNickname}
}
```

<br>

[#116](https://github.com/woowacourse/react-payments/pull/116#discussion_r867500171)

> useInput, useInputArray을 사용해서, 필드별로 어떤 초기값을 받아서 어떤 상태와 메소드를 반환할지가 일관적이다보니 생각보다 가독성이 좋고 맥락이 굉장히 잘보이더라고요~ 커스텀훅을 너무 잘 만들어서 사용하신것 같아요.
