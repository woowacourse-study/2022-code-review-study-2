# Level-2 로또 Step1(81, 82, 87, 90, 112, 113, 116, 119) - 작성자닉네임
- 분석 담당 코드
    - [#81](https://github.com/woowacourse/javascript-lotto/pull/81)
    - [#82](https://github.com/woowacourse/javascript-lotto/pull/82)
    - [#87](https://github.com/woowacourse/javascript-lotto/pull/87)
    - [#90](https://github.com/woowacourse/javascript-lotto/pull/90)
    - [#112](https://github.com/woowacourse/javascript-lotto/pull/112)
    - [#113](https://github.com/woowacourse/javascript-lotto/pull/113)
    - [#116](https://github.com/woowacourse/javascript-lotto/pull/116)
    - [#119](https://github.com/woowacourse/javascript-lotto/pull/119)



## 아키텍처 분석(desc: 담당한 1개의 소프트웨어의 아키텍처를 간단히 분석하고 설명합니다)
- [해당 PR 번호] 내용
    - 상세 내용

## 피드백 정리
### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)
- [[#81](https://github.com/woowacourse/javascript-lotto/pull/81#discussion_r814068248) - css] 중복되는 css를 하나의 클래스로 만들어서 중복을 줄인다.
  ```css
    .bonus-number-wrapper {
    display: flex;
    align-items: flex-end;
    flex-direction: column;
    }

    #align-converter-container {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    }
  ```
  
  위처럼 중복되는 css가 있으면 하나의 클래스로 만들어서 코드 중복 사용을 줄일 수도 있겠다고 느꼈습니다.

<br>

- [[#82](https://github.com/woowacourse/javascript-lotto/pull/82/files/b4f543c1072422b932f3a57e9e2cea989732fd01#r813912754) - 드모르간 법칙] 드모르간 법칙을 사용하여 효율적인 코드를 만든다.

    ```javascript

    export function isValidNumber(lottoNumbers) {
        return lottoNumbers.every(
            (number) =>
            Number.isInteger(number) &&
            number >= NUMBER.LOTTO_MIN_NUMBER &&
            number <= NUMBER.LOTTO_MAX_NUMBER
        );

    ```

    위 메서드는 `every`를 사용하여 모든 조건을 탐색해야했었는데 `드모르간 법칙`을 이용하게 되면 `some`을 사용하여 좀 더 효율적인 탐색을 할 수 있는 것을 알게되었습니다.

<br>

- [[#82](https://github.com/woowacourse/javascript-lotto/pull/82/files/b4f543c1072422b932f3a57e9e2cea989732fd01#r813916377) - 메서드 분리] 단순히 기능이 다르다는 이유만으로 메서드를 쪼개는건 지양

    ```javascript

    renderLottoList(lottoList) {
        this.$lottoContainer.innerHTML = lottoList
        .map((lotto) => this.generateLottoTemplate(lotto))
        .join('');
    } 

    renderPurchasedMessage(lottoAmount) {
        this.$purchasedMessage.innerText = `총 ${lottoAmount}개를 구매하였습니다.`;
    }

    ```

    지금까지는 기능이 다르면 무작정 메서드를 분리해주었는데, 꼭 기능만을 기준으로 분리해주는 것도 `답`이 아님을 알 수 있었습니다.

<br>


- [[#113](https://github.com/woowacourse/javascript-lotto/pull/113#discussion_r814420062) - css 주석] 주석을 작성하여 어디에 사용되는 css인지 파악할 수 있도록 작성할 수도 있다는 것을 알게되었습니다.

- [[#116](https://github.com/woowacourse/javascript-lotto/pull/116#discussion_r815274010) - css 세팅] css 초기화를 위해 reset.css가 아니라 normalize.css도 존재한다는 것을 알게되었습니다.


