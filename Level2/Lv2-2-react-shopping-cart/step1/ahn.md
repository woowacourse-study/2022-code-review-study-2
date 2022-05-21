## Level2 장바구니 Step1 - 안

### 분석 담당 코드

- [#64, 안](https://github.com/woowacourse/react-shopping-cart/pull/64)
- [#65, 코카콜라](https://github.com/woowacourse/react-shopping-cart/pull/65)
- [#95, 태태](https://github.com/woowacourse/react-shopping-cart/pull/95)
- [#70, 소피아](https://github.com/woowacourse/react-shopping-cart/pull/70)
- [#85, 록바](https://github.com/woowacourse/react-shopping-cart/pull/85)
- [#88, 샐리](https://github.com/woowacourse/react-shopping-cart/pull/88)
- [#69, 나인](https://github.com/woowacourse/react-shopping-cart/pull/69)
- [#74, 도리](https://github.com/woowacourse/react-shopping-cart/pull/74)

## 질문사항

> 스타일드 컴포넌트 양이 많으면, 컴포넌트 파일에 들어갔을 때 코드 상단에 컴포넌트 대신 스타일 코드가 먼저 보입니다. 파일을 들어갔을 때, 스타일보단 컴포넌트와 로직이 먼저 보이는 게 맞는 거 같아서 이번엔 각각의 컴포넌트 폴더 내부에 styled.jsx라는 파일을 만들어 사용했습니다. 컴포넌트를 함수 선언식으로 작성했기 때문에 스타일 코드를 밑에 내려도 되지만, 호이스팅에 의존하는 건 지양해야한다고 생각했습니다. 앞의 방법으로 하면 단점이 폴더가 너무 많아지고, 한 곳에 없으니 너무 분산되었다는 느낌이 들었습니다!

컴포넌트안에 스타일

- 한 곳에서 확인 가능
- 스타일드 컴포넌트 양이 많아지면 가독성이 떨어진다 -> 컴포넌트 분리를 잘 못 한건인가?
- 호이스팅 의존 지양?

스타일 파일 따로

- 폴더가 많아짐
- 분산되어있는 느낌

> 말씀하신대로 관련있는 코드가 한 곳에 모여있지 않으면 코드파악이 상대적으로 어렵고 분산된다는 느낌을 받을 수 있고, 또 반대로 컴포넌트 파일에 스타일 코드의 양이 너무 많아지게 되면 정작 컴포넌트를 파악하는데 불편함을 느끼게 되죠.
> 또 폴더가 많아지는 것 보단 폴더의 구조 자체가 컴포넌트의 구조와 관련이 없이 비대해지거나 도메인과 관련 없이 늘어나는 구조는 피해야 하고요.

> 그래서 보통은 디자인 시스템을 만들고 작게 만들어진 컴포넌트를 확장해 나가는 방식으로 코드를 작성합니다.
> 이럴 경우 스타일코드가 차지하는 비중이 줄어 비지니스 로직 보다 앞에 있다고 하더라도 크게 방해되지 않는 선으로 작성될 수 있을 것 같아요. 다만 스타일 코드를 어떻게 관리하느냐에 따라 작성 방식이 좀 달라 지는 것이죠.

## 피드백 정리

- [#65](https://github.com/woowacourse/react-shopping-cart/pull/65#discussion_r872435175)

```jsx
// before
const StyledImageBox = styled.div`
  width: ${(props) =>
    `${
      props.width === "large" ? 430 : props.width === "middle" ? 250 : 100
    }`}px;
  height: ${(props) =>
    `${
      props.height === "large" ? 430 : props.height === "middle" ? 250 : 100
    }`}px;
`;

//
// after
const SIZE_MAP = {
  large: 430,
  middle: 250,
  small: 100,
};

const StyledImageBox = styled.div`
  width: ${(props) => `${SIZE_MAP[props.width]}`}px;
  height: ${(props) => `${SIZE_MAP[props.height]}`}px;
  border-radius: 8px;
  overflow: hidden;
`;
```

<br>

- [#95](https://github.com/woowacourse/react-shopping-cart/pull/95#discussion_r874895687)

```jsx
//전
const productList = useSelector((state) => state.productList.data);
const isLoading = useSelector((state) => state.productList.isLoading);
const errorMessage = useSelector((state) => state.productList.errorMessage);

// 후
const {
  isLoading,
  errorMessage,
  data: productList,
} = useSelector((state) => state.productList);
```

<br>

- [#70](https://github.com/woowacourse/react-shopping-cart/pull/70#discussion_r873869237)
  생성하고 채우고 한번에 ~!

```jsx
// 전
const dummyProductList = [];
dummyProductList.length = 22;
dummyProductList.fill(dummyProduct);

//후
const productCount = 22;
const dummyProductList = Array(productCount).fill(dummyProduct);
```

<br>

- [#70](https://github.com/woowacourse/react-shopping-cart/pull/70#discussion_r873052236)

> dispatch, selector, fetch, effect훅까지 포함해서 비즈니스 로직을 담은 커스텀 훅으로 분리해보시면 어떨까요?
> 꼭 '재사용'뿐만이 아니라 '관심사 분리'의 측면으로도 활용해보시면 좋을 것 같아요 🙂
> 컴포넌트가 가능한 렌더링에 관련된 부분만 신경쓸 수 있게요!
> <br>

- [#70](https://github.com/woowacourse/react-shopping-cart/pull/70#discussion_r873053702)

> div의 배경 이미지로 넣는 것과 `img` 태그로 넣는 것은 어떤 차이가 있나요?

이미지 자체가 컨텐츠로 취급되어야 한다면 img태그, 디자인 요소로만 사용된다면 background-image로 사용하는 것을 권장하고 있는 것으로 알고 있어요 🙂 참고해보시면 좋을 것 같습니다~
<br>

- [#85](https://github.com/woowacourse/react-shopping-cart/pull/85#discussion_r872586831)

차크라 플랙스

```jsx
const Flex = styled.div`
  ${({
    direction = "row",
    wrap = "nowrap",
    justify = "normal",
    align = "normal",
    gap = "0",
  }) => css`
    display: flex;
    flex-direction: ${direction};
    flex-wrap: ${wrap};
    justify-content: ${justify};
    align-items: ${align};
    gap: ${gap};
  `}
`;

// 1.
<Flex justify="center" align="center" direction="column" gap="40px">
  <img src={NotFoundImage} alt="결과 없음 이미지" />
  <Styled.TextBox>
    이용에 불편을 드려 죄송합니다.
    <br /> 홈페이지로 이동하시어 서비스를 다시 이용해주세요.
  </Styled.TextBox>
  <Link to="/react-shopping-cart">
    <img src={HomeButtonImage} alt="홈으로 가는 이미지" />
  </Link>
</Flex>

// 2.
<Flex justify="center" align="center">
  <img src={thumbnail} alt="상품 이미지" />
</Flex>;
```

<br>
