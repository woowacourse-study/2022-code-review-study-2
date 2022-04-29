## 1. 왜 styled-components를 사용하는가?

### 1. styled-components 란?

컴포넌트에 스타일을 더할 수 있도록 해주는 라이브러리

CSS-in-JS 방식이다. CSS 파일을 따로 두지 않고, JavaScript로 작성된 컴포넌트에 CSS를 바로 삽입하는 스타일 기업이다.

기존에 HTML, CSS, JavaScript를 모두 분리하여 따로 관리하는 방식을 지향했다. React에서 HTML과 JavaScript를 한 데 묶은 JSX를 사용하고, styled-components를 사용하면 JS 파일 하나에 CSS까지 묶어서 사용할 수 있다.

```jsx
// app.jsx
const Title = styled.h1`
  font-size: 1.5em;
`;

function App() {
  return <Title>Hello World!</Title>;
}
```

Title 처럼, 이름이 컴포넌트로 지정되었고 이를 그 파일 속에서 곧바로 스타일링할 수 있게 해준다.

위 코드는 다음과 같다.

```jsx
// app.jsx
function App () {
  return (
    <h1>
      Hello World!
    </h1>
  );
}

// app.css
h1 {
  font-size: 1.5em;
}
```

### 2. styled-components 의 특징 및 장점

- css가 js에 들어가 있기 때문에, 동적 스타일링이 간단하다.
- no-class coding - 구현 시 클래스명이 임의로 부여된다. 이로 인한 버그를 줄인다.

### 3. **styled-components와 scss 비교**

- styled-components
  - 동적인 이벤트가 많은 사이트라면 컴포넌트가 자주 렌더링 될 때 그만큼 스타일 정보도 다시 읽어와야 된다.그에 반해 css in css는 이미 html문서에 읽혀져 있는 상태이기 때문에 처음에는 스타일 정보를 가져오는 양이 많더라도 그 후 추가적인 렌더링은 상대적으로 style-components보다 적을 것이다. 그러나 이를 개선하기 위해 CSS-in-JS에서도 css를 SSR 방식으로 넣어주는 등 다양한 노력을 이어가고 있다.
  - **css in js** 방식으로 컴포넌트가 렌더링 될 때만 해당 스타일 정보를 읽는다
    - webpack의 트리 셰이킹을 통해서 사용하지 않는 스타일 코드들이 제거되어질 수 있어서 성능의 향상을 가져온다.
  - FOCU(flash of unstyled content)
    - 스타일 시트가 적용되기 전 마크업 된 그대로의 모습이 잠깐 보이는 현상이다. 원래는 브라우저를 렌더링할때, 스타일요소와 스크립트가 병렬적으로 행해졌는데, 이제는 모든 스타일 코드가 스크립트 안에 들어가 있으므로, 스크립트가 방대해지고 스타일이 적용되지 않은 html뼈대인 FOUC가 나타나서 좋지 않은 사용자 경험을 줄 수 있다.
- scss
  - 브라우저에 보이지 않은 컴포넌트까지 읽기 때문에 불필요한 컴파일 과정이 추가된다.
  - css in css는 이미 html문서에 읽혀져 있는 상태이기 때문에 처음에는 스타일 정보를 가져오는 양이 많더라도 그 후 추가적인 렌더링은 상대적으로 style-components보다 적을 것이다.

## 2. 기본적인 사용 방법

### 1. 설치 방법

```jsx
yarn add styled-components

npm install styled-components
```

그리고, 스타일링 처리할 js 파일 에서

```jsx
import styled from "styled-components";
```

→ styled API를 사용할 수 있다.

- 자동완성 VS Extension

  vscode-styled-components

### 2. 기본 문법

