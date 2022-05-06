# 코드리뷰
## [병민](https://github.com/woowacourse/react-payments/pull/87)
### 파일구조
```
payment
├─ src
│  ├─ App.tsx
│  ├─ components
│  │  ├─ Provider.tsx
│  │  ├─ card
│  │  │  ├─ Card.tsx
│  │  │  └─ CardContainer.tsx
│  │  ├─ card-form
│  │  │  ├─ Fieldset.tsx
│  │  │  ├─ card-cvc
│  │  │  │  ├─ CVCFieldset.tsx
│  │  │  │  ├─ CVCInput.tsx
│  │  │  │  └─ CVCInputContainer.tsx
│  │  │  ├─ card-expired-period
│  │  │  │  ├─ ExpiredPeriodFieldset.tsx
│  │  │  │  ├─ ExpiredPeriodInput.tsx
│  │  │  │  └─ ExpiredPeriodInputContainer.tsx
│  │  │  ├─ card-number
│  │  │  │  ├─ CardNumberFieldset.tsx
│  │  │  │  └─ CardNumberInputContainer.tsx
│  │  │  ├─ card-owner
│  │  │  │  ├─ CardOwnerNameFieldset.tsx
│  │  │  │  ├─ CardOwnerNameInput.tsx
│  │  │  │  └─ CardOwnerNameInputContainer.tsx
│  │  │  ├─ card-password
│  │  │  │  ├─ CardPasswordFieldset.tsx
│  │  │  │  ├─ CardPasswordInput.tsx
│  │  │  │  ├─ CardPasswordInputContainer.tsx
│  │  │  │  └─ CardPasswordInputContainerList.tsx
│  │  │  └─ confirm-button
│  │  │     ├─ ConfirmButton.tsx
│  │  │     └─ ConfirmButtonContainer.tsx
│  │  ├─ navigation
│  │  │  ├─ BackButton.tsx
│  │  │  ├─ Navigation.tsx
│  │  │  └─ PageTitle.tsx
│  │  └─ templates
│  ├─ constants.ts
│  ├─ custom.d.ts
│  ├─ hooks
│  │  ├─ hooks.ts
│  │  └─ useForm
│  │     ├─ constants.ts
│  │     ├─ types.ts
│  │     ├─ useForm.tsx
│  │     ├─ useFormContext.tsx
│  │     └─ utils.ts
│  ├─ images
│  │  └─ back-arrow.svg
│  ├─ index.tsx
│  ├─ scss
│  │  ├─ _flex.scss
│  │  ├─ _spacing.scss
│  │  ├─ _typhography.scss
│  │  ├─ _variables.scss
│  │  ├─ components
│  │  │  ├─ _back-arrow.scss
│  │  │  └─ _helptip.scss
│  │  └─ style.scss
│  ├─ types.ts
│  └─ utils.ts
```
### 디렉토리 및 컴포넌트 분리
```
일단 저는 atomic design 패턴은 잘못된 패턴이라고 생각합니다. 디자인관점에서 봤을때 컴퓨터가 처음나오고 인터넷이 처음 나온 시절에 atomic 사고로 ui를 만들지는 않았을테고, 사이트끼리 서로 디자인을 베끼고 사용자들에게 선택되어 남은 ui 요소가 있겠죠. 그리고 스마트폰이 등장하면서 HCI,UX 학계, 구글과 같은 업체에서 2D와 터치스크린에서 만들 수 있는 요소는 다 테스트한걸로 알고있습니다. 모바일 가이드라인 애플의 human interface guideline, 구글의 material design만 봐도 모두 atomic을 언급하지 않고 있고요.
지금은 작은 프로젝트여서 괜찮겠지만 지금 같은 구조가 더 커졌을때 관리하기 편할지는 잘 모르겠습니다. 도메인과 기능을 고려하지 않고 단순히 atomic구조나 역할별로 나누면 규모가 커졌을때 관리하기 힘들다고 생각합니다. (https://ahnheejong.name/articles/package-structure-with-the-principal-of-locality-in-mind)
```

