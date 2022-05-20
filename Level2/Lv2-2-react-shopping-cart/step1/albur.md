# Leve2-2 React-Shopping-Cart Step1 - 앨버

## 다른 크루들 코드 분석

[앨버](https://github.com/woowacourse/react-shopping-cart/pull/91)
[자스민](https://github.com/woowacourse/react-shopping-cart/pull/90)
[빅터](https://github.com/woowacourse/react-shopping-cart/pull/94)
[우연](https://github.com/woowacourse/react-shopping-cart/pull/93)
[콤피](https://github.com/woowacourse/react-shopping-cart/pull/87)
[유세지](https://github.com/woowacourse/react-shopping-cart/pull/92)
[동키콩](https://github.com/woowacourse/react-shopping-cart/pull/82)
[꼬재](https://github.com/woowacourse/react-shopping-cart/pull/83)

## 피드백 정리

#### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)

<br>

- [[자스민](https://github.com/woowacourse/react-shopping-cart/pull/90#pullrequestreview-970699758) - 컴포넌트 분리기준]

  > 컴포넌트가 정말 작게 분리되어있군요! 잘게 분리해보니 어땠나요? 먼저, 컴포넌트의 분리 기준이 궁금했어요.
  > 어떤건 스타일만 가진 컴포넌트가 있고, 사용하는 쪽에서 로직을 주입하기도 하고 어떤건 컴포넌트 내에서 로직을 갖고 있는 녀석도 있었어요! 사실 코드를 읽을 때 컴포넌트 마다 다 다르게 표현된 것 같아서 파악하는 데 좀 어려움이 있었습니다! (물론 양이 많아서 그럴 수도..!) 그래서 컴포넌트의 관리 전략을 공유해주시면 코드를 이해하는 데 훨씬 도움이 될 것 같아요 :)

<br>

- [[자스민](https://github.com/woowacourse/react-shopping-cart/pull/90#discussion_r872939307) - styled-component를 이용해서 type 지정해주기]

  ```javascript
  const CheckBox = styled.input.attrs({ type: "checkbox" })`
  ```

<br>

- [[자스민](https://github.com/woowacourse/react-shopping-cart/pull/90#discussion_r872949730) - 정답이 없는 스토리북]

  > 어떤 부분을 의도하고 만드셨는 지 궁금했어요.ㅎㅎ 어디까지 스토리북화할 것인지는 케바케죠..! 다만, 우리가 이전에 열심히 작성했던 테스트코드 처럼 스토리북도 코드이기 때문에 유지보수의 대상이라 어디까지 스토리북을 작성할 지는 고민해보면 좋을 것 같아요 :)
  > 스토리북은 보통 개발자 혼자서 결정하진 않고 디자인과 협의해서 컴포넌트 별로 정의하기 때문에 정답은 없는 것 같습니다!

<br>

- [[우연](https://github.com/woowacourse/react-shopping-cart/pull/93#discussion_r873716546) - 일관성있는 color pallette 값 + 투명도 줄 수 있는 함수]

  > 컬러 지정하는 방식을 통일하면 어떨까요?
  > 나중에 관리하기 힘들어질 것 같아요.
  > 숫자를 지정하는 방식도 아래 palette처럼 낮은 숫자일 때 색상이 연하면 좋을 것 같습니다 🙁

  ```javascript
  export function withOpacityValue(hexCode, opacity) {
    const red = hexCode.substring(1, 3);
    const green = hexCode.substring(3, 5);
    const blue = hexCode.substring(5);

    return `rgba(${red}, ${green}, ${blue}, ${opacity})`;


  }

  // 사용처

  box-shadow: 0 4px 4px ${({ theme }) => withOpacityValue(theme.colors['BLACK_002'], 0.3)};
  ```

<br>

- [[우연](https://github.com/woowacourse/react-shopping-cart/pull/93#discussion_r872942113) - 마크업을 신경써서 작성하자]

  > styled-component를 사용하더라도 마크업 태그가 시멘틱하게 작성했는지 점검해보면 좋을거같아요.

  ```javascript
  <Button as='a'>Click Me</Button>
  ```

  - 위처럼 as를 사용하면 태그를 변화시킬 수 있다!

<br>

- [[우연](https://github.com/woowacourse/react-shopping-cart/pull/93#discussion_r872942447) - 안전한 데이터 타입 체크]

  > 혹시나 서버에서 특정한 문제가 생겨서 data타입이 array타입으로 들어오지 않으면 어떻게 될까요?..(그러면 안되겠지만요.. 😓 )

  - 타입스크립트를 사용해야 하는 걸까?...

<br>

- [[유세지](https://github.com/woowacourse/react-shopping-cart/pull/92#discussion_r873051742) - env 사용]

  > 드디어 env를 올려주신 크루님이!.... 😭
  > 감사해요...

  - 감사해요라고 말씀하신 이유가 무엇일까요?
  - 이게 엄청 중요한 것 같아서 가져왔습니다.

<br>

- [[유세지](https://github.com/woowacourse/react-shopping-cart/pull/92#discussion_r873054731) - reset css 라이브러리]

  - reset css를 해주는 라이브러리가 있다?
  - https://github.com/zacanger/styled-reset

  ```javascript
  import * as React from 'react';
  import { createGlobalStyle } from 'styled-components';
  import reset from 'styled-reset';

  const GlobalStyle = createGlobalStyle` ${reset} /* other styles */`;

  const App = () => {
    <React.Fragment>
      <GlobalStyle />

      <div>Hi, I'm an app!</div>
    </React.Fragment>;
  };

  export default App;
  ```

  <br>

- [[유세지](https://github.com/woowacourse/react-shopping-cart/pull/92#discussion_r873059944) - container vs wrapper]

  > Wrapper도 있고 Container도 있던데 차이가 있을까요? 🤔

  - Wrapper의 경우 단일 요소를 감쌀때 사용하고, Container의 경우 다중 요소를 감싸줄때 사용한다고 해요! (https://stackoverflow.com/questions/4059163/css-language-speak-container-vs-wrapper)

<br>

- [[유세지](https://github.com/woowacourse/react-shopping-cart/pull/92#discussion_r873643126) - 넉넉한 color pallete]

  ```javascript

  GRAY_005: '#555555',
  GRAY_004: '#AAAAAA',
  GRAY_003: '#DDDDDD',
  GRAY_001: '#F6F6F6',
  GRAY_002: '#F3F3F3',

  ```

  > 001부터 쌓아올라가는 palette!...
  > 사실 이러면 중간범위에 새로운 색상을 넣어주기가 힘들어서 간격을 처음 드린 링크처럼 50~ 100단위로 넣으면 좋아요

<br>

- [[동키콩](https://github.com/woowacourse/react-shopping-cart/pull/82)- 마음껏 상상하라]

  > 그러니 당장은 어렵겠지만 이 상태에서 인증이 추가된다면? 페이지도 스토어로 관리한다면? 새로고침할때 데이터를 유지해야한다면? 등등 다양한 상상을 마음껏해보세요!
  > 그것이 코드로 녹아져있지 않아도 괜찮습니다.
  > 다만 마음껏 상상하고 고민하고 문제에 직면하는 것과 아무 생각없이 구현하고 일이 닥쳐오는 것은 결과적으로 다를 수 있거든요
