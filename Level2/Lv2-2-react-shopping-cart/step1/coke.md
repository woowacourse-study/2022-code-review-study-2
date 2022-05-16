# Level2 페이먼츠 미션 Step2 - 코카콜라

- [#65, 코카콜라](https://github.com/woowacourse/react-shopping-cart/pull/65)
- [#64, 안](https://github.com/woowacourse/react-shopping-cart/pull/64)
- [#96, 해리](https://github.com/woowacourse/react-shopping-cart/pull/96)
- [#84, 무비](https://github.com/woowacourse/react-shopping-cart/pull/84)
- [#68, 위니](https://github.com/woowacourse/react-shopping-cart/pull/68)
- [#67, 아놀드](https://github.com/woowacourse/react-shopping-cart/pull/67)
- [#66, 결](https://github.com/woowacourse/react-shopping-cart/pull/66)

---

## 피드백 정리

### html tag

- [#68, 위니, img alt 속성](https://github.com/woowacourse/react-shopping-cart/pull/68)

img alt 속성 추가하자!

- src 특성은 필수이며, 포함하고자 하는 이미지로의 경로를 지정합니다.
- alt 특성은 이미지의 텍스트 설명이며 필수는 아니지만, 스크린 리더가 alt의 값을 읽어 사용자에게 이미지를 설명하므로, 접근성 차원에서 매우 유용합니다. 또한 네트워크 오류, 콘텐츠 차단, 죽은 링크 등 이미지를 표시할 수 없는 경우에도 이 속성의 값을 대신 보여줍니다.

---

- [#68, 위니, default 이미지로 대체](https://github.com/woowacourse/react-shopping-cart/pull/68)

이미지를 불러오지 못하는 문제 대응, 상품 이미지를 default 이미지로 대체
[how-to-replace-img-src-onerror-with-react](https://thewebdev.info/2022/05/10/how-to-replace-img-src-onerror-with-react/)

```javascript
import React, { ImgHTMLAttributes, useState } from "react";

export default function ImageWithFallback({ fallback, src, ...props }) {
  const [imgSrc, setImgSrc] = useState(src);
  const onError = () => setImgSrc(fallback);

  return <img src={imgSrc ? imgSrc : fallback} onError={onError} {...props} />;
}
```

---

### Custom Hook

fetch 호출에 대한 Hook을 만들어서 정리해보는 건 어떨까요? 🙂

- API 호출상태와 에러상태를 분리할 수 있어요.
- fetch API를 특정컴포넌트에서 직접적으로 호출하는 걸 막아줄 수 있어요.
- fetch API를 호출하는 방식을 관리할 수 있어요. (여러 컴포넌트에서 동일하게 호출)
  ex) [예시링크](https://velog.io/@chun_gil/How-to-fetch-data-with-React-Hooks%EC%A0%95%EB%A6%AC)

useEffect data fetching 중단

- 해당 컴포넌트가 마운트 해제가 되었음에도 상태가 설정되는 이슈
- 마운트 해제된 컴포넌트 상태 설정 방지
- 내부 분기 처리 로직을 통해 해결

```javascript
const useDataApi = (initialUrl, initialData) => {
  const [url, setUrl] = useState(initialUrl);
  const [state, dispatch] = useReducer(dataFetchReducer, {
    isLoading: false,
    isError: false,
    data: initialData,
  });

  useEffect(() => {
    let didCancel = false;
    const fetchData = async () => {
      dispatch({ type: "FETCH_INIT" });
      try {
        const result = await axios(url);
        if (!didCancel) {
          dispatch({ type: "FETCH_SUCCESS", payload: result.data });
        }
      } catch (error) {
        if (!didCancel) {
          dispatch({ type: "FETCH_FAILURE" });
        }
      }
    };
    fetchData();
    return () => {
      didCancel = true;
    };
  }, [url]);

  return [state, setUrl];
};
```

---

### CSS

- [#84, 무비, styled-reset](https://github.com/woowacourse/react-shopping-cart/pull/84)

- css를 reset 해주는 라이브러리 https://www.npmjs.com/package/styled-reset
- styled-component의 globalStyles 활용

```javascript
// src/components/GlobalStyles.js
import { createGlobalStyle } from "styled-components";
import reset from "styled-reset";

const GlobalStyles = createGlobalStyle`
    ${reset}
    html,
    body,
    #root {
      width: 100%;
      height: 100%;
      margin: 0;
      font-family: 'Noto Sans KR';
      color: red;
    }
    input,
    textarea,
    button {
      font-family: 'Noto Sans KR';
    }
`;

export default GlobalStyles;

// src/App.js

import GlobalStyles from 'components/GlobalStyles';


...
          <Route path={BASE_URL} element={<ProductListPage />} />
        </Routes>
      </StyledRoutes>
      <GlobalStyles />
    </BrowserRouter>
  );
```

---

- [#66, 결, 컬러 범용적 사용 링크 참조](https://github.com/woowacourse/react-shopping-cart/pull/66)

컬러 범용적 사용 링크 참조
[발리스타~컬러 링크](https://react-spectrum.adobe.com/react-spectrum/styling.html#color-values)

---

### 스타일 컴포넌트

- [#65, 코카콜라, props, theme 코딩 스킬](https://github.com/woowacourse/react-shopping-cart/pull/65)

```javascript
// before
import styled from "styled-components";

const StyledImageWrapper = styled.div`
  width: ${({ width, theme }) =>
    `${
      width === "large"
        ? theme.IMAGE_SIZE_MAP.large
        : width === "middle"
        ? theme.IMAGE_SIZE_MAP.middle
        : theme.IMAGE_SIZE_MAP.small
    }`}px;
  height: ${({ height, theme }) =>
    `${
      height === "large"
        ? theme.IMAGE_SIZE_MAP.large
        : height === "middle"
        ? theme.IMAGE_SIZE_MAP.middle
        : theme.IMAGE_SIZE_MAP.small
    }`}px;
`;

// refactor

const StyledImageWrapper = styled.div`
  width: ${({ width, theme }) =>
    `${theme.IMAGE_SIZE_MAP[width] || theme.IMAGE_SIZE_MAP.middle}px;
  height: ${({ height, theme }) =>
    `${theme.IMAGE_SIZE_MAP[height] || theme.IMAGE_SIZE_MAP.middle}px;
`;

// src/stles/theme.js
const IMAGE_SIZE_MAP = {
  large: 430,
  middle: 250,
  small: 100,
};

const theme = {
  IMAGE_SIZE_MAP,
};

export default theme;
```
