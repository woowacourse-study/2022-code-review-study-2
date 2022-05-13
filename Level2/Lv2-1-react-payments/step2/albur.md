# Leve2-1 React-payments Step1 - 앨버

- 분석 담당 코드

  - [#143](https://github.com/woowacourse/react-payments/pull/143)
  - [#112](https://github.com/woowacourse/react-payments/pull/112)
  - [#120](https://github.com/woowacourse/react-payments/pull/120)
  - [#124](https://github.com/woowacourse/react-payments/pull/124)
  - [#130](https://github.com/woowacourse/react-payments/pull/130)
  - [#138](https://github.com/woowacourse/react-payments/pull/138)

## 다른 크루들 코드 분석

#### 컴포넌트를 어떻게 나눴을까?

(앨버)

```
📦react-payments
┣ 📂.github
┃ ┗ 📂workflows
┃ ┃ ┣ 📜main.yml
┃ ┃ ┗ 📜storybook.yml
┣ 📂.storybook
┃ ┣ 📜main.js
┃ ┗ 📜preview.js
┣ 📂public
┃ ┗ 📜index.html
┣ 📂src
┃ ┣ 📂assets
┃ ┃ ┣ 📜arrow.svg
┃ ┃ ┣ 📜loading.png
┃ ┃ ┗ 📜plus.svg
┃ ┣ 📂components
┃ ┃ ┣ 📂common
┃ ┃ ┃ ┣ 📜Button.jsx
┃ ┃ ┃ ┣ 📜Card.jsx
┃ ┃ ┃ ┣ 📜Header.jsx
┃ ┃ ┃ ┣ 📜Input.jsx
┃ ┃ ┃ ┗ 📜ModalPortal.jsx
┃ ┃ ┣ 📜CardForm.jsx
┃ ┃ ┣ 📜CardKindButton.jsx
┃ ┃ ┣ 📜CardPickModal.jsx
┃ ┃ ┣ 📜CVCTooltip.jsx
┃ ┃ ┣ 📜EmptyCard.jsx
┃ ┃ ┗ 📜index.js
┃ ┣ 📂constants
┃ ┃ ┣ 📜color.js
┃ ┃ ┗ 📜index.js
┃ ┣ 📂contexts
┃ ┃ ┗ 📜CardContext.jsx
┃ ┣ 📂hooks
┃ ┃ ┣ 📜index.js
┃ ┃ ┣ 📜useAddCard.jsx
┃ ┃ ┣ 📜useCardNumber.jsx
┃ ┃ ┣ 📜useCardOwnerName.jsx
┃ ┃ ┣ 📜useCardPassword.jsx
┃ ┃ ┣ 📜useCVC.jsx
┃ ┃ ┣ 📜useGetCardList.jsx
┃ ┃ ┣ 📜useNavigateTo.jsx
┃ ┃ ┗ 📜useValidDate.jsx
┃ ┣ 📂pages
┃ ┃ ┣ 📜AddCard.jsx
┃ ┃ ┣ 📜AddCardComplete.jsx
┃ ┃ ┣ 📜CardList.jsx
┃ ┃ ┗ 📜index.js
┃ ┣ 📂stories
┃ ┃ ┣ 📜AddCardCompletePage.stories.jsx
┃ ┃ ┣ 📜AddCardPage.stories.jsx
┃ ┃ ┣ 📜Button.stories.jsx
┃ ┃ ┣ 📜Card.stories.jsx
┃ ┃ ┣ 📜CardListPage.stories.jsx
┃ ┃ ┣ 📜Input.stories.jsx
┃ ┃ ┗ 📜mixedComponents.stories.jsx
┃ ┣ 📂utils
┃ ┃ ┣ 📜fetcher.js
┃ ┃ ┣ 📜maskNumbers.js
┃ ┃ ┗ 📜validator.js
┃ ┣ 📜App.jsx
┃ ┣ 📜GlobalStyle.js
┃ ┗ 📜index.js
┣ 📜.env
┣ 📜.eslintrc.js
┣ 📜.gitignore
┣ 📜.prettierrc.js
┣ 📜jsconfig.json
┣ 📜package-lock.json
┣ 📜package.json
┣ 📜README.md
┗ 📜REQUIREMENTS.md
```

(하리)

```
📦react-payments
┣ 📂.storybook
┃ ┣ 📜main.js
┃ ┗ 📜preview.js
┣ 📂public
┃ ┗ 📜index.html
┣ 📂src
┃ ┣ 📂assets
┃ ┃ ┗ 📜arrow.svg
┃ ┣ 📂components
┃ ┃ ┣ 📂Button
┃ ┃ ┃ ┗ 📜index.jsx
┃ ┃ ┣ 📂Card
┃ ┃ ┃ ┣ 📜Basic.jsx
┃ ┃ ┃ ┣ 📜DisplayCard.jsx
┃ ┃ ┃ ┗ 📜index.jsx
┃ ┃ ┣ 📂complex
┃ ┃ ┃ ┣ 📜CardCVC.jsx
┃ ┃ ┃ ┣ 📜CardNumberInput.jsx
┃ ┃ ┃ ┣ 📜CardOwnerNameInput.jsx
┃ ┃ ┃ ┣ 📜CardPasswordInput.jsx
┃ ┃ ┃ ┣ 📜CardValidDateInput.jsx
┃ ┃ ┃ ┗ 📜index.jsx
┃ ┃ ┣ 📂Container
┃ ┃ ┃ ┣ 📜AppContainer.jsx
┃ ┃ ┃ ┣ 📜index.jsx
┃ ┃ ┃ ┗ 📜InputContainer.jsx
┃ ┃ ┣ 📂Input
┃ ┃ ┃ ┣ 📜Basic.jsx
┃ ┃ ┃ ┣ 📜index.jsx
┃ ┃ ┃ ┗ 📜Underlined.jsx
┃ ┃ ┣ 📂Modal
┃ ┃ ┃ ┗ 📜index.jsx
┃ ┃ ┗ 📜index.jsx
┃ ┣ 📂constants
┃ ┃ ┗ 📜index.js
┃ ┣ 📂contexts
┃ ┃ ┗ 📜index.js
┃ ┣ 📂hooks
┃ ┃ ┣ 📜index.jsx
┃ ┃ ┣ 📜useCardNumber.jsx
┃ ┃ ┣ 📜useCardOwnerName.jsx
┃ ┃ ┣ 📜useCardPassword.jsx
┃ ┃ ┣ 📜useCVC.jsx
┃ ┃ ┣ 📜useInput.jsx
┃ ┃ ┗ 📜useModal.jsx
┃ ┣ 📂pages
┃ ┃ ┣ 📂AddCompletePage
┃ ┃ ┃ ┣ 📜Fail.jsx
┃ ┃ ┃ ┣ 📜index.jsx
┃ ┃ ┃ ┗ 📜Success.jsx
┃ ┃ ┣ 📂AddPage
┃ ┃ ┃ ┣ 📜CardInputs.jsx
┃ ┃ ┃ ┣ 📜CompanyModal.jsx
┃ ┃ ┃ ┣ 📜index.jsx
┃ ┃ ┃ ┗ 📜styled.jsx
┃ ┃ ┣ 📂CardListPage
┃ ┃ ┃ ┣ 📜Cards.jsx
┃ ┃ ┃ ┗ 📜index.jsx
┃ ┃ ┣ 📂NotFound
┃ ┃ ┃ ┗ 📜index.jsx
┃ ┃ ┗ 📜index.jsx
┃ ┣ 📂reducers
┃ ┃ ┗ 📜index.js
┃ ┣ 📂router
┃ ┃ ┣ 📜AddPageRouter.jsx
┃ ┃ ┗ 📜index.jsx
┃ ┣ 📂stories
┃ ┃ ┣ 📂pages
┃ ┃ ┃ ┣ 📜AddCompletePage.stories.jsx
┃ ┃ ┃ ┣ 📜AddPage.stories.jsx
┃ ┃ ┃ ┗ 📜CardListPage.stories.jsx
┃ ┃ ┣ 📜App.stories.jsx
┃ ┃ ┣ 📜Button.stories.jsx
┃ ┃ ┣ 📜Card.stories.jsx
┃ ┃ ┣ 📜Input.stories.jsx
┃ ┃ ┗ 📜mixedComponents.stories.jsx
┃ ┣ 📂utils
┃ ┃ ┣ 📜event.js
┃ ┃ ┣ 📜processCard.js
┃ ┃ ┣ 📜regExp.js
┃ ┃ ┗ 📜validator.js
┃ ┣ 📜App.jsx
┃ ┣ 📜index.css
┃ ┗ 📜index.js
┣ 📜.eslintrc.js
┣ 📜.gitignore
┣ 📜.prettierrc.js
┣ 📜package-lock.json
┣ 📜package.json
┣ 📜README.md
┗ 📜REQUIREMENTS.md
```

(밧드)

```
📦react-payments
 ┣ 📂.storybook
 ┃ ┣ 📜main.js
 ┃ ┗ 📜preview.js
 ┣ 📂public
 ┃ ┣ 📜favicon.ico
 ┃ ┣ 📜index.html
 ┃ ┣ 📜logo192.png
 ┃ ┣ 📜logo512.png
 ┃ ┗ 📜manifest.json
 ┣ 📂src
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📂Atoms
 ┃ ┃ ┃ ┣ 📂CardDeleteButton
 ┃ ┃ ┃ ┃ ┣ 📜CardDeleteButton.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂InfoLabel
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜InfoLabel.stories.jsx
 ┃ ┃ ┃ ┣ 📂Input
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜Input.stories.jsx
 ┃ ┃ ┃ ┣ 📂InputLabel
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂InputWrapper
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂LabeledInput
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┗ 📂SubmitButton
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜SubmitButton.stories.jsx
 ┃ ┃ ┣ 📂Modules
 ┃ ┃ ┃ ┣ 📂AddCard
 ┃ ┃ ┃ ┃ ┣ 📜AddCard.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂Card
 ┃ ┃ ┃ ┃ ┣ 📜Card.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂CardNameInput
 ┃ ┃ ┃ ┃ ┣ 📜CardNameInput.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂CardNumberInput
 ┃ ┃ ┃ ┃ ┣ 📜CardNumberInput.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂CardOwnerInput
 ┃ ┃ ┃ ┃ ┣ 📜CardOwnerInput.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂ExpiredDateInput
 ┃ ┃ ┃ ┃ ┣ 📜ExpiredDateInput.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂Head
 ┃ ┃ ┃ ┃ ┣ 📜Head.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂PasswordInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜PasswordInput.stories.jsx
 ┃ ┃ ┃ ┗ 📂SecurityNumberInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜SecurityNumberInput.stories.jsx
 ┃ ┃ ┗ 📂Templates
 ┃ ┃ ┃ ┣ 📂CardAddForm
 ┃ ┃ ┃ ┃ ┣ 📜CardAddForm.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┗ 📂CardNameForm
 ┃ ┃ ┃ ┃ ┣ 📜CardNameForm.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┣ 📂constant
 ┃ ┃ ┣ 📜index.js
 ┃ ┃ ┣ 📜inputNames.js
 ┃ ┃ ┣ 📜Link.js
 ┃ ┃ ┣ 📜mark.js
 ┃ ┃ ┣ 📜message.js
 ┃ ┃ ┗ 📜regularExpression.js
 ┃ ┣ 📂containers
 ┃ ┃ ┣ 📂Button
 ┃ ┃ ┃ ┗ 📜CardDeleteButtonContainer.jsx
 ┃ ┃ ┣ 📂Card
 ┃ ┃ ┃ ┗ 📜CardContainer.jsx
 ┃ ┃ ┣ 📂Form
 ┃ ┃ ┃ ┣ 📜CardAddFormContainer.jsx
 ┃ ┃ ┃ ┗ 📜CardNameFormContainer.jsx
 ┃ ┃ ┗ 📂Input
 ┃ ┃ ┃ ┣ 📜CardNameInputContainer.jsx
 ┃ ┃ ┃ ┣ 📜CardNumberInputContainer.jsx
 ┃ ┃ ┃ ┣ 📜CardOwnerInputContainer.jsx
 ┃ ┃ ┃ ┣ 📜ExpiredDateInputContainer.jsx
 ┃ ┃ ┃ ┣ 📜PasswordInputContainer.jsx
 ┃ ┃ ┃ ┗ 📜SecurityNumberInputContainer.jsx
 ┃ ┣ 📂context
 ┃ ┃ ┗ 📜CardContext.jsx
 ┃ ┣ 📂hooks
 ┃ ┃ ┣ 📜useFocus.js
 ┃ ┃ ┗ 📜useSomeInput.js
 ┃ ┣ 📂Pages
 ┃ ┃ ┣ 📂CardAddPage
 ┃ ┃ ┃ ┣ 📜CardAddPage.stories.jsx
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┣ 📂CardCompletePage
 ┃ ┃ ┃ ┣ 📜CardCompletePage.stories.jsx
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┗ 📂CardListPage
 ┃ ┃ ┃ ┣ 📜CardListPage.stories.jsx
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┣ 📂Reducer
 ┃ ┃ ┣ 📜CardReducer.js
 ┃ ┃ ┗ 📜InputtedInfoReducer.js
 ┃ ┣ 📂validation
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📜App.css
 ┃ ┣ 📜App.js
 ┃ ┣ 📜index.css
 ┃ ┗ 📜index.js
 ┣ 📜.eslintrc.js
 ┣ 📜.gitignore
 ┣ 📜.prettierrc.json
 ┣ 📜jsconfig.json
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┣ 📜README.md
 ┣ 📜REQUIREMENTS.md
 ┗ 📜yarn.lock

```

(코이)

```
📦react-payments
 ┣ 📂.storybook
 ┃ ┣ 📜main.js
 ┃ ┗ 📜preview.js
 ┣ 📂public
 ┃ ┣ 📜favicon.ico
 ┃ ┣ 📜index.html
 ┃ ┣ 📜logo192.png
 ┃ ┣ 📜logo512.png
 ┃ ┗ 📜manifest.json
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┃ ┣ 📜arrow.svg
 ┃ ┃ ┗ 📜question.svg
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📂Button
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂Card
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂CardEditor
 ┃ ┃ ┃ ┣ 📂CardCVCInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂CardDueDateInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜useCardDueDate.js
 ┃ ┃ ┃ ┣ 📂CardNumberInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜useCardNumber.js
 ┃ ┃ ┃ ┣ 📂CardOwnerInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂CardPasswordInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┃ ┣ 📜style.js
 ┃ ┃ ┃ ┃ ┗ 📜useCardPassword.js
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┗ 📜index.stories.jsx
 ┃ ┃ ┣ 📂ColorBox
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂Header
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂Input
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂InputBox
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂Modal
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┗ 📂Palette
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┣ 📂constant
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂context
 ┃ ┃ ┗ 📜CardListProvider.jsx
 ┃ ┣ 📂hooks
 ┃ ┃ ┣ 📜useInput.js
 ┃ ┃ ┗ 📜useModal.js
 ┃ ┣ 📂pages
 ┃ ┃ ┣ 📂Edit
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┣ 📂Finish
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┣ 📂Home
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┣ 📂New
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┗ 📜index.stories.jsx
 ┃ ┃ ┣ 📂NotFound
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┗ 📜style.js
 ┃ ┣ 📂theme
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂utils
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂validation
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📜App.jsx
 ┃ ┗ 📜index.js
 ┣ 📜.gitignore
 ┣ 📜jsconfig.json
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┣ 📜README.md
 ┣ 📜REQUIREMENTS.md
 ┗ 📜yarn.lock
```

(도리)

```
📦react-payments
 ┣ 📂.storybook
 ┃ ┣ 📜main.js
 ┃ ┗ 📜preview.js
 ┣ 📂public
 ┃ ┣ 📜favicon.ico
 ┃ ┣ 📜index.html
 ┃ ┣ 📜logo192.png
 ┃ ┣ 📜logo512.png
 ┃ ┗ 📜manifest.json
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┃ ┣ 📜addCard.svg
 ┃ ┃ ┣ 📜arrow.svg
 ┃ ┃ ┗ 📜questionMark.svg
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📂AddCard
 ┃ ┃ ┃ ┣ 📂CardNumberField
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.stories.jsx
 ┃ ┃ ┃ ┣ 📂CVCField
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.stories.jsx
 ┃ ┃ ┃ ┣ 📂DueDateField
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.stories.jsx
 ┃ ┃ ┃ ┣ 📂OwnerField
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📂PasswordField
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┗ 📂common
 ┃ ┃ ┃ ┣ 📂Button
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂Card
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂CardCompany
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂Field
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂Header
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂Input
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┗ 📂Modal
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┣ 📂constant
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂context
 ┃ ┃ ┣ 📜cardInfo-context.jsx
 ┃ ┃ ┣ 📜constant.jsx
 ┃ ┃ ┗ 📜reduce.jsx
 ┃ ┣ 📂hooks
 ┃ ┃ ┣ 📜useAutoFocus.jsx
 ┃ ┃ ┗ 📜useLocalStorage.jsx
 ┃ ┣ 📂pages
 ┃ ┃ ┣ 📂AddPage
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┗ 📜index.stories.jsx
 ┃ ┃ ┣ 📂CardListPage
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂NickNamePage
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┣ 📜index.stories.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂NotFoundPage
 ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┗ 📜style.js
 ┃ ┣ 📂theme
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂validation
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📜App.jsx
 ┃ ┣ 📜index.css
 ┃ ┗ 📜index.js
 ┣ 📜.gitignore
 ┣ 📜.prettierrc
 ┣ 📜jsconfig.json
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┣ 📜README.md
 ┣ 📜REQUIREMENTS.md
 ┗ 📜yarn.lock
```

(빅터)

```
📦react-payments
 ┣ 📂.storybook
 ┃ ┣ 📜main.js
 ┃ ┣ 📜preview.js
 ┃ ┗ 📜storybook.css
 ┣ 📂public
 ┃ ┣ 📜favicon.ico
 ┃ ┣ 📜index.html
 ┃ ┣ 📜logo192.png
 ┃ ┣ 📜logo512.png
 ┃ ┗ 📜manifest.json
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┃ ┗ 📂images
 ┃ ┃ ┃ ┗ 📜backButtonArrow.svg
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📂Atoms
 ┃ ┃ ┃ ┣ 📂Button
 ┃ ┃ ┃ ┃ ┣ 📜Button.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.js
 ┃ ┃ ┃ ┣ 📂CardCompanyButton
 ┃ ┃ ┃ ┃ ┣ 📜CardCompanyButton.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂Input
 ┃ ┃ ┃ ┃ ┣ 📜index.js
 ┃ ┃ ┃ ┃ ┗ 📜input.stories.jsx
 ┃ ┃ ┃ ┣ 📂InputLabel
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┗ 📂Tooltip
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜Tooltip.stories.jsx
 ┃ ┃ ┣ 📂Molecules
 ┃ ┃ ┃ ┣ 📂Card
 ┃ ┃ ┃ ┃ ┣ 📜Card.stories.jsx
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┃ ┣ 📂CardCompanySelector
 ┃ ┃ ┃ ┃ ┣ 📜CardCompanySelector.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂CardNumbersInput
 ┃ ┃ ┃ ┃ ┣ 📜CardNumbersInput.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂ExpiredDateInput
 ┃ ┃ ┃ ┃ ┣ 📜ExpiredDataInput.stories.jsx
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┣ 📂OwnerNameInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜OwnerNameInput.stories.jsx
 ┃ ┃ ┃ ┣ 📂PasswordInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜PasswordInput.stories.jsx
 ┃ ┃ ┃ ┗ 📂SecurityNumberInput
 ┃ ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┃ ┗ 📜SecurityNumberInput.stories.jsx
 ┃ ┃ ┗ 📂Templates
 ┃ ┃ ┃ ┣ 📂Head
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┃ ┃ ┗ 📂ModalPortal
 ┃ ┃ ┃ ┃ ┗ 📜index.jsx
 ┃ ┣ 📂constant
 ┃ ┃ ┣ 📜index.js
 ┃ ┃ ┣ 📜mark.js
 ┃ ┃ ┣ 📜message.js
 ┃ ┃ ┣ 📜path.js
 ┃ ┃ ┣ 📜regularExpression.js
 ┃ ┃ ┗ 📜selector.js
 ┃ ┣ 📂context
 ┃ ┃ ┗ 📜cardList.js
 ┃ ┣ 📂hooks
 ┃ ┃ ┣ 📜useCardCompany.js
 ┃ ┃ ┣ 📜useCardNumbers.js
 ┃ ┃ ┣ 📜useExpiredDate.js
 ┃ ┃ ┣ 📜useModal.js
 ┃ ┃ ┣ 📜useOwnerName.js
 ┃ ┃ ┣ 📜usePassword.js
 ┃ ┃ ┗ 📜useSecurityNumber.js
 ┃ ┣ 📂pages
 ┃ ┃ ┣ 📂CardAddCompletionPage
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┣ 📂CardAddPage
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┃ ┗ 📂CardListPage
 ┃ ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┃ ┗ 📜style.js
 ┃ ┣ 📂validation
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📜App.jsx
 ┃ ┣ 📜index.js
 ┃ ┗ 📜style.js
 ┣ 📜.eslintrc.js
 ┣ 📜.gitignore
 ┣ 📜.prettierrc.json
 ┣ 📜jsconfig.json
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┣ 📜README.md
 ┗ 📜REQUIREMENTS.md
```

#### 재사용 컴포넌트는 어느 정도까지의 확장성을 가지고 있을까?

## 피드백 정리

#### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)

<br>

- [[#73](https://github.com/woowacourse/react-payments/pull/143#discussion_r869885305) - 공통 컴포넌트의 규격]

  - 공통 컴포넌트인데 규격이 너무 복잡해져 가는 것 같네요
    공통에서는 제외하고 반복되는 규격이 있다면 해당 컴포넌트를 wrapping해서 구체화 된 컴포넌트로 만들어 가는 방식으로 개선해 보면 어떨까요?

  - `discussion`에 코드 첨부해 놓았습니다. 이후, discussion에서 이야기를 해보면 좋을 것 같습니다.

<br>

- [[#112](https://github.com/woowacourse/react-payments/pull/112#discussion_r867441635) - 의식적인 UI/UX 생각]

  - 화살표 버튼을 클릭했을 때, history상 이전페이지를 보여주는게 맞나요? 아니면 /add으로 보내는게 맞나요?
    페이먼츠 요구사항에는 정확하게 안나와있는 것 같아서 어떤 방법이 ui상 좋은지 고민해보셔도 좋을 것 같습니다!

  - figma를 그대로 옮기는 것이 아니라 의식적으로 사용자를 생각해서 개발을 하면 좋을 것 같다!

<br>

- [[#112](https://github.com/woowacourse/react-payments/pull/112#discussion_r867441748) - 의식적인 UI/UX 생각2]

  - UX/UI상 /react-payments/{임의 path}값이 들어왔을 때, 404페이지등 예외처리가 되면 더 좋을것 같습니다.

<br>

- [[#120](https://github.com/woowacourse/react-payments/pull/120#pullrequestreview-965455520) - 컴포넌트 분리에 대한 생각]

  - 컴포넌트를 분리해서 중간에 다른 컴포넌트를 두거나 hook을 만들거나 이런 과정들이 결국 Depth를 늘리는거죠?
    설계에서 Depth를 늘리는 건 유연함을 얻는 대신 구조의 복잡도가 올라간다고 생각합니다.
    (만능 설계란 없고 트레이드 오프라는 것을 염두하셔야 됩니다)

  응집도 높은 로직들을 한 곳에 짰는데 변경 사항도 없고 읽기도 좋다? 그럼 베스트입니다.

  그런데 특정 요구 사항이 변경이 잦고 앞으로도 변경이 예상된다?
  -> 분리를 고려합니다. (잘 분리할 수 있도록 다양한 패턴이나 구조를 학습하는 겁니다.)
  공통적인 부분을 추상화해서 추출해야 유연한 설계가 됩니다.
  (개발하는 서비스 & 도메인에 대한 이해가 필요)

  유연하게 설계하려면 복잡도가 올라가는 만큼 파악하기 쉽지 않습니다.
  따라서 의도 전달을 최대한 돕기 위해 네이밍이 더 중요해집니다.

<br>

- [[#138](https://github.com/woowacourse/react-payments/pull/138#discussion_r867642393) - path 이름]

  route path 는 되도록이면 한 단어만 사용하는게 좋습니다! cardAddCompletion 의 경우에는 세 단어가 들어갔죠?
  보통은 도메인을 앞으로 빼주고 뒤에 crud 를 나타내고는 합니다.

  현재
  / : 카드리스트 페이지
  /cardAdd: 카드 추가 페이지
  /cardAddCompletion: 카드 추가 완료 페이지

  제안
  /cards : 카드 리스트 페이지
  /cards/:id : 각 카드의 상세 페이지
  /cards/new, /cards/create ... 중 하나 : 카드 생성 페이지
  /cards/result, /cards/complete ... 중 하나 : 카드 생성 완료 페이지
