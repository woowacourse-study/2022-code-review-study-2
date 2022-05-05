### Level-1 lotto Step1(106, 71, 85, 98, 103, 104, 78) - 안, 돔하디, 록바, 무비, 꼬재, 블링, 소피아

- 분석 담당 코드

  - [#106](https://github.com/woowacourse/react-payments/pull/106) 안
  - [#71](https://github.com/woowacourse/react-payments/pull/71) 돔하디
  - [#85](https://github.com/woowacourse/react-payments/pull/85) 록바
  - [#98](https://github.com/woowacourse/react-payments/pull/98) 무비
  - [#103](https://github.com/woowacourse/react-payments/pull/103) 꼬재
  - [#104](https://github.com/woowacourse/react-payments/pull/104) 블링
  - [#78](https://github.com/woowacourse/react-payments/pull/78) 소피아

## 피드백 정리

[#106](https://github.com/woowacourse/react-payments/pull/106#discussion_r862413613)

> AddCardForm 컴포넌트가 위치한 디렉토리를 봤을 때 이 컴포넌트가 테스트가 있는지, 스토리북이 있는지를 한번에 파악하기도 어렵고 멀리 떨어져있다보니 연결성이 떨어지는 느낌이라 저희 팀은 test, stories 파일을 모두 대상 파일과 같은 디렉토리에 위치시키고 있어요!
> <br>

[#106](https://github.com/woowacourse/react-payments/pull/106#discussion_r862443530)

> React@17 부터 React 는 따로 import 하지 않아도 됩니다.
> <br>

[#106](https://github.com/woowacourse/react-payments/pull/106#discussion_r862443851)

validators를 객체로 넘겨줘서 처리한다.
<br>

[#85](https://github.com/woowacourse/react-payments/pull/85#discussion_r861400101)

> gitignore에 대해서 자세히 설명 (.pnp.js 는 무엇인가)
> <br>

[#85](https://github.com/woowacourse/react-payments/pull/85#discussion_r862428758)

> react-scripts 요 모듈은 devdependencies 로 들어가도 되는게 아닐까요?

react-scripts가 존재하는 이유는, "구버전 브라우저 호환 바벨 및 폴리필 코드 (라이브러리)등"이 react-scripts에 다수 들어가있기 때문입니다.

모던 브라우저 기준으로 작업하신다면 dev로 빼셔도 되고, IE등의 서포트가 필요하면 디펜던시로 올리면 되겠어요.
<br>

#85

> manifest.json은 무슨 역할을 하는걸까요?

manifest.json은 PWA 앱에서도 쓰이지만 기본적으로 브라우저에서 앱의 정보를 가지고 있기도 합니다!
그렇기 때문에 아이콘이나 제목 등을 매니페스트로 넣어두면 그 설정값으로 사용자가 볼 수 있게 한 번 래핑해둔거라 보셔도 될 것 같아요 :) (물론 구버전 브라우저는 호환 안됨)

[#85](https://github.com/woowacourse/react-payments/pull/85#discussion_r862430873)

> 그런데, 카드 레이아웃에서 보여지는 것은 4/4/4/4 이지만, 실제 인식에 처리되는 값은 6 - 9 - 1 이렇게 되기 때문에 괴리감이 많이 왔었는데요! 그래서, 컴포넌트로 만들어서 이러한 도메인을 격리시켰습니다.
> <br>
> 여기서 중요한 포인트는 4/4/4/4 에 얽매일 필요가 없다는 것입니다. 디스플레이 되는 값이 first, second 든 그것은 중요하지 않다는 것입니다. 결국 출력만 해주면되고, 서버에선 6-9-1로 되는 값만 이해할 수 있게 전달해주는게 주 포인트입니다.

- 컴포넌트 내에서 displaying value와 실제 input으로 전달되는 상태를 두 개로 쪼개서 관리했습니다.
- displaying value는 input으로 전달되는 값을 바인딩하며, value을 linear한 값을 2차원 배열로 displaying에서 관리합니다. [ [1,2,3,4], [1,2,3,4], [1,2,3,4], [1,2,3,4] ] 형태인 것이죠.
- 그래서, 실제 비즈니스에서 쓰이는 값은 value, 카드에 보이는 값은 displaying value 형태로 쪼개어 보여집니다.
- 각각의 input은 결국 하나의 state에서 관리되며, 해당 state로 하여금 displaying된 값을 각각의 input은 바라봅니다.
  <br>

[#98](https://github.com/woowacourse/react-payments/pull/98#discussion_r862403705)

> toggle만 한다면 reducer를 통해 간단하게 작성할 수 있다

```jsx
// before
const handleModal = useCallback(() => {
  setModalVisible((prevModalVisible) => !prevModalVisible);
}, []);

// after
const [modalVisible, handleModal] = useReducer((visible) => !visible, false);
```

<br>

[#104](https://github.com/woowacourse/react-payments/pull/104#issuecomment-1115772135)

> form 태그를 활용한 auto focus!

```jsx
const handleFocus = (form, currElement, direction) => {
  const formInputArray = [...form];
  const currentIndex = formInputArray.indexOf(currElement);

  formInputArray[currentIndex + direction]?.focus();

const handlePrevFocus = (e) => {
  const { key, target } = e;
  const { form, value } = target;

  if (key !== "Backspace") return;
  if (value !== "") return;

  handleFocus(form, target, -1);
};

const handleFormChange = (e) => {
  const { target } = e;
  const { form, maxLength, value } = target;

  if (value.length === maxLength) {
    handleFocus(form, target, 1);
  }
};

return (
  <StyledCardInfoForm
    autoComplete="off"
    onChange={handleFormChange}
    onKeyDown={handlePrevFocus}
  >
    {children}
  </StyledCardInfoForm>
);
```
