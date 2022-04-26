# Level1 나만의 유튜브 강의실 Step2 - 코카콜라

- [#134, 코카콜라](https://github.com/woowacourse/javascript-youtube-classroom/pull/134)
- [#148, 후이](https://github.com/woowacourse/javascript-youtube-classroom/pull/148)
- [#141, 콤피](https://github.com/woowacourse/javascript-youtube-classroom/pull/141)
- [#130, 민초](https://github.com/woowacourse/javascript-youtube-classroom/pull/130)
- [#133, 우연](https://github.com/woowacourse/javascript-youtube-classroom/pull/133)
- [#154, 아놀드](https://github.com/woowacourse/javascript-youtube-classroom/pull/154)
- [#119, 하리](https://github.com/woowacourse/javascript-youtube-classroom/pull/119)
- [#130, 민초](https://github.com/woowacourse/javascript-youtube-classroom/pull/130)

---

## 피드백 정리

### JS 데이터 바인딩이란?

- 자바스크립트 웹 애플리케이션의 복잡도가 증가하면서 브라우저의 메모리에 있는 여러 개의 자바스크립트 객체와 화면에 있는 데이터를 일치시키기가 매우 어려워졌다 - 이러한 어려운 작업을 쉽게 해주는 해결책이 데이터 바인딩

## 데이터 바인딩

- 두 데이터 혹은 정보의 소스를 모두 일치시키는 기법. 즉, 화면에 보이는 데이터와 브라우저 메모리에 있는 데이터를 일치시키는 기법
- 많은 자바스크립트 프레임워크가 이러한 데이터 바인딩 기술을 제공하고 있다.

## 단방향 데이터 바인딩 vs 양방향 데이터 바인딩

- 단방향 데이터 바인딩 : 데이터와 템플릿을 결합하여 화면을 생성
- 양방향 데이터 바인딩 : 데이터의 변화를 감지해 템플릿과 결합하여 화면을 갱신하고 화면에서의 입력에 따라 데이터를 갱신
  즉, 데이터와 화면사이의 데이터가 계속 일치

- [참고 1](https://blog.hyunmin.dev/15)
- [참고 2](<https://sungjk.github.io/2015/11/22/AngularJS(2).html>)
- [참고 3](https://docs.microsoft.com/ko-kr/dotnet/desktop/wpf/data/?view=netdesktop-6.0)

---

### 함수/클래스

[#133, 우연, 인스턴스](https://github.com/woowacourse/javascript-youtube-classroom/pull/133)

```javascript
// before
// src/js/.../YoutubeAPI.js
class YoutubeAPI {}
export default YoutubeAPI;

// src/js/.../sample1.js
import YoutubeAPI from "../YoutubeAPI/index.js";
const youtubeAPI = new YoutubeAPI();

// src/js/.../sample2.js
import YoutubeAPI from "../YoutubeAPI/index.js";
const youtubeAPI = new YoutubeAPI();

// src/js/.../sample3.js
import YoutubeAPI from "../YoutubeAPI/index.js";
const youtubeAPI = new YoutubeAPI();
```

```javascript
// refactor
// src/js/.../YoutubeAPI.js
class YoutubeAPI {}
const youtubeAPI = new YoutubeAPI();
export default youtubeAPI;

// src/js/.../sample1.js
import YoutubeAPI from "../YoutubeAPI/index.js";
YoutubeAPI();

// src/js/.../sample2.js
import YoutubeAPI from "../YoutubeAPI/index.js";
YoutubeAPI();

// src/js/.../sample3.js
import YoutubeAPI from "../YoutubeAPI/index.js";
YoutubeAPI();
```

위와 같이 인스턴스를 내보내고 youtubeAPI 인스턴스가 필요한부분들에서 바로 사용하면됩니다.

const videoView = new VideoView(async () => polishVideos(await YoutubeAPI.getVideosInfo()));
videoView에서 인자로 api함수를 받을 필요가 없고 인스턴스를 import해서 사용하면되죠. 또한 videoView에서 youtubeAPI 함수를 멤버변수로 가지고 있을 필요가 없습니다. 어떤것을 클래스의 멤버변수로 가지고 있어야하는지도 같이 생각해보면 좋을듯합니다!

---

[#141, 콤피, early return](https://github.com/woowacourse/javascript-youtube-classroom/pull/141)

```javascript
// before
handleVideoCheckButtonClick = e => {
    if (e.target.classList.contains('video-item__check-button')) {

// refactor
if (!e.target.classList.contains('video-item__check-button')) {
    return;
}
```

---

### 네이밍

[#133, 우연, 변수 네이밍](https://github.com/woowacourse/javascript-youtube-classroom/pull/133)
변수인데 동사로 이름이 지어져있네요!

```javascript
// before
const findSameKindVideos = videos.filter((video) =>
  this.#isValidVideo(kind, video.watched)
);

// refactor
const sameKindVideos = videos.filter((video) =>
  this.#isValidVideo(kind, video.watched)
);
```

---

### DOM

[#148, 후이, 데이터 바인딩](https://github.com/woowacourse/javascript-youtube-classroom/pull/148)
[#133, 우연, 데이터 바인딩](https://github.com/woowacourse/javascript-youtube-classroom/pull/133)

```javascript
// issue
 #makeVideoDataObject(element, children) {
    return {
      id: element.dataset.videoId,
      thumbnail: children[0].currentSrc,
      title: children[1].textContent,
      channelTitle: children[2].textContent,
      date: children[3].textContent,
      saved: children[4].textContent,
      watched: false,
    }
 }
```

검색된 결과로 반환된 데이터들을 멤버변수(상태)로 저장하지 않고 바로 화면에 렌더링하고 있습니다. 화면에는 그려졌지만 메모리(변수)에는 없는거죠. 그러다보니 save를 하게되는 경우에 dom에 접근해서 데이터를 추출하게 됩니다.
만약 검색된 결과를 정렬해야하는 필터 기능이 추가되야 한다면 어떻게 될까요? 화면내 모든 리스트에 접근해서 데이터를 추출하고 다시 가공하는 상황이 일어납니다. 멤버변수로 데이터를 가지고 있다면 바로 정렬하고 dom에 반영하기만 하면되죠.
