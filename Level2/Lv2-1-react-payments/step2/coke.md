# Level2 페이먼츠 미션 Step2 - 코카콜라

- [#134, 코카콜라](https://github.com/woowacourse/react-payments/pull/134)
- [#110, 태태](https://github.com/woowacourse/react-payments/pull/110)
- [#123, 콤피](https://github.com/woowacourse/react-payments/pull/123)
- [#128, 티거](https://github.com/woowacourse/react-payments/pull/128)
- [#121, 호프](https://github.com/woowacourse/react-payments/pull/121)
- [#111, 샐리](https://github.com/woowacourse/react-payments/pull/111)
- [#129, 민초](https://github.com/woowacourse/react-payments/pull/129)
- [#132, 위니](https://github.com/woowacourse/react-payments/pull/132)

---

## 피드백 정리

### Context

- [#123, 콤피, Context API](https://github.com/woowacourse/react-payments/pull/123)

컨텍스트는 모든 수준에서 props를 수동으로 전달하지 않고도 구성 요소 트리를 통해 데이터를 전달할 수 있는 방법을 제공한다.

**컨텍스트를 사용해야 하는 경우**

- 컨텍스트는 현재 인증된 사용자,
- 테마 또는 선호하는 언어 등
- 전역으로 간줄될 수 있는 테이터를 공유해야 한다.

**컨텍스트 주의 할 점**

- 컨텍스트는 다른 중첩 수준의 많은 구성 요소에서 일부 데이터에 액세스해야 할 때 주로 사용해야 한다.
- 컨텍스트를 사용하면 컴포넌트 재사용을 어렵게 하므로 드물게 사용해야 한다.
- 컨텍스트 대신 컴포넌트 합성을 사용 하도록 하자.

---

### Provider

- [#134, 코카콜라, Provider 여러개 일때, BrowserRouter 위치](https://github.com/woowacourse/react-payments/pull/134)

[context 가 왜 나왔을까?](https://reactjs.org/docs/context.html#:~:text=Context%20provides%20a%20way%20to%20pass%20data%20through%20the%20component%20tree%20without%20having%20to%20pass%20props%20down%20manually%20at%20every%20level.)

Provider가 여러개 라면 BrowserRouter 의 위치는 어느곳에 놔둬야 적당할까요? 어떤 기준이 있는 걸까요? 아니면 그냥 적당한 위치에 두는 걸까요?

```javascript
// src/index.jsx
// 현재 반영된 코드
root.render(
  <React.StrictMode>
    <BrowserRouter basename={process.env.PUBLIC_URL}>
      <CardProvider>
        <App />
      </CardProvider>
    </BrowserRouter>
  </React.StrictMode>
);

// 샘플 코드
root.render(
  <React.StrictMode>
    <HelmetProvider>
      <Provider store={store}>
        <StyledEngineProvider>
          <SettingsProvider>
            <BrowserRouter basename={process.env.PUBLIC_URL}>
              <AuthProvider>
                <SessionProvider>
                  <App />
                </SessionProvider>
              </AuthProvider>
            </BrowserRouter>
          </SettingsProvider>
        </StyledEngineProvider>
      </Provider>
    </HelmetProvider>
  </React.StrictMode>
);
```

> 리뷰어: BrowserRouter에서 context에 담긴 값을 사용해야하는 일이 있을까요? 관계를 생각해서 위치를 정해주시면 될것 같습니다.

---

### 컨벤션

- [#110, 태태, styled-components 위치](https://github.com/woowacourse/react-payments/pull/110)

스타일 컴포넌트는 아래로 이동하자

```javascript
// before
import useInputHandler from "../../hooks/useInputHandler";
import { validatePassword } from "../../validator";

const InputPasswordWrapper = styled.div``;

...

const Page = () =>{
    ...
}

// refactor
import useInputHandler from "../../hooks/useInputHandler";
import { validatePassword } from "../../validator";

const Page = () =>{
    ...
}

const InputPasswordWrapper = styled.div``;
...
```

---

### React

- [#110, 태태, <></> fragment vs <React.Fragment>](https://github.com/woowacourse/react-payments/pull/110)

<></> fragment 만 사용하면 키나 속성을 추가할 수 없다.
키나 속성을 추가 할려면 <></> fragment 대신 <React.Fragment>로 사용해야 한다.

---

- [#121, 호프, context 전역 상태관리](https://github.com/woowacourse/react-payments/pull/121)

```javascript
// src/context/card-form-context.js

secondCardNumber: '',
thirdCardNumber: '',
fourthCardNumber: '',
isInitialCardNumber: true,
...
```

전역에서 관리되어야 될 상태는 최소화 될수록 좋다. is\*로 시작하는 이런 상태들은 일시적으로 사용되는 값들로 보인다.
예를 들어 다른 컴포넌트에서 사용되지 않고 한 곳에서만 사용되는 전역 상태값은 생각을 해보는 것이 좋다.

---

- [#132, 위니, false 일 때 따로 렌더링 할게 없다면 && 사용](https://github.com/woowacourse/react-payments/pull/132)

```javascript
// before
{
  cards.length
    ? cards.map((item) => (
        <li key={item.nickname}>
          <Card isEmpty={false} cardInfo={item} />
          <div className="nickname-text">{item.nickname}</div>
        </li>
      ))
    : "";
}

// refactor
{
  cards.length > 0 &&
    cards.map((item) => (
      <li key={item.nickname}>
        <Card isEmpty={false} cardInfo={item} />
        <div className="nickname-text">{item.nickname}</div>
      </li>
    ));
}
```

### 스타일 컴포넌트

- [#111, 샐리, 스타일 컴포넌트 props](https://github.com/woowacourse/react-payments/pull/111)

```javascript
// before
return (
<EmptyCardWrapper color={cardType.color} size={size}>
)

// refactor
const EmptyCardWrapper = styled.div`
  width: ${(props) => CardScaleType[props.size].width}px;
  height: ${(props) => CardScaleType[props.size].height}px;
  ...

  ${CardName} {
    font-size: ${(props) => CardScaleType[props.size].fontSize}px;
  }
`;


<EmptyCardWrapper color={cardType.color} size={size}>
  ...
</EmptyCardWrapper>

```
