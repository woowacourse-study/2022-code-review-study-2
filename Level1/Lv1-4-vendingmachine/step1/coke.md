# Level1 자판기 미션 Step1 - 코카콜라

- [#1, 코카콜라](https://github.com/woowacourse/javascript-vendingmachine/pull/1)
- [#2, 유세지](https://github.com/woowacourse/javascript-vendingmachine/pull/2)
- [#20, 소피아](https://github.com/woowacourse/javascript-vendingmachine/pull/20)
- [#15, 콤피](https://github.com/woowacourse/javascript-vendingmachine/pull/15)
- [#28, 도리](https://github.com/woowacourse/javascript-vendingmachine/pull/28)
- [#33, 우디](https://github.com/woowacourse/javascript-vendingmachine/pull/33)
- [#35, 아놀드](https://github.com/woowacourse/javascript-vendingmachine/pull/35)
- [#5, 해리](https://github.com/woowacourse/javascript-vendingmachine/pull/5)
- [#16, 돔하디](https://github.com/woowacourse/javascript-vendingmachine/pull/16)
- [#9, 마르코](https://github.com/woowacourse/javascript-vendingmachine/pull/9)

---

## 피드백 정리

### 함수/클래스

- [#1, 코카콜라, model에서 범용적 성향의 메소드 분리](https://github.com/woowacourse/javascript-vendingmachine/pull/1)

```javascript
getRandomInt(max: number) {
    return Math.floor(Math.random() * max);
}
```

서로 생각을 공유하고 공부하고 좋은 모임이네요:)
좋은 질문 덕분에 저도 생각을 해봤네요. 질문을 듣고 어디에 분리하는게 맞을까 생각하다가 '이 함수를 함수로 만들 필요가 있을까' 생각이 들었습니다. 지금 상황에서 어느곳에도 '재사용이 되지 않고' 이름과 의미를 부여하기 위해서 함수로 만들었습니다. 저도 랜덤로직을 보통 그렇게 만들었고요. 근데 Math.floor(Math.random() \* max) 가 정말 그렇게 복잡한 로직인가?? 그리고 함수호출 비용을 들이면서까지 이걸 함수로 만들어야 하나 생각이 드네요. 그래서 함수로 만들지 않을것 같습니다.

만약 함수로 만든다면 콜라님처럼 2번으로 뺄것 같습니다. 전역함수를 만드는것은 신중해야된다고 생각합니다. 전역함수를 만드게 된다면 프로그램 전체에 퍼지게 됩니다. 그러한 상황에서 해당 함수를 고치게 되는 경우가 발생할 수 있겠죠. 파라미터를 고치거나 내부 로직을 살짝 변경하는등.. 그러면 그걸 호출하는 쪽에서 확인을 해야하는 과정이 필요한데 전역에 퍼져있기 때문에 시간이 오래 걸리고 불안하죠.

---

### CSS

- [#1, 코카콜라, CSS parsing 최적화](https://github.com/woowacourse/javascript-vendingmachine/pull/1)

```css
/* src/css/index.css */

#product-list li input {
  ...;
}
```

1. 선택자가 돔 구조에 의존하게 됩니다
2. 아이디를 사용하고 요소를 선택함으로서 우선순위가 꽤 높습니다. CSS의 이름은 Cascading입니다. cascading이 될 여지에 대해서도 생각해야 합니다. class를 부여하여도 스타일을 오버라이드할 수 없고 id + class 합쳐서 오버라이드 해야합니다. 되도록 class를 사용하여 선택자 우선 순위를 낮게 유지하는게 좋습니다.
3. css 선택자의 파싱은 'right to left parsing'입니다. 위와 같이 선택자를 적는다면 브라우저는 요소를 더 탐색하겠죠(물론 브라우저나 컴퓨터의 성능이 워낙 좋고 측정된 수치를 보지못하여 3개는 지나친 걱정일수도 있습니다)

[Which styles render faster? - Website Performance Optimization](https://www.youtube.com/watch?v=gkTy6G4FtMg&list=PLAwxTw4SYaPmKmNX-INgcxQWf30KuWa_A&index=21)
[Why do browsers match CSS selectors from right to left?](https://stackoverflow.com/questions/5797014/why-do-browsers-match-css-selectors-from-right-to-left)
[How CSS is parsed | It's right to left | Know why?](https://www.youtube.com/watch?v=pWM9eXfgMLc)

---

- [#2, 유세지, 한번에 속성 설정](https://github.com/woowacourse/javascript-vendingmachine/pull/2)

```css
/* before */

#change-list-wrapper ul {
  font-family: "Roboto";
}

li {
  font-family: "Roboto";
}

/* refactor */

* {
  font-family: inherit;
}

body {
  font-family: "Roboto";
}
```

- 텍스트가 연관되어있는 폰트를 전부 font-family: 'Roboto' 하거나,
- body에서 한번에 내려주는게 좋다.

---

### 테스트

- [#35, 아놀드, 테스트 코드 의존성 제거](https://github.com/woowacourse/javascript-vendingmachine/pull/35)

```javascript
describe('동전 충전 테스트', () => {
  let vendingMachine: VendingMachine;

  beforeEach(() => {
    vendingMachine = new VendingMachineImpl();
  });
```

---

### 기타

- [#2, 유세지, 메타태그](https://github.com/woowacourse/javascript-vendingmachine/pull/2)

```
<!DOCTYPE html>
<html lang="ko">


<head>
    <meta charset="UTF-8" />
    <title>자판기</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
```

`<meta>` 태그는 문서 레벨 메타데이터 요소
모바일에서 보이는 크기와 배율을 설정할 수 있는 태그다.

---

- [#33, 우디, custom-elements](https://github.com/woowacourse/javascript-vendingmachine/pull/33)
  [custom-elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements)

```javascript
 }
}

customElements.define('item-row', ItemRow, { extends: 'tr' });
```

리뷰어: custom-elements 에 대해서 잘 몰라 질문을 드립니다! extends 는 보통 어떤 경우에 사용되나요?

```javascript
<table>
  ...
  <tbody>
    <item-row></item-row>
  <tbody>
</table>
```

우디: 위와 같이 사용을 하고 싶었는데 { extends: 'tr' } 옵션 없이는 테이블이 로우로 인식을 못하더라구요. HTMLTableRowElement를 상속하고 무조건 저 옵션을 붙여야 테이블 로우가 제대로 렌더링이 되었습니다. 커스텀엘리먼츠에 제약사항이 많은 것 같아 좀 아쉽네요. 2단계, 그리고 앞으로는 커스텀 엘리먼츠를 잘 사용하지 않을 것 같습니다.
