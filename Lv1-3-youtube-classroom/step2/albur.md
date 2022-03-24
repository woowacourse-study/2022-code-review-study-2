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

-[[#139](https://github.com/woowacourse/javascript-youtube-classroom/pull/139#discussion_r830580284) - jest 테스트시 cypress ignore]

```json
  "jest": {
    "testPathIgnorePatterns": [
      "cypress"
    ]
  },
```

<br>
