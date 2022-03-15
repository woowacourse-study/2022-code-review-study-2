# Level-2 로또 Step1(76, 81, 88, 89, 92, 101, 104, 108, 111, 112) - 앨버

- 분석 담당 코드
  - [#76](https://github.com/woowacourse/javascript-youtube-classroom/pull/76)
  - [#81](https://github.com/woowacourse/javascript-youtube-classroom/pull/81)
  - [#88](https://github.com/woowacourse/javascript-youtube-classroom/pull/88)
  - [#89](https://github.com/woowacourse/javascript-youtube-classroom/pull/89)
  - [#92](https://github.com/woowacourse/javascript-youtube-classroom/pull/92)
  - [#101](https://github.com/woowacourse/javascript-youtube-classroom/pull/101)
  - [#104](https://github.com/woowacourse/javascript-youtube-classroom/pull/104)
  - [#108](https://github.com/woowacourse/javascript-youtube-classroom/pull/108)
  - [#111](https://github.com/woowacourse/javascript-youtube-classroom/pull/111)
  - [#112](https://github.com/woowacourse/javascript-youtube-classroom/pull/112)

## 아키텍처 분석(desc: 담당한 1개의 소프트웨어의 아키텍처를 간단히 분석하고 설명합니다)

<br>

## 피드백 정리

### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)

- [[#76](https://github.com/woowacourse/javascript-youtube-classroom/pull/76#discussion_r825292680) - 명료한 코드 작성] 반환해주는 값을 변수로 선언해주어 다른 사람들에게 해당 데이터가 무엇인지 명료하게 알려준다.

  ```javascript
  const response = await fetch(url, { method: 'GET' });

  this.checkExceedCapacity(response);
  return await response.json();
  ```

  위처럼 `response.json()`을 반환하는 것보다 해당 데이터가 무엇인지 변수로 선언, 할당한 후 전달해주면 다른 개발자들이 코드를 읽는데 가독성이 더 좋을 듯하다.

<br>

- [[#81](https://github.com/woowacourse/javascript-youtube-classroom/pull/81#pullrequestreview-908079725) - 과도한 set 사용]

  ```
  set-* 이 너무 많습니다! get은 많아도 됩니다. 왜냐하면 내부 상태를 바꿀 수 있진 않거든요. 그런데 set이 너무 많으면 무슨 문제가 생기냐면, 내부에 어떤 로직이 있다고 했을때 외부의 어떤 상황에 의해 set이 호출되서 상태가 변경이 되고, 내부의 로직이 변경될 수 있습니다. 잠재적 위험이 있는거죠 ㅠ
  ```

<br>

- [[#81](https://github.com/woowacourse/javascript-youtube-classroom/pull/81#discussion_r825378003) - semantic 태그]

  ```javascript
  <div class="modal-container hide">
  ```

  모달창에 대한 semantic tag인 `<dialog>`를 사용할 수 있다. 기본적으로 제공되었던 HTML이라 `semantic tag` 사용을 놓쳤었던 것을 반성한다..

<br>

- [[#81](https://github.com/woowacourse/javascript-youtube-classroom/pull/81#discussion_r825378158) - pacakage.json의 버전]

  ```json
  {
  "name": "javascript-youtube-classroom",
  "version": "1.0.0",
  ```

  ```
  package.json 처럼 쓰이는 버전 양식을 semver 라고 합니다. (Sementic Versioning의 약자)

  제가 보기엔, 완성된게 아니므로 메이저 버전이 1이 될 수 없을 것 같아요!
  그렇기에 0.x.x 요렇게 표기되어야 하지 않을까 싶네요~
  ```

  package.json에서의 버전에 대한 코멘트가 있어서 가지고 와밨습니다~

<br>

- [[#81](https://github.com/woowacourse/javascript-youtube-classroom/pull/81#discussion_r825379549) - 체이닝 패턴]

  ```javascript
  const {
    thumbnails: {
      high: { url },
    },
    channelTitle,
    title,
    publishTime,
  } = item.snippet;
  ```

  위처럼 체이닝 패턴을 이용해 가독성있게 정보를 추출할 수 있다!

<br>

- [[#81](https://github.com/woowacourse/javascript-youtube-classroom/pull/81/files/1b344e5fc75663f80b4f10feb0714ac03330ec41#r825379763) - 클로저를 이용한 throttle]

  ```javascript
  const throttle = (callback, time) => {
    let throttleReference;

    return function () {
      if (!throttleReference) {
        throttleReference = setTimeout(() => {
          throttleReference = null;
          callback();
        }, time);
      }
    };
  };
  export default throttle;
  ```

  클로저를 이용해서 throttle을 사용!

<br>

- [[#89](https://github.com/woowacourse/javascript-youtube-classroom/pull/89#discussion_r825416052) - document에 이벤트 리스너를 달면 안좋은 이유]

  ```
  전역에서 사용되는 document에 click event listener를 추가하는 방식은 불필요한 이벤트 감지가 자주 발생하여 권해 드리기 어렵습니다
  지금은 혼자 개발하지만 대부분은 협업으로 개발을 진행하게 되는데, 이때 전역에 매핑�된 이벤트 리스너는 의도치 않은 동작을 발생시킬 수 있습니다
  이벤트를 매핑하는 영역은 내가 다루고 있는 컴포넌트 영역으로 한정하시면 좋을 것 같습니다
  ```

<br>

- [[#92](https://github.com/woowacourse/javascript-youtube-classroom/pull/92#discussion_r825280248) - localStorage.getItem 에러핸들링]

  ```javascript
  export const getLocalStorage = (key) => {
    return JSON.parse(localStorage.getItem(key)) || [];
  };
  ```

  일반적인 `localStorage.getItem`을 `JSON.parse` 해줬을 경우 변환할 문자열이 유효한 JSON이 아닐 경우 SyntaxError에러가 발생하므로 해당 에러처리도 해주면 좋을 것 같다.

<br>

- [[#101](https://github.com/woowacourse/javascript-youtube-classroom/pull/92#discussion_r825280248) - URLSearchParams 사용]

  ```javascript
  #generateSearchParams(keyword) {
    return new URLSearchParams({
      ...SEARCH_API.PARAMS,
      pageToken: this.nextPageToken,
      q: keyword,
    }).toString();
  }
  ```

  URLSearchParams를 활용하여 깔끔하게 URL을 만들어줄 수 있다.

<br>

- [[#111](https://github.com/woowacourse/javascript-youtube-classroom/pull/111#discussion_r825246994) - addEventListener this 바인드 방식]

  ```
  bind(this) 대신 handler로 등록할 메소드들을 class field (arrow function)으로 전환하시는걸 추천합니다.

  메소드 선언 방식에 의하면 prototype에 원본메소드가 남아있는 채로, 실제로 호출되는건 새로 만들어진 bound 메소드입니다. 사용하지 않을 불필요한 메소드가 남아있다는 뜻이죠. 반면 class field를 이용하면 prototype에는 남아있지 않고, 인스턴스 자신이 사용할 함수만 들고 있게 됩니다.
  ```

<br>

- [[#111](https://github.com/woowacourse/javascript-youtube-classroom/pull/111#discussion_r825247862) - 성능을 생각한 스켈레톤 UI]

  ```
  로딩완료시 loading중에 보여주는 임시 element들을 전부 삭제했다가 다음번 loading시 다시 삽입하는 방식 대신에
  처음부터 loading중에 보여줄 요소를 맨 뒤에 만들어두고, show/hide만 하는 방식이 성능상 더 좋을 것 같아요.
  ```

  [왜 이럴까?에 대한 참고 링크](https://stackoverflow.com/questions/2447309/javascript-removechild-and-appendchild-vs-display-none-and-display-blockinl)

<br>

- [[#111](https://github.com/woowacourse/javascript-youtube-classroom/pull/111#discussion_r825249100) - replaceChildren]

  ```javascript
  while (parentNode.firstChild) {
    parentNode.removeChild(parentNode.firstChild);
  }
  ```

  위의 코드를 대체할 수 있는 `replaceChildren`

<br>
