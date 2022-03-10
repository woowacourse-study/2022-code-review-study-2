# Level-2 로또 Step1(81, 82, 87, 90, 112, 113, 116, 119) - 앨버
- 분석 담당 코드
    - [#136](https://github.com/woowacourse/javascript-lotto/pull/136)
    - [#120](https://github.com/woowacourse/javascript-lotto/pull/120)
    - [#132](https://github.com/woowacourse/javascript-lotto/pull/132)
    - [#138](https://github.com/woowacourse/javascript-lotto/pull/138)
    - [#141](https://github.com/woowacourse/javascript-lotto/pull/141)
    - [#121](https://github.com/woowacourse/javascript-lotto/pull/121)
    - [#133](https://github.com/woowacourse/javascript-lotto/pull/133)
    - [#150](https://github.com/woowacourse/javascript-lotto/pull/150)



<br>

## 피드백 정리
### 대분류(ex: 아키텍처, 함수/클래스, 컨벤션, DOM, 테스트 등)
- [[#132](https://github.com/woowacourse/javascript-lotto/pull/132#discussion_r819360517) - 클래스 내 변수 선언] 

  ```javascript
	constructor() {
	this.$coverTheBackground = null;
	this.$lottoResultSection = null;
	this.$restartButton = null;
	this.$lottoListToggleButton = null;
	}
  ```
  
	위처럼 클래스 내부에서 null로 초기화 해줄 필요가 없다. 어차피 constructor에서 모두 `undefined`로 초기화되기 때문

<br>


- [[#138](https://github.com/woowacourse/javascript-lotto/pull/138#discussion_r819526399) - 로또 당첨 결과 순위 계산하는 로직]

	```javascript
	const result = [0, 0, 0, 0, 0];
	```
	위처럼 단순히 인덱스로 순위를 유추하는 것보다는 {first, second: 0, ... } 와 같이 객체를 사용하는 것이 사용하거나 읽을 때도 명확하게 순위까지 알 수 있을 것 같다.

<br>

- [[#138](https://github.com/woowacourse/javascript-lotto/pull/138#discussion_r819525674) - 함수 및 변수 네이밍]

	```javascript
	const result = totalWinningCount(lottoList.getPurchasedLotto(), winningNumber, bonusNumber);	
	```

	`totalWinningXXX 앞에 get 이라는 이름을 붙여 함수라는 사실을 알기 쉽게 해주면 좋겠고, result ...보단 좀 더 명확한 네이밍을 가지면 좋겠어요ㅎㅎ`
	



<br>

- [[#141](https://github.com/woowacourse/javascript-lotto/pull/141#discussion_r820197575) - css]

	- css에서 수치를 표현할 때 1px 이하로는 표현을 못한다고 한다!


<br>

- [[#141](https://github.com/woowacourse/javascript-lotto/pull/141#discussion_r820113715) - html의 data attribute]

	>	일반적으로 html의 data attribute는 정적인 값 위주로 넣어주고,
	이 상황과 같이 style 처리를 위한 경우에는 class를 이용합니다.
	css에서 [data-invalid-state]와 같은 선택자는 class에 비해 성능이 떨어지기 때문입니다.

<br>

- [[#133](https://github.com/woowacourse/javascript-lotto/pull/133#discussion_r820814624) - 함수 네이밍]
  
	> handleEnter라는 메서드가 꼭 엔터를 누를 때가 아니라 버튼을 클릭할 때도 호출하고 있는데.
	차라리 어떤 기능을 수행하는지 드러나는 네이밍이 좋지 않을까요?

	함수 네이밍을 할 때 어떤 기능을 수행하는지를 보여줄 수 있으면 좋겠다.


