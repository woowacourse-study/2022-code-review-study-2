## π― Level-1 lotto Step1(114, 105, 95, 94, 93, 98, 88, 91) - μ

- λΆμ λ΄λΉ μ½λ

  - [#114](https://github.com/woowacourse/javascript-lotto/pull/114) μ
  - [#105](https://github.com/woowacourse/javascript-lotto/pull/105) μ½μ΄

  - [#95](https://github.com/woowacourse/javascript-lotto/pull/95) λμΈ
  - [#94](https://github.com/woowacourse/javascript-lotto/pull/94) λΉλ

  - [#93](https://github.com/woowacourse/javascript-lotto/pull/93) νμ΄
  - [#98](https://github.com/woowacourse/javascript-lotto/pull/98) μ½€νΌ

  - [#88](https://github.com/woowacourse/javascript-lotto/pull/88) λΈλ§
  - [#91](https://github.com/woowacourse/javascript-lotto/pull/91) νν

## π μν€νμ² λΆμ
[#114 μ](https://github.com/woowacourse/javascript-lotto/pull/114)
- μ²μ μ μΆν λ΄μ©
  - controller
    1. μ΄λ²€νΈλ₯Ό λ°λλ€
    2. μ ν¨μ± κ²μ¬
    3. λͺ¨λΈμμ λ‘λ λ²νΈ μμ±
    4. λ·°μμ λλλ§ λ©μλ νΈμΆ
  - model
    - λ‘λ λ²νΈ μμ±
    - λ‘λ λ²νΈ λ¦¬μ€νΈ κ΄λ¦¬
  - view 
    - attribute μμ± μ μ΄ 
    - λλλ§

μ΄μ²λΌ μ»¨νΈλ‘€λ¬κ° μΌμ λ€νκ³  μλ€. <br>
μ΄λ κ²λλ©΄ μ»¨νΈλ‘€λ¬κ° λ·°μκ² μ κ·Ήμ μΌλ‘ κ°μμ νκ² λλ―λ‘ μ΄λ²€νΈ μ²λ¦¬λ view κ° ν΄μΌ νλ κ²μ΄ λ§λ€!! <br>
κ·ΈλΌ μ»¨νΈλ‘€λ¬λ μ΄λ€ λ©μλλ₯Ό λΆλ¦¬ ν΄μΌ νλκ°μ λν μ΄λ €μμ΄ μλ€. μ΅μ§λ‘ μ»¨νΈλ‘€λ¬ νν λ©μλλ₯Ό λ§λλ λλμ΄λΌ μΌλ¨ λ·°μ λͺ¨λΈλ‘λ§ κ΅¬νμ νκ³  λ μκ°ν΄λ³Όλ €κ³  νλ€

## β νΌλλ°± μ λ¦¬

- [μ­ν  λΆλ¦¬](https://github.com/woowacourse/javascript-lotto/pull/114#discussion_r814525324)
  - μλ ν°λ₯Ό μμλ‘ λ΄λ κ²μ μ΄λ€ κ°μΉκ° μλκ°? μ μ²΄ νλ‘μ νΈμμ νκ΅°λ°μμλ§ μ¬μ©νλ€λ©΄ κ·Έκ³³μμλ§ μ¬μ©νλ©΄ λκ³ , λκ΅°λ° μ΄μμμ μ¬μ©νλ€λ©΄ κ·Έκ±΄ μ­ν λΆλ¦¬κ° μ λλ‘ μλμλ€λ λ»μ΄λ€.
κ΄μ¬μ¬ λΌλ¦¬ λΆλ¦¬κ° λμλμ§ νμΈν΄μΌ νκ³ , λ€λ₯Έκ³³μμλ μ¬μ©νκ³  μλ€λ©΄ μμ¬ν΄λ΄μΌ νλ€.
<br>

- [constructor νΈμΆ](https://github.com/woowacourse/javascript-lotto/pull/114#discussion_r814526816)
  - μΈμ€ν΄μ€ννκ³  bindEventsλ₯Ό νΈμΆνλ λͺλ Ήμ΄ λ°λμ μμ°¨μ μΌλ‘ μΌμ΄λλ κ±°λΌλ©΄,
  bindEvents λ©μλλ₯Ό constructorμ λ£μ΄λλ νΈμ΄ λ«λ€
  κ΅³μ΄ `initDom(), bindEvents()` ν  νμκ° μκ³ , constructor κ° κΈΈμ΄ μ§λ€κ³  ν΄μ λμ  μ΄μ κ° μλ€. 

```js
// before
bindEvents() {
  this.purchaseForm.addEventListener("submit", this.onSubmitPurchase.bind(this));
  this.switchInput.addEventListener("click", this.onClickSwitch.bind(this));
}

// after
constructor() {
  this.purchaseForm.addEventListener("submit", this.onSubmitPurchase.bind(this));
  this.switchInput.addEventListener("click", this.onClickSwitch.bind(this));
}
```

- [λ‘λ λ²νΈ μμ±](https://github.com/woowacourse/javascript-lotto/pull/114#discussion_r814528467) 
  - 1 ~ 45 μ«μλ₯Ό μκ³  0 ~ 5 μΈλ±μ€ λ°°μ΄μ κ°μ Έμ¨λ€.
  λλΆλΆ while λ¬Έμ μ¬μ©ν΄μ κ΅¬νμ νμλ€. μν€νμ² λ¦¬ν©ν λ§λ μ€μνμ§λ§, νλμ κΈ°λ₯λ μ€μνλ€!!<br>
  λ μ’μ λ°©λ²μ΄ μλμ§ μκ°ν΄λ³Έλ€

```js
// 1. λλΆλΆ while λ¬Έμ μ¬μ©ν΄μ κ΅¬νν¨
generateRandomNumber() {
  while (this.numbers.length < LOTTO_NUMBER.LENGTH) {
    const randomNumber = getRandomNumber(LOTTO_NUMBER.RANGE_MIN, LOTTO_NUMBER.RANGE_MAX);
    if (!this.numbers.includes(randomNumber)) {
      this.numbers.push(randomNumber);
    }
  }
}


// 2. 1~45 λ°°μ΄μ λ§λ€κ³  λλ€ μΈλ±μ€λ₯Ό λ½μμ λ²νΈλ₯Ό λ§λ λ€
const lottoNumbers = Array(RANGE_MAX)
  .fill()
  .map((num, index) => index + RANGE_MIN);
for (let i = 0; i < 6; i += 1) {
  const randomIndex = getRandomNumber(lottoNumbers.length);
  this.numbers.push(lottoNumbers[randomIndex]);
  lottoNumbers.splice(randomIndex, 1);
}


// 3. 1~45 λ°°μ΄μ λ§λ€κ³  shuffle ν λ€, 0~5 μΈλ±μ€ slice
export const shuffleArray = (array) => {
  array.sort(() => Math.random() - 0.5);
};

const lottoNumbers = Array(RANGE_MAX)
  .fill()
  .map((_, index) => index + RANGE_MIN);
shuffleArray(lottoNumbers);
this.numbers = lottoNumbers.slice(LENGTH_MIN, LENGTH_MAX);
```

- [html/class-name](https://github.com/woowacourse/javascript-lotto/pull/93#discussion_r815450624)
  - label κ³Όcheckbox input μ κ°μΈλ μΉκ΅¬λ₯Ό `wrapper` λΌ λ³΄κ³ , form κ³Ό κ°μ΄ μ¬λ¬ μ»΄ν¬λνΈ (μ¬λ¬ λ¨μμ element) λ₯Ό κ°μΈλ μΉκ΅¬λ₯Ό `container` λΌκ³  μκ°λλ€
<br>

- [test code](https://github.com/woowacourse/javascript-lotto/pull/98#discussion_r814772262) 
  - νμ€νΈμ½λκ° μμΌλ©΄ νμ€νΈμ½λλ₯Ό λ¨Όμ  λ³΄λ©΄μ κ΅¬νν λ΄μ©μ νμνλ νΈμ΄κ³ , νμ€νΈμ½λ === λͺμΈλΌκ³ λ μκ°ν  μ μκΈ° λλ¬Έμ νμ€νΈμ½λλ μ νν΄μΌ νλ€!
<br>

- [html κ°μ](https://github.com/woowacourse/javascript-lotto/pull/88#discussion_r815314518)
  - μ΄λ³΄μλ₯Ό μν HTML κΈ°μ΄ μ‘°μ κ°λ°μλμ΄ κ³΅μλ¬Έμ μ€νμ κΈ°μ€μΌλ‘ νλ λ§λ  κ°μμ΄λ μκ°λμ€λ νλ² λ£λκ±Έ μΆμ²ν©λλ€
