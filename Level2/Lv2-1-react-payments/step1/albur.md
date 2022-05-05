# Leve2-1 React-payments Step1 - 앨버

- 분석 담당 코드

  - [#73](https://github.com/woowacourse/react-payments/pull/73)
  - [#74](https://github.com/woowacourse/react-payments/pull/74)

  - [#97](https://github.com/woowacourse/react-payments/pull/97)
  - [#100](https://github.com/woowacourse/react-payments/pull/100)

  - [#88](https://github.com/woowacourse/react-payments/pull/88)
  - [#90](https://github.com/woowacourse/react-payments/pull/90)

## 다른 크루들 코드 분석

#### 상태 관리를 어디서 해주는지? (최상단?)

#### 커스텀 훅을 어떻게 사용해주는지?

#### 이벤트 핸들러를 어떻게 내려주는지? (함수를 만들어서 내려주는지?)

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
