# Level-2 로또 Step1(81, 82, 87, 90, 112, 113, 116, 119) - 앨버
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
- [[#116](https://github.com/woowacourse/javascript-lotto/pull/116), [#119](https://github.com/woowacourse/javascript-lotto/pull/119)] Flux pattern
    - 티거와 병민은 이번 미션에서 `Flux` 패턴을 사용하였습니다. 
    - Flux는 애플리케이션에서 데이터를 취급하기 위한 패턴(pattern)입니다. 
    - [Flux 패턴이 나오게 된 이유](https://bestalign.github.io/translation/cartoon-guide-to-flux/#%EA%B7%BC%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%AC%B8%EC%A0%9C%EC%A0%90) - 데이터의 흐름을 예측하기 어렵기 때문이라고 합니다.
        ```
        <발췌>

        이전에는 데이터를 가지고 있는 모델(model)이 렌더링(rendering)을 하기위해 뷰 레이어(view layer)로 데이터를 보냈을 것이다.

        사용자와의 상호작용(user interaction)이 뷰(view)를 통해서 일어났기 때문에 사용자의 입력에 따라 뷰가 가끔씩 모델을 업데이트해야할 필요가 있었다. 그리고, [의존성(dependency) 때문에] 모델이 다른 모델을 업데이트해야할 때도 있었다.

        그 외에도, 가끔씩 이런 것들 때문에 산사태처럼 아주 많은 다른 변경을 초래하기도 했다. 이것은 마치 아주 긴장감 넘치는 Pong 게임1과 같다 — 공이 어디로 날아갈지 알기 아주 어렵다 (화면 밖으로 가버릴지도 모른다).
        ```

        ![여러 데이터 흐름을 나타내는 사진](https://user-images.githubusercontent.com/64825713/156369229-88655af9-5f2d-47e3-9d47-bf6af1c7fdea.png)
    
    <br>
    
    - 이에 대한 해결책으로 `단방향 데이터 흐름`을 기반으로 하는 `Flux`패턴을 개발하였습니다. 
    ![flux 패턴](https://user-images.githubusercontent.com/64825713/156369470-6442c41b-8db9-487c-8034-306e0bd4f85e.png)

    - `Action` - 모든 변경사항과 사용자와의 상호작용이 거쳐가야 하는 액션의 생성을 담당하고 있습니다. 언제든 애플리케이션의 상태를 변경하거나 뷰를 업데이트하고 싶다면 액션을 생성해야만 합니다. 액션 메시지를 생성한 뒤에는 디스패쳐(dispatcher)로 넘겨줍니다.
    - `Dispatcher` - 디스패쳐는 액션을 보낼 필요가 있는 모든 스토어(store)를 가지고 있고, 액션 생성자로부터 액션이 넘어오면 여러 스토어에 액션을 보냅니다. 이 처리는 동기적으로(synchronously) 실행됩니다.
    - `Store` - 스토어는 애플리케이션 내의 모든 상태와 그와 관련된 로직을 가지고 있습니다. 모든 상태 변경은 반드시 스토어에 의해서 결정되어야만 하며, 상태 변경을 위한 요청을 스토어에 직접 보낼 순 없습니다. 스토어에 상태 변경을 완료하고 나면, 변경 이벤트(change event)를 내보냅니다. 이 이벤트는 컨트롤러 뷰(the controller view)에 상태가 변경했다는 것을 알려주게 됩니다.
    - `View` - 뷰는 상태를 상태를 가져오고 유저에게 보여주고 입력받을 화면을 렌더링하는 역할을 맡습니다.

<br>

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