- tagged template literal 을 사용한다. (tag + ` back tick)
- Components 이름을 대문자로 선언한다.
- styled API를 사용하여 스타일링한다.

```jsx
const Btn = styled.button`
  font-size: 30px;
  width: 40%;
  height: 100px;
  margin: 5%;
`;

const Button = (props) => {
  return <Btn>React Study!</Btn>;
};
```

### 3. 가변 스타일링 1

styled-components - CSS를 간단하게 처리할 수 있는 것이 큰 장점이다

→ React.Component 간 props를 사용하여 동적인 변수를 넘겨주는 것과 같이, styled-components 에서도 props를 활용한다.

```jsx
const Container = styled.div`
  background-color: ${(props) => props.color};
  width: 100%;
  height: 100%;
  text-align: center;
`;

function App() {
  let [color, setColor] = useState("black");
  function onClick() {
    setColor(color === "black" ? "white" : "black");
  }

  return (
    <Container color={color}>
      <Button onClick={onClick} bc={color} />
      <Button onClick={onClick} bc={color} />
      <Button onClick={onClick} bc={color} />
      <Button onClick={onClick} bc={color} />
    </Container>
  );
}
```

```jsx
const Btn = styled.button`
  color: ${(props) => props.bc};
  background-color: ${(props) => (props.bc === "black" ? "white" : "black")};

  font-size: 30px;
  width: 40%;
  height: 100px;
  margin: 5%;
`;

const Button = ({ onClick, bc }) => {
  return (
    <Btn onClick={onClick} bc={bc}>
      React Study!
    </Btn>
  );
};
```

### 4. 가변 스타일링 2 (조건을 만족할 때, 두 개 이상의 스타일을 주고 싶을 때)

css API를 사용한다.

```jsx
import styled, { css } from "styled-components";

const Btn = styled.button`
  ${(props) =>
    props.bc === "black" &&
    css`
      color: black;
      background-color: white;
    `}
  ${(props) =>
    props.bc === "white" &&
    css`
      color: white;
      background-color: black;
    `}
    font-size:30px;
  width: 40%;
  height: 100px;
  margin: 5%;
`;
```

## 3. 추가적인 사용 방법

### 1. & - 자기 선택 문자

```jsx
const Btn = styled.button`
  width: 40%;
  height: 100px;
  margin: 5%;
  transition: transform 300ms ease-in;
  &:hover {
    transform: scale(1.1);
  }
`;
```

### 2. className을 물론 선언할 수 있다.

```jsx
<Btn className="Buttons123" onClick={onClick} bc={bc}>
  React Study!
</Btn>
```

### 3. 전역 스타일(GlobalStyle) 사용 (글꼴, \*, box-sizing, button, p,)

```jsx
// GlobalStyle.js

import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
  *, *::before, *::after {
    box-sizing: border-box;
  }

  body {
    font-family: "Helvetica", "Arial", sans-serif;
    line-height: 1.5;
  }
`;

export default GlobalStyle;

//app.jsx (최상위 컴포넌트에)
import GlobalStyle from "./GlobalStyle";

function App() {
  return (
    <>
      <GlobalStyle />
      <BlogPost title="Styled Components 전역 스타일링">
        이번 포스팅에서는 Styled Components로 전역 스타일을 정의하는 방법에
        대해서 알아보겠습니다.
      </BlogPost>
    </>
  );
}
```

### 4. CSS 전역 변수 사용 (ThemeProvider)

CSS 에서 :root {} 를 생성하여 변수를 사용하는 것과 같다.

- 필요성

  1. 스타일 코드의 일관성을 유지하기 위하여.
  2. 협업 시 통일된 단위를 사용하기 위하여.
  3. 재사용을 위하여.

- ThemeProvider 사용 방법

  1. 최상위 컴포넌트에서 모든 컴포넌트를 ThemeProvider로 감싸준다.
  2. theme = {전역 변수} 를 속성으로 추가한다.
  3. 그렇다면 나머지 자식 요소의 props로 theme이 전해진다.
  4. 자식 요소에서 props.theme.전역변수 로 사용한다

```jsx
// app.jsx

import styled, { ThemeProvider } from 'styled-components';

function App() {
  return (
    <ThemeProvider
      theme={{
        palette: {
          blue: '#228be6',
          gray: '#495057',
          pink: '#f06595'
        }
      }}

      <AppBlock>
        <Button>BUTTON</Button>
        <Button color="gray">BUTTON</Button>
        <Button color="pink">BUTTON</Button>
      </AppBlock>
    </ThemeProvider>
  );
}

// button.jsx
const StyledButton = styled.button`
  /* 색상 */
  ${({theme, color}) => {
    const selected = theme.palette[color];
    return css`
      background: ${selected};
      &:hover {
        background: ${lighten(0.1, selected)};
      }
      &:active {
        background: ${darken(0.1, selected)};
      }
Button.defaultProps = {
    color: 'blue'
};

```

어떤 컴포넌트가 몇 단계를 거쳐서 depth를 갖더라도 루트에 ThemeProvider가 자리잡고 있다면, 모든 렌더 트리의 잣기에는 다 theme 속성을 갖게 된다.

큰 프로젝트를 진행할 때, 전역 변수가 많아질 때, 따로 theme.js를 만들어 주어서 관리한다.

```jsx
// theme.js

import styled from "styled-components";

// 반응형 디자인을 위한 픽셀 컨버팅 함수
const pixelToRem = (size) => `${size / 16}rem`;

// font size를 객체로 반환해주자.
const fontSizes = {
  title: pixelToRem(60),
  subtitle: pixelToRem(30),
  paragraph: pixelToRem(18),
};

// 자주 사용하는 색을 객체로 만들자.
const colors = {
  black: "#000000",
  grey: "#999999",
  green: "#3cb46e",
  blue: "#000080",
};

// mixin - 자주 사용하는 스타일 속성을 theme으로 만들어보자.
const common = {
  flexCenter: `
    display: flex;
    justify-contents: center;
    align-items: center;
  `,
  flexCenterColumn: `
    display: flex;
    flex-direction: column;
    justify-contents: center;
    align-items: center;
  `,
};

// theme 객체에 감싸서 반환한다.
const theme = {
  fontSizes,
  colors,
  common,
};

export default theme;

// app.js
import theme from "./theme";

const App = () => {
  return (
    <ThemeProvider theme={theme}>
      <Container></Container>
    </ThemeProvider>
  );
};

// 또는 index.js에 넣어준다.
import theme from "./style/theme";
import GlobalStyle from "./style/global";

ReactDOM.render(
  <React.StrictMode>
    <ThemeProvider theme={theme}>
      <App />
      <GlobalStyle />
    </ThemeProvider>
  </React.StrictMode>,
  document.getElementById("root")
);
```

### 5. 스타일 상속

const Btn2 = styled(Btn)``

⇒ Btn2 가 Btn의 스타일을 그대로 가져온다.

```jsx
const Btn = styled.button`
  color: blue;
  font-size: 30px;
  width: 40%;
  height: 100px;
  margin: 5%;
  transition: transform 300ms ease-in;
  &:hover {
    transform: scale(1.1);
  }
`;

const Btn2 = styled(Btn)`
  color: red;
`;

const Button = ({ onClick, bc }) => {
  return (
    <>
      <Btn className="Buttons123" onClick={onClick} bc={bc}>
        React Study!
      </Btn>
      <Btn2 onClick={onClick} bc={bc}>
        React Study!
      </Btn2>
    </>
  );
};
```

### 6. media query in styled-components

```jsx
const Btn = styled.button`
  width: 40%;
  height: 100px;
  margin: 5%;
  transition: transform 300ms ease-in;
  &:hover {
    transform: scale(1.1);
  }
  @media screen and (max-width: 768px) {
    width: 100%;
  }
`;
```
