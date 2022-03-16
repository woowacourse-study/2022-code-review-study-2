## 🎯 Level-1 lotto Step2(80, 84, 87 / 98, 99 / 93, 86 / 83, 90 / 91, 102) - 안

- 분석 담당 코드

  - [#80](https://github.com/woowacourse/javascript-youtube-classroom/pull/80) 안
  - [#84](https://github.com/woowacourse/javascript-youtube-classroom/pull/84) 샐리
  - [#87](https://github.com/woowacourse/javascript-youtube-classroom/pull/87) 온스타

  - [#98](https://github.com/woowacourse/javascript-youtube-classroom/pull/98) 꼬재
  - [#99](https://github.com/woowacourse/javascript-youtube-classroom/pull/99) 유세지

  - [#93](https://github.com/woowacourse/javascript-youtube-classroom/pull/93) 태태
  - [#86](https://github.com/woowacourse/javascript-youtube-classroom/pull/86) 결

  - [#83](https://github.com/woowacourse/javascript-youtube-classroom/pull/83) 준찌
  - [#90](https://github.com/woowacourse/javascript-youtube-classroom/pull/90) 빅터

  - [#91](https://github.com/woowacourse/javascript-youtube-classroom/pull/91) 나인
  - [#102](https://github.com/woowacourse/javascript-youtube-classroom/pull/102) 밧드

## 📝 코드 분석

#### 검색을 하고 스크롤을 내린 뒤 재검색시 자동으로 맨 위로 올라간다!

```js
export const scrollToTop = (element = document.querySelector("body")) => {
  element.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};
```

#### url 입력

search 속성의 매개변수 각각에 접근할 수 있는 URLSearchParams 객체입니다.
url을 간편하게 다룰 수 있도록 URL객체가 마련되어 있다. 이것을 사용하면 프로토콜, 파라미터, 호스트 네임 변경과 같은 작업을 편하게 할 수 있다.

```js
const url = new URL(REDIRECT_SERVER_HOST);

const parameters = new URLSearchParams({
  part: "snippet",
  type: "video",
  maxResults: ITEMS_PER_REQUEST,
  regionCode: "kr",
  safeSearch: "strict",
  pageToken: nextPageToken,
  q: searchKeyword,
});

url.search = parameters.toString();
```

#### throttle

스크롤 이벤트 발생시 throttl을 호출하고 콜백함수로 `this.#onScrollVideoList` 넘겨준다

```js
this.#videoList.addEventListener(
  "scroll",
  throttle(this.#onScrollVideoList, DELAY_TIME)
);

export const throttle = (callback, delayTime) => {
  let timerId;

  return () => {
    if (timerId) return;

    timerId = setTimeout(() => {
      timerId = null;
      callback();
    }, delayTime);
  };
};
```

## ✅ 피드백 정리

#### [#80](https://github.com/woowacourse/javascript-youtube-classroom/pull/80#issuecomment-1065912476)

검색이 완료되었을 때, 기존 검색어가 지워지고 영상이 노출되는데 검색어를 그대로 남겨놓는 건 어떻게 생각하세요?

다른 미션을 할 때에는 input value를 지워 주는게 사용자 입장에서 더 좋다고 생각하였는데,
유튜브 검색에서는 검색어를 남겨주는게 더 맞다고 생각됩니다.

#### [#98](https://github.com/woowacourse/javascript-youtube-classroom/pull/98#pullrequestreview-908107500)

⭐️ 테스트코드를 잘 작성해주신 덕분에 코드 파악하기가 완전 수월했습니다.

이런식으로 테스트를 잘게 나누어서 작성할 수 있다. 되는 경우와 안되는 경우 둘다 테스트 한다
짧게 작성해도 아무 문제 없다!

```js
describe("검색하려는 입력값이 유효한 값인지 검증한다.", () => {
  test("입력값이 비어있는 경우 true를 반환한다.", () => {
    const inputValue = "     ";

    expect(isEmptyString(inputValue)).toBe(true);
  });

  test("입력값이 비어있지 않을 경우 false를 반환한다.", () => {
    const inputValue = "xooos";

    expect(isEmptyString(inputValue)).toBe(false);
  });
});

test("응답받은 날짜 데이터를 정해진 형식(YYYY년 M월 D일)으로 변경한다.", () => {
  const rawDate = "2022-03-02T11:39:31Z";

  expect(parsedDate(rawDate)).toBe("2022년 3월 2일");
});
```

#### [#98](https://github.com/woowacourse/javascript-youtube-classroom/pull/98/files/bb9259cf61f17d1cfc9872fd125664337d8758f6#r825415865)

- 실제 API를 호출하지 않고 Mock Data를 이용하여 테스트하는 케이스는 불필요하다고 생각되는데...
  실제 API 통신을 테스트 할 때는 어떻게 하는지 알 수 있을까요?

- 테스트의 대상이 누구인지 부터 정의를 해보면 좋을 거 같습니다.
  API 를 테스트할 것인가? 아니면 API 의 응답을 처리하는 로직을 테스트할 것인가?
  저는 전자는 BE 의 몫이라고 생각합니다. 기본적으로는 테스트는 독립적이어야한다고 생각을 하는데요 (문제가 하나라면 테스트 케이스도 하나 실패) API 를 테스트 할 게 아니라면 실제 API 를 호출할 필요는 없다고 생각합니다.

  만약 테스트가 실패했을 경우 네트워크 문제, API 문제 등 우리 테스트와 관계없는 곳에서 문제가 발생할 여지가 있으니까요.

#### [#98](https://github.com/woowacourse/javascript-youtube-classroom/pull/98#issuecomment-1068012386)

- 꼬재 : 현재 구조를 디벨롭 시키고 싶은 마음이 있는데, 지식이 부족하여 방향 설계하는 부분에 어려움이 있는 것 같습니다. 리뷰어님의 경우 이러한 미션이 주어지셨을때 어떤 방향성으로 접근하여 구조를 설계하는지 궁금합니다!! 😯
  (처음 구조를 설계할 때 어떻게 접근하면 좋은지??)

- 리뷰어 : 먼저,, 그림으로 작성해주셨지만 꼬재님이 어떤 방향으로 접근하여 구조를 설계하신지 궁금해요! 말씀 주시면 거기에 제 생각을 더 얹어 말씀드리는 게 좋을 것 같습니다.

- 꼬재 :도메인과 UI를 분리하자를 초점을 잡고 분리하였고 util과 dom 관련된 요소들을 분리해서 관리하자! 로 구조를 잡았던 것 같아요
  이후 디벨롭을 해보려했는데, 미션 시간이 촉박하여 진행하지 못한 부분도 있습니다!!
  YoutubeApp 모든 일을 다하고 있는 것 같아보여서 이 부분을 디벨롭 하는게 좋아 보인다 생각했었어요!
  저와 페어의 고민은 여기까지 였습니다!
  근데, 혹시 저희가 생각하는 방향이 잘못되진 않았는지 궁금해서 월터님께도 여쭤봤던거에요!
  보통은 어떤식으로 접근해서 구조를 잡아나가는게 좋은지에 대한...?? 순수한 궁금증이랄까요.... 🥲 <br>

- 리뷰어 : 지금쯤이면 꼬재님도 "정답은 없다." 라는 사실을 알고 계실 것 같아요 ㅋㅋㅋㅋ,
  저는 개인적으로 도메인과 UI를 분리하자를 초점을 잡고 분리하였고 util과 dom 관련된 요소들을 분리해서 관리하자 라는 컨셉을 잡고 프로젝트를 진행한 점이 매우 좋았습니다. 사실 구조/코드에는 정답이 없기 때문에 여러 시도를 해봐야한다고 생각을 하거든요. 말씀주신 것처럼 이런 컨셉으로 진행을 했더니 "YoutubeApp 이 하는 일이 너무 많아진 거 같다." 라는 고민을 하고 개선을 해야겠다고 생각을 하셨구용. 매우 긍정적인 방향인 거 같아요 :) <br>
  사실 step2 에서 구조를 바꾸는 건 서로가ㅋㅋ 힘들 상황 같은데, 꼬재가 모든 건 다 완벽하게 했어! 라는 생각이 들면 구조 개선을 진행해봐도 좋을 거 같아요. - 구조보다는 미션에 집중하는게 좋겠다? <br>
  만약 e2e 테스트를 작성하지 않았다면, 반대했을 거 같은데ㅎㅎㅎㅎ, e2e 테스트가 작성되어있는 상황에서 안전한 환경에서 테스트를 최소한으로 깨뜨리고 빨리 복구시키면서 리팩터링을 해보는 것도 좋은 경험일 거 같습니다.
  지금같이 작은 프로젝트에서는 어떤 구조를 적용하더라도 오버엔지니어링 느낌이 강해서, 컨셉을 하나 잡고 앞으로 기능이 늘어나면 어떤 점이 유리하겠다 불리하겠다 등을 느끼는 게 더욱 중요한 거 같습니다! (지금 매우 잘하고 계세요 진~짜)

- 한마디로 정리하면 먼저 자신만의 기준을 잡고 여러 시도를 해보는 것이 중요하다. 그 과정에서 스스로 느낀 문제점이나
  불편한점을 알게 되면 그때 수정을 하면 된다. 그렇게 구조가 잡혀 가는 것 같다. 또한, 설계 구조도 중요하지만 일단 미션 자체에
  집중을 하고 여유가 된다면 구조를 생각해 보면 좋겠다.
  피드백을 받고 난 뒤 꼬재의 생각이 궁금하여 DM을 보냈다!!

- 꼬재 한테 받은 DM : 아직 js에 대한 개념도 부족하다고 생각이 많이 들어 최대한 바닐라 js에 집중을 해보고자... 하려구요!!!
  구조에 대해 굉장히 많이 신경을 썼는데... 리뷰어가 답장을 남겨주신 것 처럼 모든 것이 완벽하다고 생각이 들면 그때 구조에 대해 고민을 해보려 하는데, 시간적인 여유가 있을것 같지는 않아요..!!!
  다음 미션에서는 페어와 이야기를 나눠봐야할 것 같아요!
  저같은 경우는 머리가 많이 복잡했는데, 조금 내려놓기로 했습니다!
