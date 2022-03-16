# Level1 나만의 유튜브 강의실 Step1 - 코카콜라

- [#77, 코카콜라](https://github.com/woowacourse/javascript-youtube-classroom/pull/77)
- [#105, 후이](https://github.com/woowacourse/javascript-youtube-classroom/pull/105)
- [#95, 콤피](https://github.com/woowacourse/javascript-youtube-classroom/pull/95)
- [#94, 민초](https://github.com/woowacourse/javascript-youtube-classroom/pull/94)
- [#109, 우연](https://github.com/woowacourse/javascript-youtube-classroom/pull/109)
- [#106, 아놀드](https://github.com/woowacourse/javascript-youtube-classroom/pull/106)
- [#79, 하리](https://github.com/woowacourse/javascript-youtube-classroom/pull/79)
- [#94, 민초](https://github.com/woowacourse/javascript-youtube-classroom/pull/94)

---

## 피드백 정리

### 함수/클래스

- [[#105, 후이](https://github.com/woowacourse/javascript-youtube-classroom/pull/105)] **JSON.parse() parse하지 못하는 값이 넘겨서 온다면 어떻게 될까요??**

> JSON.parse(text[, reviver])

- [text] JSON으로 변환할 문자열. JSON 구문은 JSON 객체의 설명을 참고하세요.
- [reviver Optional] 함수라면, 변환 결과를 반환하기 전에 이 인수에 전달해 변형함.
- [반환 값] 주어진 JSON 문자열에 대응하는 Object.
- [예외] 변환할 문자열이 유효한 JSON이 아닐 경우 SyntaxError.

```javascript
// 예외 case

// 후행 쉼표 사용 불가
// SyntaxError
JSON.parse("[1, 2, 3, 4, ]"); // SyntaxError JSON.parse: unexpected character
JSON.parse('{"foo" : 1, }'); // SyntaxError JSON.parse: unexpected character
JSON.parse('{"foo": 01}'); // SyntaxError: JSON.parse: expected ',' or '}' after property value
JSON.parse('{"foo": 1.}'); // SyntaxError: JSON.parse: unterminated fractional number
JSON.parse("{'foo': 1}"); // SyntaxError: JSON.parse: expected property name or '}'
JSON.parse('{"test":"테스트\r\n테스트\r\n테스트\r\n테스트\r\n"}'); // SyntaxError: JSON.parse: Unexpected token in JSON, 특정문자(\r, \n, \t, \f)

// refactor
JSON.parse("[1, 2, 3, 4]");
JSON.parse('{"foo" : 1 }');
JSON.parse('{"foo": 1}');
JSON.parse('{"foo": 1}');
JSON.parse('{"foo": 1}');
JSON.parse('{"test":"테스트 테스트 테스트 테스트"}');
console.log(
  JSON.parse('{"test":"테스트\\r\\n테스트\\r\\n테스트\\r\\n테스트\\r\\n"}') // {test: '테스트\r\n테스트\r\n테스트\r\n테스트\r\n'}
); //
```

---

- [[#105, 후이](https://github.com/woowacourse/javascript-youtube-classroom/pull/105)] **굳이 bindEvent를 따로 뺄 필요는 없다고 생각하는데 후이님은 어떻게 생각하시나요?**

```javascript
bindEvents() {
    this.parentElement.addEventListener('click', this.storeIDHandler.bind(this));
  }
```

bindEvent를 따로 빼게 되는 경우

1. 클래스 인스턴스를 만들게 될때 멤버변수와 멤버함수를 가지고 메모리에 올라가게 됩니다. 최초 실행 이후 더이상 실행되지 않는 멤버함수를 계속 들고 있을 필요가 없다고 판단됩니다.
2. 생성자 호출이후 bindEvent를 stack에 할당하고 호출하는데 이 또한 1번처럼 굳이 한번 더 할 필요없느 불필요한 과정이라고 생각합니다.
3. bindEvent를 private으로 은닉하지 않음으로서 메소드가 노출되고 외부에서 잘못 사용할 여지가 있습니다.
   (1번과 2번은 지나친 성능 고려이긴 합니다)

한편 여러 줄이여서 길어진다면 주석을 활용하여 구분, 줄바꿈을 통해서 구분, 새로운 메소드를 활용하여 구분할 수 있습니다. 이부분은 개발자마다 다르겠지만 이때는 bindEvent를 메소드를 따로 빼도 괜찮다고 생각합니다.

해당 일관성을 지키는게 개발생산성에 크게 유의미한것 같지 않으며, bindEvent가 없어도 의미를 전달하는것은 문제가 없어보입니다

---

- [[#105, 후이](https://github.com/woowacourse/javascript-youtube-classroom/pull/105)] **button의 default type은 무엇인가요??**

button의 type에는 3가지 값을 지정해 줄 수 있는데 각각 submit, reset, button입니다.
만약 아무런 값도 지정하지 않았다면 기본값은 submit이 됩니다.

따라서 아래와 같다.

```
<button></button> === <button type="submit"></button>
```

IE에서의 default type은 'button', 다른 브라우저에서는 'submit'이다.
그러므로 단순 버튼에는 type="button"을 명시해주는 것이 좋겠다.

---

- [[#95, 콤피](https://github.com/woowacourse/javascript-youtube-classroom/pull/95)] **bind(this) 대신 handler로 등록할 메소드들을 class field (arrow function)으로 전환하시는걸 추천합니다.**

```javascript
// before
$(".dimmer").addEventListener("click", this.closeModal.bind(this));

closeModal(e) { ... }

// refactor
$('.dimmer').addEventListener('click', this.closeModal);

closeModal = (e) => { ... }
```

메소드 선언 방식에 의하면 prototype에 원본메소드가 남아있는 채로, 실제로 호출되는건 새로 만들어진 bound 메소드입니다. 사용하지 않을 불필요한 메소드가 남아있다는 뜻이죠. 반면 class field를 이용하면 prototype에는 남아있지 않고, 인스턴스 자신이 사용할 함수만 들고 있게 됩니다.
