# Level1 유튜브 Step2(126, 127, 136, 143, 147, 150) - 시지프

분석 담당 코드

- [#143, 시지프](https://github.com/woowacourse/javascript-youtube-classroom/pull/143)
- [#151, 우디](https://github.com/woowacourse/javascript-youtube-classroom/pull/151)

- [#126, 블링](https://github.com/woowacourse/javascript-youtube-classroom/pull/126)
- [#149, 돔하디](https://github.com/woowacourse/javascript-youtube-classroom/pull/149)

- [#127, 도리](https://github.com/woowacourse/javascript-youtube-classroom/pull/127)
- [#136, 소피아](https://github.com/woowacourse/javascript-youtube-classroom/pull/136)

- [#147, 마르코](https://github.com/woowacourse/javascript-youtube-classroom/pull/147)
- [#150, 위니](https://github.com/woowacourse/javascript-youtube-classroom/pull/150)

## 로컬 스토리지 데이터를 어떻게 캡슐화하여 사용했지?

- 사람들은 클래스를 어떻게 정의하지? (클래스, 객체 사용 기준)

- [#126] ManageVideoStorage class 를 선언하여 각각의 video를 수정, 삭제, 저장하는 기능을 만들었다. 주입해주는 변수는 없다.

- [#127] SaveVideoManager class 를 선언하여 각각의 video를 수정, 삭제, 저장하는 기능을 만들었다. 주입해주는 변수는 없다.

- [#149] 객체로 선언하였음.

  ```javascript
  const storage = {
    getSavedVideos,
    addSavedVideos,
    isSavedVideo,
    setSavedVideos,
  };
  ```

## 사람들은 VideoCardList를 어떻게 재사용했지?

- [#126] videoCard를 재사용하고, button(저장, 시청 기록 기록, 삭제)만 따로 append 해주었다.

- [#127] 저장된 비디오, 모달 비디오 각각 정의

## try/catch는 어떻게 썼지?

- 메소드 전체를 try/catch 감싸야할까? 그러면 어디서 에러가 나는지 판단하기 어렵지 않을까?
- try/catch가 계속 전파되는 것 괜찮을까?

- [#126] 메소드 전체를 try catch로 감쌌다. 계속 전파시킨다.

- [#127, #149, #136] error 가 발생할 수 있는 부분에만 try/catch를 감싼다.

  ```javascript
    onSubmitSearchKeyword(e) {
    e.preventDefault();
    const keyword = $('#search-input-keyword').value;
    try {
      validateSearchKeyword(keyword);
    } catch ({ message }) {
      return alert(message);
    }
    this.searchOnSubmitKeyword(keyword);
  }
  ```

- [#147] try-catch가 촘촘히 있네요! 좋습니다!

```javascript
  async #searchVideo(event) {
    this.searchResultView.removeVideo();
    const { keyword } = event.detail;

    try {
      this.video.keyword = keyword;
    } catch (error) {
      this.mainView.toastNotification('error', error.message);
      return;
    }

    this.searchResultView.showSkeleton();
    const fetchedVideos = await fetchYoutubeApi(keyword);

    try {
      this.video.setVideoInfo(fetchedVideos);
    } catch (error) {
      this.searchResultView.removeVideo();
      this.searchResultView.showNotFound();
      this.mainView.toastNotification('error', error.message);
      return;
    }

    this.video.accumulateVideoItems();
    this.video.updateNewVideoItems();
    this.searchResultView.hideNotFound();

    try {
      this.searchResultView.renderVideo(this.video.newVideoItems);
    } catch (error) {
      this.searchResultView.hideSkeleton();
    }
    this.searchResultView.startObserve();
  }
```

- vs [#150]

  특히 한 메서드에서 try~catch구문이 2번이상 반복되는 경우 해당 메서드의 내용을 이해하는데 시간이 많이 걸리더라구요~!

## 이벤트 위임은 어떻게 했지?

- [#126] VideoCardList 전체가 아니라, 각각의 VideoCard 대해서 이벤트 적용. 이벤트 위임을 쓰긴 하였음.

## 에러 처리

- [#127] 오프라인 처리

  ```javascript
  window.addEventListener("offline", () => {
    showSnackbar(ALERT_MESSAGE.OFFLINE);
  });
  ```

## Model/View간 의존, View간의 의존은 어떻게 했지?

- [#126, #127] View간 의존. Model/View간 의존
- [#136] View에 Domain을 주입해주는 형태

  ```javascript
  const searchVideoManager = new SearchVideoManager({ storage });
  const saveVideoManager = new SaveVideoManager({ storage });

  const homeView = new HomeView({ saveVideoManager });
  const searchModalView = new SearchModalView({
    searchVideoManager,
    saveVideoManager,
  });
  ```

  - 주입하기 vs import 해서 사용하기
    - 주입을 해주면, 이 View은 이 Domain을 필요로 하는구나 하고 명확하게 인지할 수 있을 것이다.

## 코드 분석

## 피드백 정리

### 사용성

- [#127] .video-list 스타일을 홈에서 모달에서 둘 다 사용하고 있네요~
  그러다 보니 홈에서 볼/본 영상 리스트들도 2라인이 넘어가면 높이가 고정되고 내부 스크롤이 생기는데요.
  원래는 내부 스크롤 없이 리스트가 페이지에 쭉 나열되고 스크롤로 내리면 메뉴 바가 상단에 붙는 UI를 많이 쓰는데 지금은 그거까지 고려할 수는 없으니 😂 최소한 콘텐츠가 잘려보이지 않게 높이를 맞춰주는게 어떨 까요?

### 컨벤션

### 클린코드

- [#147] 클래스 내 변수, 메소드 정의 순서

  1. static public 상수
  2. static private 변수
  3. private instance 변수(public instance 변수가 필요한 경우는 거의 없음)
  4. public method
  5. private method는 자신을 호출하는 public method 직후에 위치

  ```javascript
  class A {
  	#myPrivateMember1;  // private instance 변수
  	#myPrivateMember2;

  	constructor() {       // 초기화
  	}

  	get myPrivateMember1() {    // getter와 setter들은 모두 같이 모아둔다.
  	}

  	set myPrivateMember1() {
    }

  	myPublicMethod1() {         // public 메서드
  			this.#myPrivateMehtod1();
  	}

    #myPrivateMethod1() {     // public에서 호출하는 private 메서드를 바로 다음에 선언
    }

  	myPublicMethod2() {         // 다른 public 메서드
  			this.#myPrivateMehtod2();
  	}

    #myPrivateMethod2() {
    }

  	static myStaticMethod() {   // static 메서드는 객체와 연관성이 제일 떨어지니까 마지막에 선언하거나 모듈화해서 extends해서 사용
  }
  ```

- [#150] for 문은 꼭 필요한 경우에만~
  Array.map이나 Array.forEach와 같은 내장 객체의 메서드로 구현할 수 있는 부분들이 for문으로 작성되어 있는 경우가 있는것 같아요. for문의 경우 휴먼 에러(사람의 실수)가 발생하기 쉽고, 읽는 사람도 조건을 이해하는데 시간이 많이 걸리는 경우도 있는것 같아요. 자바스크립트에서 제공해주는 유용한 메서드들을 더 잘 활용해서 더 읽기 좋은 코드를 만들어보는건 어떨까요~? 💪🏻

### 성능

### 설계

### JS

- [#136] JSON.parse는 Exception이 발생할 수 있습니다. 어떻게 처리하면 좋을까요?

  - 빈 배열을 반환하면서 console error 로그 남기기
  - 함수 사용부에서 처리할 수 있도록 커스텀 Error throw

  ```javascript
  const getData = (key) => JSON.parse(localStorage.getItem(key));

  #getLocalStorageVideos() {
    let videos;
    try {
      videos = getData('videos') || [];
    } catch (err) {
      videos = 'ERROR';
      this.#status = RESULT.FAIL;
      console.error(ERROR_MESSAGE.FAIL_TO_READ_SAVED_VIDEO_INFO);
      return [];
    }
    this.#status = RESULT.SUCCESS;
    return videos;
  }
  ```

- [#147] DOMContentLoaded event

  ```javascript
  window.addEventListener("DOMContentLoaded", new Controller());
  ```

  로딩이 다 된 후 자바스크립트 동작이 이뤄지는 것이 일반적이다.
  DOM 로딩이 다 되지 않았는데 DOM을 조작하는 자바스크립트 코드가 실행되면 원하는 결과를 내지 못할 것이다.
  DOMContentLoaded 이벤트로 이런 불상사를 막을 수 있다.
  DOMContentLoaded 이벤트는 DOM Tree 분석이 끝나면 발생한다.
  (load는 DOM Tree 외의 모든 자원이 다 받아져서 브라우저에 렌더링(화면 표시)까지 다 끝난 시점에 발생한다.)
  DOM Tree가 다 만들어진 후에 DOM API를 이용하여 DOM에 접근할 수 있기 때문에, 보통 자바스크립트 코드는 DOMContentLoaded 이후에 동작하도록 구현한다. 이 방법이 로딩 속도 성능에 유리하다고 생각하기 때문이다.

- [#147] method의 this를 binding하기 위하여 arrow function을 사용

  전략적으로 두 개를 사용할 수 있을 것 같아요~ 외부로 나가는 친구들은 this가 흩어질 수 있으니, arrow function으로 표기하고 내부 함수들은 #을 붙여 function으로 하는 형식등이요!

### 변수명

### 객체지향

- [#147] setter 에 대해서
  객체지향에서 말하길, setter와 getter에서 setter는 사용하지 않는걸 권장하고 있습니다.
  그 이유는 객체지향은 객체간 협력을 나타내는 것인데, setter는 객체간 협력보다는 "의존" 혹은 "명령"이거든요. ㅠㅠ

  예시를 들어볼께요.

  A와 B가 모래성을 쌓고 있어요. 이들은 멋진 모래성을 쌓는게 목표에요.
  그렇게 열심히 둘이 모래성을 쌓고 있는데, B가 실수로 A에게 파괴하라! 라고 명령(set)을 했어요.
  그래서 A는 모래성을 파괴해버렸죠.

  만약 setter를 안쓰고 행동 단위로 했다면 어땟을까요?

  A와 B는 C라는 목표를 달성하기 위해 행동하는 객체에요.
  C라는 목표를 모래성으로 설정하고. A와 B는 메소드로 PileUp() 이라는 메소드로 쌓을 수 있어요.
  PileUp(C)를 통해 C를 서로가 쌓을 수 있겠죠. 여기서 C가 B로 바뀌던 A로 바뀌던, 결국엔 쌓기만 하겠죠?
  쌓는 행위 외 다른 것들은 할 수 없으니 비교적 명령보다 안전할꺼에요.

  대략적으로 설명했는데, 대충 이렇습니다 :)
  그렇기 때문에 행동 단위로 하시는걸 추천드립니다 :)

### HTML 웹 표준

- [#127] <input type="search" name="q" >

  <input type=“search”>는 검색어를 입력할 수 있는 텍스트 필드를 정의합니다.

  검색 필드는 텍스트 필드와 기능적으로는 완전히 똑같지만, 브라우저에 의해 다르게 표현될 수 있습니다.
  검색 필드에는 반드시 name 속성을 설정해야 하며, name 속성이 설정되어 있지 않으면 서버로 제출되지 않을 것입니다.
  이때 가장 자주 사용되는 대표적인 name 속성값은 ‘q’입니다.

### CSS

- [#147] :(의사 클래스)와 ::(의사 요소)의 차이

  CSS3는 ::before이고 CSS2는 :before였네요. 브라우저에서는 콜론 하나는 CSS 의사 클래스에서 사용하고, 콜론 두 개는 CSS 의사 요소에서 사용하구요. 즉, CSS3에 들어서면서, CSS 의사 요소와 CSS 의사 클래스를 구분하기 위해, 콜론 두 개 ::before 구문을 도입했네요.
  아직 브라우저에서는 CSS2 구문인 :before도 아직 허용한다고 하지만, 의사 요소이므로 ::before 구문으로 사용해야겠네요.
  즉, CSS3 도입 취지에 부합하도록, 의사요소(:active, :hover 등)와 의사클래스(::before, ::after 등)를 구분하여 표시하도록 하는 게 중요하겠네요! 감사합니다.

### 테스트 코드

- [#136] cypress config로 baseUrl을 관리할 수 있습니다.

  ```json
  // cypress.json
  {
    "baseUrl": "http://localhost:9000/"
  }
  ```

  ```javascript
  // app.spec.js
  cy.visit("/");
  ```

## 기타 배울 점

## cypress test 를 잘 한 사람이 있는가?!

- [#136, 소피아]

  - cypress 내 함수 재사용
  - api mocking (intercept) 자유 자재로 사용
  - as, within, scrollTo, and, invoke 등 다양한 키워드 사용

  ```javascript
  // mocking, and
  it("정상적으로 검색이 끝나면, 검색 결과 리스트에 결과 아이템이 나타난다.", () => {
    // given
    cy.intercept("GET", "**/search*").as("getSearchResult");

    // when
    submitSearchKeywordCorrectly();
    cy.wait("@getSearchResult");

    // then
    cy.get(".video-item").should("have.length", 10).and("be.visible");
  });

  // scrollTo
  it("키워드 검색이 끝난 후, 검색 결과 리스트를 끝까지 스크롤하면 추가 로딩이 시작되며 스켈레톤 아이템이 나타난다.", () => {
    // given
    cy.intercept("GET", "**/search*").as("getSearchResult");

    // when
    submitSearchKeywordCorrectly();
    cy.wait("@getSearchResult");
    cy.get(".video-item").should("have.length", 10);
    cy.get("#search-result-video-list").scrollTo("bottom");

    // then
    cy.get(".skeleton").should("have.length", 10).and("be.visible");
  });

  it("스크롤에 의한 검색 결과 추가 로딩에 성공하면, 검색 결과 리스트에 결과 아이템이 추가된다.", () => {
    // given
    cy.intercept("GET", "**/search*").as("getSearchResult");

    // when
    submitSearchKeywordCorrectly();
    cy.wait("@getSearchResult");
    cy.get("#search-result-video-list").within(() => {
      cy.get(".video-item").should("have.length", 10);
    });
    cy.get("#search-result-video-list").scrollTo("bottom");
    cy.wait("@getSearchResult");

    // then
    cy.get(".video-item").should("have.length", 20).and("be.visible");
  });

  // mocking
  it("검색 과정에서 에러가 발생하면, 에러 안내 화면이 나온다.", () => {
    // given
    cy.intercept("GET", "**/search*", { statusCode: 404 });

    // when
    submitSearchKeywordCorrectly();

    // then
    cy.get("#no-result-description").should(
      "have.text",
      "검색 결과를 가져오는데 실패했습니다.관리자에게 문의하세요."
    );
  });

  // mocking
  it("검색 결과가 없는 경우, 검색 결과 없음 화면이 나온다.", () => {
    // given
    cy.intercept("GET", "**/search*", { items: [] });

    // when
    submitSearchKeywordCorrectly();

    // then
    cy.get("#no-result-description").should(
      "have.text",
      "검색 결과가 없습니다.다른 키워드로 검색해보세요."
    );
  });

  // invoke
  it("검색 결과의 영상 카드에서 저장 버튼을 누르면, 해당 영상이 볼 영상에 추가된다.", () => {
    // when
    const savedFirstVideo = saveFirstVideoInSearchResult();
    savedFirstVideo.invoke("attr", "data-id").then((savedVideoID) => {
      cy.get("#unwatched-video-list").within(() => {
        // then
        cy.get(".video-item").should("have.length", 1);
        cy.get(".video-item")
          .invoke("attr", "data-id")
          .should("eq", savedVideoID);
      });
    });
  });

  // @
  it("볼 영상의 영상 카드에서 ✅ 버튼을 클릭하면, 해당 영상 카드가 본 영상으로 이동한다.", () => {
    // when
    saveFirstVideoInSearchResult();

    cy.get("#unwatched-video-list").within(() => {
      cy.get(".video-item").as("unwatchedVideo");
      cy.get("@unwatchedVideo").within(() => {
        cy.get(".check-watched-button").click();
      });
    });

    cy.get("#watched-video-list-button").click();
    cy.get("#watched-video-list").within(() => {
      cy.get("@unwatchedVideo")
        .invoke("attr", "data-id")
        .then((checkedVideoID) => {
          // then
          cy.get(`[data-id=${checkedVideoID}]`)
            .should("exist")
            .and("be.visible");
        });
    });
  });
  ```
