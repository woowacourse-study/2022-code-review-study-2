# Level-3 유튜브 Step2 - 앨버

- 분석 담당 코드

  - [#116](https://github.com/woowacourse/javascript-youtube-classroom/pull/116)
  - [#123](https://github.com/woowacourse/javascript-youtube-classroom/pull/123)
  - [#124](https://github.com/woowacourse/javascript-youtube-classroom/pull/124)
  - [#129](https://github.com/woowacourse/javascript-youtube-classroom/pull/129)
  - [#135](https://github.com/woowacourse/javascript-youtube-classroom/pull/135)
  - [#137](https://github.com/woowacourse/javascript-youtube-classroom/pull/137)
  - [#138](https://github.com/woowacourse/javascript-youtube-classroom/pull/138)
  - [#139](https://github.com/woowacourse/javascript-youtube-classroom/pull/139)
  - [#146](https://github.com/woowacourse/javascript-youtube-classroom/pull/146)

## 피드백 정리

### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)

- [[#116](https://github.com/woowacourse/javascript-youtube-classroom/pull/116#discussion_r830493006) - dom 탐색 비용] 비디오를 저장할때마다 dom을 탐색해서 값을 직접 가져오고 있기 때문에 dom 탐색 비용이 많이 든다.

  ```javascript
  {
    videoThumbnail: parentTarget.querySelector('.video-item__thumbnail').src,
    videoChannelTitle: parentTarget.querySelector('.video-item__channel-name').innerText,
    videoTitle: parentTarget.querySelector('.video-item__title').innerText,
    videoDate: parentTarget.querySelector('.video-item__published-date').innerText,
  };
  ```

<br>

- [[#129](https://github.com/woowacourse/javascript-youtube-classroom/pull/129#discussion_r830478991)] - css 상수화]

중복된 색상을 찾기힘들어 step1에서 PR을 안드렸었는데 분리해주셨네요!

색상은 특히 해주신거처럼 100단위 팔레트로 빼두는게 좋다고 생각해요 👍

```javascript
:root {
--cyan-dark: rgba(0, 188, 212, 0.12);
--cyan: #00bcd4;

--gray-dark: #8b8b8b;
--gray-900: #b4b4b4;
--gray-800: #ebebeb;
--gray-700: #efefef;
--gray-600: #f5f5f5;
--gray-500: #f9f9f9;

--skeleton-gray-dark: #e0e0e0;
--skeleton-gray-light: #ededed;

--dimmer: rgba(0, 0, 0, 0.5);
--border: rgba(0, 0, 0, 0.12);
}

```

- [[#135](https://github.com/woowacourse/javascript-youtube-classroom/pull/135#pullrequestreview-915496528) - 아키텍처에 대한 리뷰어님의 생각]

  가장 중요한 것은, 아키텍처는 프로그래밍 개발 지식만으론 만들어지지 않는다는걸 이해하셔야합니다. 오늘 만드셨던 "나만의 유튜브 강의실"의 경우 지금 만드신 아키텍처가 적합한지 다시 생각해볼 필요가 있어요.

  "나만의 유튜브 강의실"은 어떤 도메인이고, 특성을 갖고있을까요? 그리고 함께 개발하는 인원은 몇명인가요? 개발 기간은 언제까지일까요? 이런 것처럼 다양한 환경적 요인과 비즈니스를 성사시키기 위해 아키텍처라는 틀을 만들고 협업/목표를 이루기 위한 수단을 만드는 거라 이해하시면 되겠습니다.

<br>

- [[#137](https://github.com/woowacourse/javascript-youtube-classroom/pull/137#discussion_r830518567) - 순수하지 않은 유틸함수]

  ```javascript
  export const toastMessage = (message) => {
    const toast = $('.toast');
    toast.innerText = message;
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), NUM.TOAST_DELAY);
  };
  ```

  toast라는 클래스 네임을 가진 돔객체가 필드에 무조건 존재해야 되는군요.

  공통 util 함수라고 하기에 다소 순수하지 않다는 생각이듭니다.

<br>

- [[#139](https://github.com/woowacourse/javascript-youtube-classroom/pull/139#discussion_r830580284) - jest 테스트시 cypress ignore]

```json
  "jest": {
    "testPathIgnorePatterns": [
      "cypress"
    ]
  },
```

<br>

- [[#146](https://github.com/woowacourse/javascript-youtube-classroom/pull/146#discussion_r830631461) - for attribute]

for 라는 attribute는 label, output 태그에만 붙는 전용속성입니다. javascript에서 활용하고자 한다면 다른 속성 (id, class, dataset)을 사용하세요.

<br>

- [[#146](https://ko.javascript.info/dom-attributes-and-properties#ref-1789) - attribute]

attribute는 '고유속성'에 가까운 정적인 개념이라고 생각하시면 좋을것 같아요.
동적으로 변하는 '상태'에는 적합하지 않습니다.

<br>

- [[#146](https://github.com/woowacourse/javascript-youtube-classroom/pull/146#discussion_r831112399) - 무한스크롤 쓰로틀 시간]

  ```
  '약간의 브레이크'라는게 과연 충분한지를 확신할 수 있는지가 관건이에요. 데이터 응답 시간은 그때그때 다를테고, 그에따라 화면에 렌더링이 이뤄지는 시간도 그때그때 다를건데, 예를 들어 데이터 응답이 1초가 걸리는 상황이라면, 0.8초만에 다시 스크롤요청을 하게 되면 연속해서 2개의 페이지를 받게 되겠죠. 브레이크를 건다는 아이디어 자체는 훌륭합니다만, 서버 및 네트워크 환경에 따라 달라질 수 있는 '시간'을 임의로 0.8초로 지정한 것이 문제라는 거예요. `그보다는 응답이 올 때까지 홀딩한다거나, 다음 리스트가 화면에 렌더링될때까지 기다린다는 식이 되어야 하지 않을까요?`
  ```

  임의의 시간을 정해놓고 한 번의 네트워크 통신이 이뤄지도록 구현한 것이지만, 사실 임의의 시간안에 요청이 오지 않는다면, 요청이 오지 않은 상태에서 하나의 추가적인 요청을 다시 보내게 됨으로써 원하는 바를 구현할 수가 없다.
