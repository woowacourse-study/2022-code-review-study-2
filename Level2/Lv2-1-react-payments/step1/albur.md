# Leve2-1 React-payments Step1 - 앨버

- 분석 담당 코드

  - [#73](https://github.com/woowacourse/react-payments/pull/73)
  - [#74](https://github.com/woowacourse/react-payments/pull/74)

  - [#97](https://github.com/woowacourse/react-payments/pull/97)
  - [#100](https://github.com/woowacourse/react-payments/pull/100)

  - [#88](https://github.com/woowacourse/react-payments/pull/88)
  - [#90](https://github.com/woowacourse/react-payments/pull/90)

## 다른 크루들 코드 분석

#### 상태 관리를 어디서 해주는지?

- [앨버, 하리] App 컴포넌트에서 모든 state 관리
- [밧드, 빅터] App -> CardAddPage 컴포넌트에서 모든 state 관리
- [코이, 도리] App -> AddPage 컴포넌트에서 모든 state 관리

- 대체적으로, 최상단 컴포넌트에서 모든 상태를 관리를 해주고 props로 state와 setState를 내려주는 방식으로 상태를 업데이트 해준다.
- 상태를 업데이트 하는 방식에서 차이가 있는데,

  1. 최상단에서 선언한 setState를 그대로 자식에게 전달해서 그대로 사용
  2. 최상단에서 setState를 가지고 함수를 따로 만들어서 자식에게 전달해서 사용

  - setState 자체를 자식에게 전달해서 사용해주는 것은 안티패턴이라고 들어서 이 부분에 대해서 이야기를 해봐도 좋을 것 같다.

#### 커스텀 훅을 어떻게 사용해주는지?

- 커스텀 훅을 사용한 팀도 있고 사용하지 않은 팀도 있었다.
- 커스텀 훅을 아래와 같은 용도로 사용해주고 있었다.
  함수 컴포넌트내에 있는 비즈니스 로직을 분리하기 위해 (재사용성 거의 없음)

#### label htmlfor와 input의 id를 연결해주었는지?

- 아무도 해주지 않고 있었다..
- 바닐라 js에서는 대부분이 해주고 있었는데, 리액트에서는 해주고 있지 않은 부분이 있는 것 같다. 신경써주자!

## 기타

- 컴포넌트가 어떻게 설계되었는 지 코드를 살펴보려고 코드를 계속 보았는데, styled-component를 선언하는 부분을 `style 파일`로 분리한 것은 살짝 보기 힘들었다..

## 피드백 정리

#### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)

<br>

- [[#73](https://github.com/woowacourse/react-payments/pull/73#discussion_r862471299) - styled-component와 로직이 담겨있는 컴포넌트와의 네이밍 컨벤션]

  ```javascript
  import Onething from '.';

  function Something() {
    const Nothing = styled.div``;

    return (
      <Fragment>
        <Onething>
          <Nothing></Nothing>
          <Nothing></Nothing>
        </Onething>
        <Nothing />
      </Fragment>
    );
  }
  ```

  위의 코드를 살펴보면 어떤 컴포넌트가 로직이 없고 UI만 설정해준 styled-component이고 로직과 UI를 모두 설정해준 일반 component인지 분간이 어려워 보인다. 이를 해결하기 위해 아래와 같이 styled-component를 나타낼 수 있는 컨벤션을 지정해줄 수도 있을 것 같다.

  ```javascript
  import Onething from '.';

  function Something() {
    const Styled = {
      Nothing: styled.div``,
    };

    return (
      <Fragment>
        <Onething>
          <Styled.Nothing></Styled.Nothing>
          <Styled.Nothing></Styled.Nothing>
        </Onething>
        <Styled.Nothing />
      </Fragment>
    );
  }
  ```

<br>

- [[#74](https://github.com/woowacourse/react-payments/pull/74#discussion_r861542674) - 한 번에 import]

  ```javascript
  import useCardNumber from './useCardNumber';
  import useValidDate from './useValidDate';
  import useCardOwnerName from './useCardOwnerName';
  import useCVC from './useCVC';
  import useCardPassword from './useCardPassword';
  import useModal from './useModal';

  export { useCardNumber, useValidDate, useCardOwnerName, useCVC, useCardPassword, useModal };
  ```

  - 디렉토리에 index 파일을 만들어서 다른 파일에서 import 구문을 줄일 수 있다고 한다.

  - > 오호 찾아보니까 지금처럼 경로에 직접 접근하여 사용한다면 만약 여러 곳에서 import하는 경우에는 불러온만큼 import를 하게 되므로 비효율적인 코드가 된다는 것 같았습니다. 그런 의미에서는 import를 한번에 하는 index 파일이 있는 편이 더 좋을 것 같네요 🙂 깔끔하기도 하고요 !

<br>

- [[#97](https://github.com/woowacourse/react-payments/pull/97#discussion_r862346217) - 변수명의 prefix]

  ```javascript
  const isNumberCharacter = () => {};
  const isShowInvalidMessage = () => {};
  ```

  - > is Prefix가 붙어서 true or false가 반환될 거 같은 네이밍이지만, 로직상으로 숫자가 반환될 수도 있겠군요

  - 위처럼, 변수명의 prefix를 보고 사람들이 해당 변수에 어떤 값이 담기게 될지, 함수에서 어떤 값이 반환하게 될지를 예측할 수 있어야한다. 그러니 신경써서 네이밍 하자!

<br>

- [[#90](https://github.com/woowacourse/react-payments/pull/90#discussion_r862373706) - 변수명의 prefix]

  - > prop에 값을 따로 전달하지 않으면 true 로 전달되기 때문에, 보통 true 를 넘길 땐 값을 따로 명시하지 않는 편이에요! https://reactjs.org/docs/jsx-in-depth.html#props-default-to-true

<br>
