# 로또
## 진행 방법
* 로또 요구사항을 파악한다.
* 요구사항에 대한 구현을 완료한 후 자신의 github 아이디에 해당하는 브랜치에 Pull Request(이하 PR)를 통해 코드 리뷰 요청을 한다.
* 코드 리뷰 피드백에 대한 개선 작업을 하고 다시 PUSH한다.
* 모든 피드백을 완료하면 다음 단계를 도전하고 앞의 과정을 반복한다.

## 온라인 코드 리뷰 과정
* [텍스트와 이미지로 살펴보는 온라인 코드 리뷰 과정](https://github.com/next-step/nextstep-docs/tree/master/codereview)

<h3>첫번째 구현_요구사항</h3>
/*
* final 상수 적극 활용하기!
* Test Case 통과에 집중함.
*
* 1. 빈 문자열 또는 null 값을 입력할 경우 0을 반환해야 한다.(예 : “” => 0, null => 0)
* 2. 숫자 하나를 문자열로 입력할 경우 해당 숫자를 반환한다.(예 : “1”)
* 3. 숫자 두개를 컴마(,) 구분자로 입력할 경우 두 숫자의 합을 반환한다.(예 : “1,2”)
* 4. 구분자를 컴마(,) 이외에 콜론(:)을 사용할 수 있다. (예 : “1,2:3” => 6)
* 5. “//”와 “\n” 문자 사이에 커스텀 구분자를 지정할 수 있다. (예 : “//;\n1;2;3” => 6)
* 6. 음수를 전달할 경우 RuntimeException 예외가 발생해야 한다. (예 : “-1,2,3”)
* */


<h3>두번째 구현</h3>
* CLASS변수 함부로 선언하지 말기
  * [메모리낭비, 불변성 보장못하기 때문] -> 여러 method에서 공유하는 값이라면, return값을 제대로 보내서 값 갱신하자.
  * [public -> private] -> 다른 CLASS에서 함부로 접근해도 상관 X?, 해당 CLASS에서만 사용할꺼면 제대로 private선언해서 접근 막아주자.
* 직관적인 변수, 파라미터명 사용하기.
* 1 Method는 1가지의 work만! 그것이 설령 NULL체크만 하더라도 분리시켜야한다.
* 매직넘버 사용하지 않고, static final을 활용하여 상수로 선언한다.
* Pattern.compile()은 되게 느림 -> "//(.)\n(.*)" 해당 정규식은 잘라내는 로직때문에 compile()을 써야하지만 정규식 검증만 하고 싶은거라면 matches()가 훨씬 가볍고 빠름.
  * 또한 정해져있는 정규식에 대한 Patterun객체를 생성하고 싶은거라면 class 변수로 Pattern인스턴스를 생성해두는것이 훨씬 빠르다.
* RuntimeException은 너무 광범위하다..! 보다 디테일한 Exception종료를 예외처리 할 수 있도록 고민해보자!