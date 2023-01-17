# Javascript-Functional-Programming
함수형 자바스크립트 프로그래밍 책을 읽고 공부한 내용을 기록하는 저장소 입니다!

=======
# Javascript-Functional-Programming
함수형 자바스크립트 프로그래밍 책을 읽고 공부한 내용을 기록하는 저장소 입니다!

# 들어가기에 앞서
## 함수형 프로그래밍이란 무엇인가?
> **부수효과를 미워하고 조합성을 강조하는 프로그래밍 패러다임**

각각의 의미를 살펴보자.
* *부수효과를 미워함* : **순수함수**를 만든다.
* *조합성을 강조한다* : **모듈화 수준**을 높인다.

이를 조금 더 살펴보자면,
* *순수함수* : 오류를 줄이고, 안정성은 높인다.
* *모듈화 수준이 높다* : 생산성이 높다! (사용하기가 쉬워요~)

=> 순수 함수의 예시
```
function add(a,b) {
	return a + b;
};
console.log(add(1,2)); // 3
console.log(add(1,2)); // 3
```
함수 add는 a와 b에 같은 값이 전달되면 항상 같은 값을 반환한다.

하지만 다음과 같은 경우를 살펴보자.
```
let c = 3;
function add2(a,b) {
	return a + b + c;
};

console.log(add2(1,2)); // 6
c = 4;
console.log(add2(1,2)); // 7
```
코드 중간에 c의 값이 4로 재할당 되었다. 이럴 경우 add2에 전달된 인자는 동일하지만, 다른 값을 반환한다.
인자가 같아도 리턴값이 다르기 떄문에, 이는 순수 함수라고 할 수 없다.

또한 다음과 같은 경우들도 순수함수라고 할 수 없다.
```
let c = 10;
function add3(a,b) {
	c = 20;
	return a + b;
};
// 같은 인자를 전달했을 때 반환값이 언제나 같지만, 외부의 변수 c의 값을 재할당 한다.
// 이렇게 외부의 값에 영향을 끼치는 걸 부수효과라고 하며, 부수효과가 있으면 순수함수가 아니다. 

let obj1 = {val : 10};
function add4(obj, b) {
	obj.val += b;
};
// 역시 외부 객체의 값에 변화를 준다. 따라서 순수함수가 아니다.
```

그런데 add4의 경우를 보면 한가지 의문이 생길 수 있다.

*오잉...그럼 객체의 값을 바꾸고 싶을 때는 순수함수를 못쓰는거 아님...?*

이럴 땐 다음과 같은 방법을 사용한다.
```
let obj2 = {val: 20};
function add5{obj, b} {
	return {val: obj.val + b};
};
let obj3 = add5{obj2, 5};
console.log(obj3.val); // 25
```
외부 객체의 값은 참조만 하고, 값이 바뀐 객체는 새로운 변수에 할당하는 방식으로 사용이 가능하다
---
순수함수의 가장 큰 장점은 *평가 시점이 상관이 없다는 점*이다.
add2 함수의 경우 변수 c가 재할당되는 시점 전후로 리턴값이 바뀌기 때문에 사용 시점을 주의해야 한다.
하지만 add1 함수는 코드의 어디서 실행하든 값이 같기 때문에, 코드의 어디서 실행해도 상관이 없고, 재사용성이 매우매우매우 높다!!!

=> 결국 이 특성을 활용해 효율적인 코드를 작성하는게 함수평 프로그래밍이라고 할 수 있다!!
___

**항상 기억해야 할 점은, '함수형 프로그래밍이 언제나 옳다' 라는 것은 아니고 단순히 프로그래밍 패러다임 중 하나라는 것**이다.

물론 새로 나온 만큼 장점이야 있겠지만...평소에 불편을 느끼면서도 머리로는 어떻게 할까 생각하지 못했던 부분들(예를 들면 위에서 말하는 평가 시점에 따라 바뀌는 함수...불편하다 느끼면서도 '휴.... 변수 선언을 어디서 하는지 신경써야지!' 라고만 생각했다.)에 대해서 배우는 과정같다. 잘 배워서 흡수했으면 좋겠다.

