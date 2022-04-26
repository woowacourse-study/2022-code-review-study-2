# Level1 유튜브 Step1(78,82,85,97,100,103,107,113) - 시지프

분석 담당 코드

- [#113, 시지프](https://github.com/woowacourse/javascript-youtube-classroom/pull/113)
- [#107, 우디](https://github.com/woowacourse/javascript-youtube-classroom/pull/107)

  - button 을 throttle로 구현
  - api mocking - strategy pattern
  - validate 방법

- [#97, 블링](https://github.com/woowacourse/javascript-youtube-classroom/pull/97)
- [#78, 도리](https://github.com/woowacourse/javascript-youtube-classroom/pull/85)

- [#85, 도리](https://github.com/woowacourse/javascript-youtube-classroom/pull/85)
- [#82, 소피아](https://github.com/woowacourse/javascript-youtube-classroom/pull/82)
  - scroll event에 debounce
  - custom event
- [#100, 마르코](https://github.com/woowacourse/javascript-youtube-classroom/pull/100)
- [#103, 위니](https://github.com/woowacourse/javascript-youtube-classroom/pull/103)

## 코드 분석

- !! 연산자
  값이 있으면 true를, null이나 undefined를 false로 반환하도록 하는 연산

  ```javascript
  var case1; // undefined
  console.log("case1  : " + case1);
  console.log("!case1 : " + !case1);
  console.log("!!case1: " + !!case1);
  console.log(""); // 개행
  var case2 = true; // 불리언 데이터
  console.log("case2  : " + case2);
  console.log("!case2 : " + !case2);
  console.log("!!case2: " + !!case2);
  console.log(""); // 개행
  var case3 = null; // null
  console.log("case3  : " + case3);
  console.log("!case3 : " + !case3);
  console.log("!!case3: " + !!case3);
  ```

- ?? 연산자

  물음표 두개, 그것이 nullish coalescing 연산자다. numberOfBanana의 값이 0인 것을 보고 이미 이 연산자의 정체를 알았을 수도 있겠다. 맞다. 기본값을 정해주는 연산자다. 값이 null 또는 undefined인 경우에 기본값을 정해준다. 이 부분에서 주목해야 할 점은 이 연산자는 OR(||) 연산자와 다르게 null이나 undefined가 아닌 falsy 값(0, ""와 같은 것들)들을 기본값으로 바꾸어 버리지 않는다는 것이다. 그렇기에 정확하게 "값이 존재하지 않을 때"에 대해 처리할 수 있다. 결과적으로, 위 코드는 다음과 같이 작동한다.

- debounce(자동완성, ), throttling(검색 버튼)

  - 서버 과부하를 줄이기 위해서

    <img src="https://media.vlpt.us/images/soulee__/post/47697d1d-2cd1-460d-a9f7-99e6f48bad14/image.png" width="50%">

    ```javascript
    export const throttle = (callback, delay = 0) => {
      let timerId = null;

      return (...args) => {
        if (timerId) return;

        timerId = setTimeout(() => {
          callback(...args);

          timerId = null;
        }, delay);
      };
    };

    export const debounce = (callback, wait = 0) => {
      let timerId = null;

      return (...args) => {
        if (timerId) clearTimeout(timerId);

        timerId = setTimeout(() => {
          callback(...args);
        }, wait);
      };
    };
    ```

- Custom Event

  - view, controller, model 간 의존을 줄일 수 있다.
  - submit 이벤트를 감지하면, submit@custom event를 dispatch 날리고, 다른 곳에서 submit@custom를 받아서 handler를 수행하게 한다.

    ```javascript
    // SearchKeywordFormView
    bindEvents() {
        $('#search-form').addEventListener('submit', this.onSubmitSearchForm.bind(this));
      }

      onSubmitSearchForm(e) {
        e.preventDefault();
        const keyword = $('#search-input-keyword').value;
        event.dispatch('searchWithNewKeyword', { keyword });
      }

    // controller
    event.addListener('searchWithNewKeyword', this.searchWithNewKeyword.bind(this));

    searchWithNewKeyword(e) {
        ...
        event.dispatch('resetSearchResult');
        ...
    }

    // SearchResultView

    event.addListener('resetSearchResult', this.resetSearchResult.bind(this));

    ```

## 피드백 정리

### 테스트 코드

- [#97](https://github.com/woowacourse/javascript-youtube-classroom/pull/97/files/bde0deb96345a143d62486356ddaf34e0bb28e9a#diff-9d4b750022db31c704dbd98d6c04ff9e6d4e2b7229107191aab53066f30042db) 음 이건 localStorage 를 테스트하는건가요? localStorage 는 직접 구현하신게 아닌 브라우저 기능인데요. 굳이 그거까지 테스트를 해야하나 싶습니다.
  e2e 테스트였다면 비디오 저장 후 새로고침했을 때 저장된 비디오가 있는지, 그리고 2단계에서는 비디오가 잘 노출되는지를 테스트해봤을 것 같네요!

  ```javascript
  describe("비디오 저장하기 관련 기능 테스트", () => {
    test("로컬 저장소에 id를 저장하고 불러올 수 있다.", () => {
      const id = "sampleId";

      storage.setSavedVideos(id);

      expect(storage.getSavedVideos()[id]).toBe(true);
    });
  });
  ```

- [#82] fetch 과정 자체만 테스트하는 케이스는 추가하지 않더라도, fetch로 받은 데이터를 후처리하는 로직에 대한 테스트를 추가하는 방향으로 고민해보고 있습니다. fetch()를 테스트하는 방법으로 저희가 놓친 부분이 있을까요?

  fetch를 mock하는 이유는 fetch 자체를 검증하기 위함보다는 메서드가 전반적인 제대로 동작하는지 보기 위함입니다. fetch에서 데이터를 성공적으로 받아올 때는 어떻게 처리하는지? 만약 중간에 에러가 나면 어떻게 처리해야 되는지? 여러 상황들을 테스트 해볼 수 있겠죠.

  하지만, 테스트하려는 메서드 내부에 정말 fetch 호출 하나만 딱 있는 경우라면 테스트를 위한 테스트가 될 수 있겠네요.

- [#100] 보통 더미 데이터로 많이 사용하지만 실제 api를 테스트해서 하는 것만큼 통합테스트에 적합한 것이 없겠습니다 :) 여기서 중요한 점은 "유닛 테스트" 와 "통합 테스트"의 차이를 집중해야한다는 것입니다. 비디오의 데이터를 활용해 다양한 메소드나 함수들이 정상동작하는지 여부를 파악하고 싶다면 더미데이터를 이용해서 유닛테스트를 진행하면 맞을 것 같고. api가 정상적으로 동작되는가에 대한 통합 테스트는 jest의 mock 기능을 이용해 진행하시면 좋겠습니다.

- [#100] 왜 안되는 케이스를 중심으로 짜야하는가?

  로직의 "정상적으로 작동" 하는 결과는 하나뿐입니다. 하지만 오작동하는 케이스는 수십가지가 넘죠. 예를들자면 결과값이 "2"가 되어야 하는 케이스가 있다고 합시다. 결국 어떤 시나리오, 2+0, 1+1, 0+2 등, 결국 2가 되면 맞는 게임입니다. 하지만 그 외에 아닌 케이스는 정말 많겠죠?

  서비스의 개발도 위와 동일합니다. 결국 어떻게 되었던 이 로직이 제대로 도는 결과는 하나이고 오작동하는 케이스는 수십가지가 넘을 것입니다. 특히 복잡한 유저관점에서 해석을 한다면 유저가 어떻게 행동할지 미리 생각해서 유저가 어떤 행동을 했을때 오작동을 하면 "유저에게 이렇게 사용하지마!" 라는 피드백이 필요할 것입니다.

  이는 기능관점에서도 유효합니다. "버튼을 누른다"의 경우 정상적인 케이스는 "버튼이 눌려서 어떤 액션이 실행되었는가?" 겠죠. 그런데 버튼을 0.1초 안에 200번을 누르는 케이스가 존재한다면 (실제로 dom 이벤트를 이렇게 증식 시켜서 디도스를 할 수도 있겠죠.) 이런 문제 케이스에 대해서 대응을 해야겠죠? 왜냐하면 버튼에서 "어떤 액션"의 범주는 굉장히 넓고, 거기엔 비동기 처리도 있을테니까요.

  결론적으로 안되는 케이스를 주요로 작성하라는건 다음과 같습니다.

  애자일 철학에서도 나오는 "유저스토리 관점으로 생각하라" 처럼, 이 메소드/함수와 같은 행동을 사용하는 유저 관점에서 생각하고, 테스트를 작성하라
  유저 관점에서 생각하면 유저가 정상적으로 사용할 수 있는 케이스는 "하나" 이고, 그 외에 오작동 하는 케이스에 대한 "수많은" 문제를 정상적으로 사용할 수 있도록 유도하는 코드가 등장하게 된다.
  테스트 코드는 협업하는 사람들에게 어떤 문제에 대해 코드가 보완되어 있는지 공유하는 성격도 갖고있습니다. 특히 현업에선 QA TC등이 결국 테스트 코드와 매칭되는 부분이 많습니다. 에러 상황에 대한 테스트 코드가 많을수록 당연히 QA에서 커버되는 커버리지를 코드단위로 이행시켜서 효율성을 증대 시킬 수 있겠죠?

## 기타 배울 점

- 네트워크 테스트, timeout 테스트
