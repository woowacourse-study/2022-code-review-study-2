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

## 클로저란?

- 어떤 함수에서 선언한 변수를 참조하는 내부함수에서만 발생하는 현상!
- 선언될 당시의 LexicalEnvironment와의 상호관계

```javascript
// 외부 함수의 변수를 참조하는 내부 함수 1
var outer = function () {
  var a = 1;
  var inner = function () {
    console.log(++a);
  };
  inner();
};
outer(); // 2
```

outer함수의 실행 컨텍스트가 종료되면 LexicalEnvironment에 저장된 식별자들(a, inner)에 대한 참조를 지웁니다. 그러면 각 주소에 저장돼 있던 값들은 자신을 참조하는 변수가 하나도 없게 되므로 가비지 컬렉터의 수집이 대상이 될 것입니다.

```javascript
// 외부 함수의 변수를 참조하는 내부 함수 2
var outer = function () {
  var a = 1;
  var inner = function () {
    return ++a;
  };
  return inner; // inner 함수 자체를 반환
};
var outer2 = outer();
console.log(outer2()); // 2
console.log(outer2()); // 3
```

- outer함수의 실행 컨텍스트가 종료될 때, outer2 변수는 outer 함수의 실행 결과인 inner 함수를 참조하게 된다.
- outer함수는 이미 실행이 끝났는데 a 변수에 접근을 할수 있는가? inner함수가 a 변수를 참조하고 있기 때문에 outer 함수는 가비지컬렉터 의 수집 대상이 아니다.
- 가비지 컬렉터는 어떤 값을 참조한느 변수가 하나라도 있다면 그 값은 수집 대상에서 제외 한다.
- 즉, 클로저란? **어떤 함수 A에서 선언한 변수 a를 참조한느 내부함수 B를 외부로 전달할 경우 A의 실행 컨텍스트가 종료된 이후에도 변수 a가 사라지지 않는 현상을 말한다.**
- 클로저 현상에 의해 메모리에 남겨진 변수들의 집합

## 클로저 메모리

- 클로저는 어떤 필요에 의해 의도적으로 함수의 지역변수를 메모리를 소모하도록 함으로써 발생 시킨다.
- 그럼 그 필요성을 없에면 더이상 메모리를 소모 하지 않는다.
- 식별자에 참조형이 아닌 기본형 데이터(null, undefined)를 할당 하면 된다.

```javascript
var outer = function () {
  var a = 1;
  var inner = function () {
    return ++a;
  };
  return inner; // inner 함수 자체를 반환
};
var outer2 = outer();
outer2 = null;
```

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