[ahnheejong.name/articles/package-structure-with-the-principal-of-locality-in-mind/][1]
[1]: https://ahnheejong.name/articles/package-structure-with-the-principal-of-locality-in-mind/

### 가독성
```
개인 스타일 차이일수도 있지만 스타일 변수들을 아래로 위치하는게 좋다고 생각합니다. 그러한 이유는 파일은 목차와 같고 해당 파일을 열었을때 해당 파일의 핵심 부분이 보이는게 읽는 흐름을 끊지 않습니다. 책을 읽을때 목차를 보고 해당 페이지를 펼쳤는데 목차 제목이 보이지 않고 주석과 각주가 먼저 보인다면 굉장히 당황할것 같고 1초 멈칫하게 되죠. 그리고 1-2초 스크롤 하는 시간이 추가되고요.
```
[Comment Link](https://github.com/woowacourse/react-payments/pull/87#discussion_r862360791)

### 네이밍

```
<Fieldset>
	<Head marginBottom='8px'>
	  <label>
	    카드 번호
	  </label>
	</Head>
	<Body>
	<CardNumberInputContainer />
	</Body>
</Fieldset>
```

`Head와 Body html 태그와 같고, Fieldset또한 특정태그인데 Head과 Body가 import되서 저는 혼란스러웠어요`

[Comment Link](https://github.com/woowacourse/react-payments/pull/87#discussion_r862361853)

## [결](https://github.com/woowacourse/react-payments/pull/86)

### 파일 구조
```
react-payments-kyoul-step1
├─ src
│  ├─ .prettierrc.json
│  ├─ App.tsx
│  ├─ components
│  │  ├─ card
│  │  │  ├─ Card.tsx
│  │  │  ├─ CardForm.tsx
│  │  │  ├─ CardFormInput.tsx
│  │  │  ├─ CardFormLabel.tsx
│  │  │  └─ ConfirmButton.tsx
│  │  ├─ modal
│  │  │  ├─ ButtonText.tsx
│  │  │  ├─ Modal.tsx
│  │  │  └─ TypeButton.tsx
│  │  └─ navigater
│  │     ├─ BackButton.tsx
│  │     └─ PageTitle.tsx
│  ├─ constants.ts
│  ├─ containers
│  │  ├─ card
│  │  │  ├─ CVCInputContainer.tsx
│  │  │  ├─ CardContainer.tsx
│  │  │  ├─ CardFormContainer.tsx
│  │  │  ├─ CardNumberInputContainer.tsx
│  │  │  ├─ CardOwnerNameInputContainer.tsx
│  │  │  ├─ CardPasswordInputContainer.tsx
│  │  │  ├─ ConfirmButtonContainer.tsx
│  │  │  └─ ExpiredPeriodInputContainer.tsx
│  │  └─ modal
│  │     ├─ TypeButtonContainer.tsx
│  │     └─ TypeButtonModalContainer.tsx
│  ├─ context
│  │  └─ Provider.tsx
│  ├─ fields
│  │  ├─ CVCFieldset.tsx
│  │  ├─ CardNumberFieldset.tsx
│  │  ├─ CardOwnerNameFieldset.tsx
│  │  ├─ CardPasswordFieldset.tsx
│  │  ├─ ExpiredPeriodFieldset.tsx
│  │  ├─ Fieldset.tsx
│  │  └─ Navigation.tsx
│  ├─ hooks
│  │  └─ hooks.ts
│  ├─ index.tsx
│  ├─ pages
│  │  └─ AddCardPage.tsx
│  ├─ scss
│  │  ├─ _flex.scss
│  │  ├─ _spacing.scss
│  │  ├─ _typhography.scss
│  │  ├─ components
│  │  │  └─ _helptip.scss
│  │  └─ style.scss
│  ├─ types.ts
│  └─ utils.ts
```

### 파일의 위치가 적당 한가?

```
components 폴더 최상위에 이 파일(Provider)을 두었는데요- contexts 같은 폴더를 두지 않고 여기에 둔 이유가 있나요?
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/86#discussion_r862354815)

### 재사용을 고려한 컴포넌트 분리

```
그럼 현재 결이 생각하는 방향의 컴포넌트들은 재사용이 가능한가요-? 동일한 디자인의 인풋을 props가 다를 때마다 개별적으로 만들게 된다면 우후죽순 늘어나게 되지 않을까요? 동일한 인풋을 다른 서비스 페이지에서 사용하기 위해서는 또 만들어서 사용하게 될 것 같지 않나요~? 🙂 재사용성을 고려한 컴포넌트에 대해 한번 더 고심해 보셨으면 좋겠네요. 그리고 input이 가지는 속성이 많기 때문에 사용하는 속성에 따라 당연히 props가 많을 수 밖에 없죠~ props를 유연하게 받기 위해 팁을 주자면, rest parameter 와 spread operator 로 접근해 보면 어떨까요?
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/86#discussion_r862857040)

### Component안에서 Eary Return
#### 가독성 Bad
```
 return(
    <>
      { 
        disabled ? 
          <Input disabled placeholder='•' />
          : <Input id="card-password-input" autoComplete="off" type="text" onChange={onChange} value={value} placeholder='' ref={ref} />
      }
    </>
```

#### 가독성 Good
```
if (disabled) {
    return <Input disabled placeholder='•' />;
  }
  
  return <Input id="card-password-input" autoComplete="off" type="text" onChange={onChange} value={value} placeholder='' ref={ref} />;
```

## [비녀](https://github.com/woowacourse/react-payments/pull/95)

### 파일 구조
```
react-payments-kangyunho1221_step1
└─ src
  ├─ App.css
  ├─ App.js
  ├─ components
  │  ├─ Card
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ CardColorPicker
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ CardNumberInput
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ CardPasswordInput
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ Color
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ ExpiredDateInput
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ ModalContainer
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ NextButton
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ OwnerNameInput
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  ├─ SecureCodeInput
  │  │  ├─ index.jsx
  │  │  ├─ index.scss
  │  │  └─ index.stories.js
  │  └─ elements
  │     ├─ Button
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     ├─ Input
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     ├─ InputContainer
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     └─ label
  │        ├─ index.jsx
  │        ├─ index.scss
  │        └─ index.stories.js
  ├─ const.js
  ├─ index.css
  ├─ index.js
  └─ pages
      └─ CardAdd
        ├─ index.jsx
        ├─ index.scss
        └─ index.stories.js
```


### HTML5 Form Validation

[HTML5 폼 검증에 대해 정리해 보자](https://jeonghwan-kim.github.io/dev/2020/06/08/html5-form-validation.html)

### 구조 분해 할당

#### 가독성 Bad
`export const Input = forwardRef((props, ref) => (`

#### 가독성 Good
```
export const Input = forwardRef(({
  type, 
  maxLength, 
  value, 
  placeholder, 
  onChange, 
  onKeyDown, 
  className = 'input__contents',
  ...otherProps}, ref) => (
```
```
props 파라미터에서 객체분해 할당으로 작성해 주는게 더 어떤값들이 들어오는지 파악하기 쉽지 않을까라는 개인적인 생각이구요. 그리고 input에서 쓰는 속성들이 굉장히 많아서, 저는 주로 자주 쓰고 필수인 속성들은 props명으로 직접 받고 나머지 속성들도 들어오면 input 속성에 들어갈 수 있도록 rest 로 otherProps를 넣는 편이에요.
그리고 Input 컴포넌트를 쓰는 곳에서 예를 들어 className을 넘기지 않았다면 기본값이 들어가도록 기본값을 지정해 주기도 합니다.
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/95#discussion_r862421571)

### target.value 수정 No!

```
	target.value = target.value.replace(/[^\d]/g, "").replace(".", "");
};

const limitInputLength = (target) => {
	target.value = target.value.substring(0, maxLength);
};

const limitExceptUpperCase = (target) => {
	target.value = target.value.replace(/[^A-Z\s]*/g, "").replace(".", "");
```

```
state와 dispatch를 사용해서 상태를 업데이트 하고 변경된 값을 다시 반영해 주고 있는 React에 의해 값이 제어되는 형태이기 때문에 중간에 이렇게 값을 변경하는것 자체가 사이드 이펙트여서 그렇다고 생각이 들어요.
```

구체적으로 어떤 사이드 이펙트가....아! state 와 VirutalDOM과 RealDOM사이의 상태값 싱크가 안맞을 수도 있겠구나.  
예를들자면, RealDOM값은 4인데 state는 3인 경우?

[Comment Link](https://github.com/woowacourse/react-payments/pull/95#discussion_r862422008)

### 함수 재생성 No!
```
onKeyDown={(e) => {
    if (e.keyCode === BACKSPACE_KEY_CODE && e.target.value === "") {
      autoFocusBackward(e.target);
    }
  }}
```

```
onKeyDown 핸들러 함수는 CardNumberInput이 새로 렌더링 될 때마다 늘 또 새로 생성되지 않아도 될 것 같은 코드 내용의 함수네요. 새로운 상태값을 참조해야 하는게 아니라면 한번 선언된 함수를 계속 참조할 수 있게 최적화 시켜주는것도 좋을 것 같아요.
```
[Comment Link](https://github.com/woowacourse/react-payments/pull/95#discussion_r862422345)

## [동키콩](https://github.com/woowacourse/react-payments/pull/77)

### 파일구조
```
react-payments-step1
└─ src
  ├─ App.css
  ├─ App.js
  ├─ Portal.js
  ├─ components
  │  ├─ common
  │  │  ├─ Card
  │  │  │  ├─ index.jsx
  │  │  │  ├─ index.scss
  │  │  │  └─ index.stories.js
  │  │  ├─ Color
  │  │  │  ├─ index.jsx
  │  │  │  ├─ index.scss
  │  │  │  └─ index.stories.js
  │  │  ├─ Input
  │  │  │  ├─ index.jsx
  │  │  │  ├─ index.scss
  │  │  │  └─ index.stories.js
  │  │  ├─ InputContainer
  │  │  │  ├─ index.jsx
  │  │  │  ├─ index.scss
  │  │  │  └─ index.stories.js
  │  │  ├─ Modal
  │  │  │  ├─ index.jsx
  │  │  │  ├─ index.scss
  │  │  │  └─ index.stories.js
  │  │  ├─ NextButton
  │  │  │  ├─ index.jsx
  │  │  │  ├─ index.scss
  │  │  │  └─ index.stories.js
  │  │  └─ label
  │  │     ├─ index.jsx
  │  │     ├─ index.scss
  │  │     └─ index.stories.js
  │  └─ organisms
  │     ├─ CardColorPicker
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     ├─ CardNumberInput
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     ├─ CardPasswordInput
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     ├─ ConfirmAdd
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     ├─ ExpiredDateInput
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     ├─ OwnerNameInput
  │     │  ├─ index.jsx
  │     │  ├─ index.scss
  │     │  └─ index.stories.js
  │     └─ SecureCodeInput
  │        ├─ index.jsx
  │        ├─ index.scss
  │        └─ index.stories.js
  ├─ index.css
  ├─ index.js
  ├─ pages
  │  └─ CardAdd
  │     ├─ index.jsx
  │     ├─ index.scss
  │     └─ index.stories.js
  └─ util
      └─ input.js
```

### 코드의 분리

```
const validateCardNum = ({ cardNumber }) => {
  if (cardNumber.join("").length !== 16) {
    throw new Error("카드 번호를 16자리 모두 입력해주세요");
  }
};
const validateExpireDate = ({ expiredDate }) => {
  if (expiredDate[0] > 12) {
    throw new Error("월은 12월까지입니다.");
  }
  if (expiredDate.join("").length !== 4) {
    throw new Error("만료일을 정확히 입력해 주세요");
  }
};

const validateSecureCode = ({ secureCode }) => {
  if (secureCode.length < 3) {
    throw new Error("카드 뒷면의 보안코드 3자리를 입력해주세요");
  }
};
const validatePassword = ({ password }) => {
  if (password.join("").length !== 2) {
    throw new Error("비밀번호 앞 두자리를 입력해 주세요");
  }
};

const validateCardName = ({ cardName }) => {
  if (cardName === "") {
    throw new Error("카드 종류를 선택해주세요");
  }
};

const validateArray = [
  validateCardName,
  validateCardNum,
  validateExpireDate,
  validateSecureCode,
  validatePassword,
];
```

```
NextButton 컴포넌트 파일에서 validation 로직도 정의하고 들고있는데 다른 위치가 더 좋지 않나 생각됩니다.
NextButton을 재활용하기는 힘들것 같아요. 이 버튼을 만약 다른곳에서 사용한다고 했을때 무조건 onClick 로직은 특정 submit 및 validation을 하게됩니다. NextButton 컴포넌트 입장에서 click은 어떤 로직을 할지는 관심사가 아니죠.
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/77#discussion_r862335888)

### 불필요한 컴포넌트 분리

```
const Button = ({ className, children, onClick, style }) => {
  return (
    <button type="button" className={className} onClick={onClick} style={style}>
      {children}
    </button>
  );
};
```

```
모든게 외부에서 결정되는데 그냥 button 태그를 사용하는것과 다른것이 있나요??
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/77#discussion_r862338381)

### Portal
```
보통 toast나 modal은 페이지나 다른 컴포넌트위에서 독립적으로 동작합니다:) portal말고 다른 방법도 있지만 modal에서 portal을 많이 활용하는편이죠
```

[React Portal Documentation](https://ko.reactjs.org/docs/portals.html)
[Comment Link](https://github.com/woowacourse/react-payments/pull/77#discussion_r862341739)

## [유세지](https://github.com/woowacourse/react-payments/pull/81)
### 파일구조

```
react-payments-myorigin-step1
└─ src
   ├─ App.css
   ├─ App.jsx
   ├─ assets
   │  └─ cvc.png
   ├─ components
   │  ├─ cardRegister
   │  │  ├─ CVCHelperModal.jsx
   │  │  ├─ CVCInputForm.jsx
   │  │  ├─ CardExpireDateInputForm.jsx
   │  │  ├─ CardNumbersInputForm.jsx
   │  │  ├─ CardOwnerInputForm.jsx
   │  │  ├─ CardPasswordInputForm.jsx
   │  │  ├─ CardSelectModal.jsx
   │  │  └─ index.js
   │  └─ common
   │     ├─ Button.jsx
   │     ├─ Card.jsx
   │     ├─ Dot.jsx
   │     ├─ InputBasic.jsx
   │     ├─ InputBox.jsx
   │     ├─ Modal.jsx
   │     ├─ PageTitle.jsx
   │     ├─ TipButton.jsx
   │     ├─ index.js
   │     └─ styled.jsx
   ├─ constants
   │  └─ constants.js
   ├─ hooks
   │  └─ useModal.js
   ├─ index.css
   ├─ index.js
   ├─ pages
   │  └─ CardRegisterPage.jsx
```

### 배열 대신 객체로 리턴하라
```
	name && setModalName(name);
};

return [modalVisibleState, setModalState, modalName];
```  
```
확장성을 위해 배열보다는 객체 형태로 return하시는게 좋을 거에요!
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/81#discussion_r863616853)


### 파일 분리

```
const handleMonthInput = (e) => {
    if (isNaN(e.nativeEvent.data) || parseInt(e.target.value) > 12) {
      return;
    }

    if (e.target.value.length === 3) {
      e.target.value = parseInt(e.target.value);
    }

    if (e.target.value.length === 1) {
      e.target.value = '0' + e.target.value;
    }

    if (e.target.value === '0' || e.target.value === '00') {
      e.target.value = '00';
    }

    handleExpireDateInput((prev) => ({ ...prev, month: e.target.value }));
  };

  const handleYearInput = (e) => {
    if (isNaN(e.nativeEvent.data) || e.target.value.length > 2) {
      return;
    }

    handleExpireDateInput((prev) => ({ ...prev, year: e.target.value }));
  };
```

```
validation을 따로 함수로 만든다면 handleMonthInput의 로직이 좀 더 눈에 잘 들어올 것 같습니다!
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/81#discussion_r863614652)

## [후이](https://github.com/woowacourse/react-payments/pull/93)

### 파일구조

```
react-payments-step1-hui
└─ src
   ├─ App.css
   ├─ App.js
   ├─ assets
   │  └─ cvc.png
   ├─ components
   │  ├─ cardRegister
   │  │  ├─ CVCHelperModal.js
   │  │  ├─ CVCInput.js
   │  │  ├─ CardExpireDateInput.js
   │  │  ├─ CardNumbersInput.js
   │  │  ├─ CardOwnerInput.js
   │  │  ├─ CardPasswordInput.js
   │  │  ├─ CardPreview.js
   │  │  └─ CardSelectModal.js
   │  └─ common
   │     ├─ AutoFocusInputContainer.js
   │     ├─ Button.js
   │     ├─ Card.js
   │     ├─ Dot.js
   │     ├─ Modal.js
   │     ├─ ModalSelector.js
   │     ├─ PageTitle.js
   │     ├─ QuestionMark.js
   │     ├─ Shimmer.js
   │     └─ styled.js
   ├─ constants
   │  └─ card.js
   ├─ hooks
   │  └─ useModalSelector.js
   ├─ index.css
   ├─ index.js
   ├─ pages
   │  └─ CardRegisterPage.js
   ├─ reducer
   │  ├─ cardInfo.js
   │  └─ types.js
```

### 네이밍
```
<>
	<PageTitle>카드 추가</PageTitle>
	<CardPreview />
	<CardNumbersInputForm />
	<CardExpireDateInputForm />
	<CardOwnerInputForm />
	<CVCInputForm />
</>
```

CardPreview 좋다!

```
import styled from 'styled-components';

export const Button = ({ children, handleClick, disabled }) => {
```

```onClick이면 더 좋을듯하네요:)```

[Comment Link](https://github.com/woowacourse/react-payments/pull/93#discussion_r864724040)

## [자스민](https://github.com/woowacourse/react-payments/pull/82)

### 파일구조
```
react-payments-step1
└─ src
  ├─ App.css
  ├─ App.js
  ├─ App.test.js
  ├─ component
  │  ├─ Card
  │  │  ├─ card.component.jsx
  │  │  ├─ card.css
  │  │  └─ card.stories.jsx
  │  ├─ CardTypeSelector
  │  │  ├─ CardTypeSelector.css
  │  │  └─ CardTypeSelector.jsx
  │  ├─ ColorBox
  │  │  ├─ colorBox.component.jsx
  │  │  ├─ colorBox.css
  │  │  └─ colorBox.stories.jsx
  │  ├─ Dot
  │  │  ├─ dot.component.jsx
  │  │  ├─ dot.css
  │  │  └─ dot.stories.jsx
  │  ├─ Form
  │  │  ├─ form.component.jsx
  │  │  ├─ form.css
  │  │  └─ form.stories.jsx
  │  ├─ Header
  │  │  ├─ Header.component.jsx
  │  │  ├─ Header.css
  │  │  └─ Header.stories.jsx
  │  ├─ HelpBox
  │  │  ├─ helpBox.component.jsx
  │  │  ├─ helpBox.css
  │  │  └─ helpBox.stories.jsx
  │  ├─ Input
  │  │  ├─ input.component.jsx
  │  │  ├─ input.css
  │  │  └─ input.stories.jsx
  │  ├─ LinkButton
  │  │  ├─ linkButton.component.jsx
  │  │  ├─ linkButton.css
  │  │  └─ linkButton.stories.jsx
  │  ├─ MessageBlock
  │  │  ├─ messageBlock.component.jsx
  │  │  ├─ messageBlock.css
  │  │  └─ messageBlock.stories.jsx
  │  ├─ Modal
  │  │  ├─ modal.component.jsx
  │  │  ├─ modal.css
  │  │  └─ modal.stories.jsx
  │  ├─ PageTitle
  │  │  ├─ pageTitle.component.jsx
  │  │  ├─ pageTitle.css
  │  │  └─ pageTitle.stories.jsx
  │  └─ VirtualKeyboard
  │     ├─ keyboard.component.jsx
  │     ├─ keyboard.css
  │     └─ keyboard.stories.jsx
  ├─ constants
  │  └─ index.js
  ├─ index.css
  ├─ index.js
  ├─ pages
  │  └─ CardAddPage
  │     ├─ CardAddPage.component.jsx
  │     ├─ CardAddPage.css
  └─ util
      ├─ focus.js
      └─ validator.js
```

### 컴포넌트 분리

```
페이지에 사용하는 컴포넌트와 공용 컴포넌트를 구분해보는건 어떨까요? 페이지에 종속될수도 있는 컴포넌트가 공용 컴포넌트에 위치하다보니 헷갈리는 면이 있었어요. 재사용을 위해 어떻게 유연하게 컴포넌트를 가져갈 수 있을지 생각해보면 좋을거같아요. 어떻게 폴더 구조를 가져갈지는 자스민이 판단해봅시다! (개선을 해보신다면 코멘트를 단 컴포넌트 이외에도 페이지에 종속된 컴포넌트가 있을텐데 점검해봅시다!)
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/82#pullrequestreview-958480375)

```
import ColorBox from "../ColorBox/colorBox.component";
import "./modal.css";

const Modal = ({ toggleModal, onClickCardType, currentCardType }) => {
```
[Comment Link](https://github.com/woowacourse/react-payments/pull/82#discussion_r862343829)

### CSS 의존
```
.card-number > div {
  background: #616161;
}
```

```
케이스를 css에 의존해서 바꿔주는게 좋은 방식일지 모르겠어요.
현재는 2가지 케이스밖에 없어 문제가 없겠지만 컴포넌트 관점에서 생각해본다면 유연한 설계는 아닐 수 있겠다고 생각이 들었어요.
dot 컴포넌트 자체에서 색상을 변경하는게 더 유연하다고 생각합니다! 별도의 css를 정의 할 필요도 없구요 🙂
```
[Comment Link](https://github.com/woowacourse/react-payments/pull/82#discussion_r862345725)

### children prop의 활용

#### Bad
```
<LinkButton {...props} />
<PageTitle {...props} />
```

#### Good
```
return (
	<Header>
	  <PageTitle title='카드 등록' />
	</Header>
)

// or
return (
	<Header>
	  <LinkButton />
	  <PageTitle title='카드 생성' />
	</Header>
)
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/82#discussion_r862351196)

### Toggle Reducer
#### Bad
```
const [canShowModal, setCanShowModal] = useState(false);
const toggleModal = () => {
	setCanShowModal((prevCanShowModal) => !prevCanShowModal);
};
```

#### Good
```
const [canShowModal, toggleModal] = useReducer((isShowModal) => !isShowModal, false)
return [canShowModal, toggleModal]
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/82#discussion_r862351581)

## [우연](https://github.com/woowacourse/react-payments/pull/105)

### 파일구조
```
react-payments-step1
└─ src
  ├─ App.css
  ├─ App.js
  ├─ App.test.js
  ├─ component
  │  ├─ Card
  │  │  ├─ card.component.jsx
  │  │  ├─ card.css
  │  │  └─ card.stories.jsx
  │  ├─ CardTypeSelector
  │  │  ├─ CardTypeSelector.css
  │  │  └─ CardTypeSelector.jsx
  │  ├─ ColorBox
  │  │  ├─ colorBox.component.jsx
  │  │  ├─ colorBox.css
  │  │  └─ colorBox.stories.jsx
  │  ├─ Dot
  │  │  ├─ dot.component.jsx
  │  │  ├─ dot.css
  │  │  └─ dot.stories.jsx
  │  ├─ Form
  │  │  ├─ form.component.jsx
  │  │  ├─ form.css
  │  │  └─ form.stories.jsx
  │  ├─ Header
  │  │  ├─ Header.component.jsx
  │  │  ├─ Header.css
  │  │  └─ Header.stories.jsx
  │  ├─ HelpBox
  │  │  ├─ helpBox.component.jsx
  │  │  ├─ helpBox.css
  │  │  └─ helpBox.stories.jsx
  │  ├─ Input
  │  │  ├─ input.component.jsx
  │  │  ├─ input.css
  │  │  └─ input.stories.jsx
  │  ├─ LinkButton
  │  │  ├─ linkButton.component.jsx
  │  │  ├─ linkButton.css
  │  │  └─ linkButton.stories.jsx
  │  ├─ MessageBlock
  │  │  ├─ messageBlock.component.jsx
  │  │  ├─ messageBlock.css
  │  │  └─ messageBlock.stories.jsx
  │  ├─ Modal
  │  │  ├─ modal.component.jsx
  │  │  ├─ modal.css
  │  │  └─ modal.stories.jsx
  │  ├─ PageTitle
  │  │  ├─ pageTitle.component.jsx
  │  │  ├─ pageTitle.css
  │  │  └─ pageTitle.stories.jsx
  │  └─ VirtualKeyboard
  │     ├─ keyboard.component.jsx
  │     ├─ keyboard.css
  │     └─ keyboard.stories.jsx
  ├─ constants
  │  └─ index.js
  ├─ index.css
  ├─ index.js
  ├─ pages
  │  └─ CardAddPage
  │     ├─ CardAddPage.component.jsx
  │     ├─ CardAddPage.css
  │     └─ CardAddPage.stories.jsx
  ├─ reportWebVitals.js
  ├─ setupTests.js
  └─ util
      ├─ focus.js
      └─ validator.js
```

### 컴포넌트에 의존적인 커스텀 훅
```
일단 적극적으로 활용하신 점 칭찬합니다.
하지만 다음부터는 의식적으로 분리하도록 노력해보세요 :)
과도한 훅 분리, 유틸인지 훅인지 헷갈리는 녀석이 제법 보입니다

추가적으로 반환을 무조건 배열로하니 유연하지 못한 경우도 있어요.
그러다보니 커스텀 훅으로 분리는 했지만 결국 특정 컴포넌트에 의존적인 훅이 탄생해버리는 경우가 종종 보이네요.

결국 하나의 컴포넌트를 구성할때 아래와 같은 구성이 한 세트로 움직이고 있습니다.

- AA.component.jsx
- AA.css
- AA.stories.jsx
- useAA.jsx
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/105#pullrequestreview-958697168)

```
- 전반적으로 커스텀 훅을 잘 이용하신 것 같아서 좋았습니다 :) 굿굿
- 그런데, 커스텀 훅으로 너무 빼다보니, 이 커스텀 훅은 훅보단 컴포넌트 단위로 들어가는게 나을수도 있었겠다 하는 부분이 보였어요 :) 대표적으로 카드 번호를 입력하는 부분인데요! 요 부분은 범용적으로 사용되는 범위가 컴포넌트 자체의 폼을 가져다 쓸 수 있기 때문에, 컴포넌트 단위로 관리가 될 수 있을 것으로 보입니다!
```

[Comment Link](https://github.com/woowacourse/react-payments/pull/105#pullrequestreview-958550505)

### 네이밍

```
export const checkNextFocus = ({ target, value, maxLength, nextElement }) => {
  if (
    value[target.name].length < target.value.length &&
    target.value.length === maxLength &&
    nextElement
  ) {
    nextElement.focus();
  }
};

export const checkPrevFocus = ({ target, value, prevElement }) => {
  if (
    value[target.name].length > target.value.length &&
    target.value.length === 0 &&
    prevElement
  ) {
    prevElement.focus();
  }
};
```

```
단순히 체크만하는 게 아닌 걸로 보이네요.
또한 UI의 포커스 행위에 관여도 하고 있고요
```
[Comment Link](https://github.com/woowacourse/react-payments/pull/105#discussion_r862593139)


```
한 페이지에 폼이 굉장히 많은데요
자세히 보면 폼이 아닌 Input 하나하나로 보입니다.
Input이 아닌 Form으로 명명하신 이유가 있으신가요?
```
[Comment Link](https://github.com/woowacourse/react-payments/pull/105#discussion_r862593650)
