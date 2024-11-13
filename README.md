# 스프링 MVC 2편 - 백엔드 웹 개발 활용 기술

## 1. 타임리프 기본 기능
### 타임리프 소개
Thymeleaf는 웹과 독립형 환경 모두를 위한 최신 서버 사이드 Java 템플릿 엔진이다.

Tymeleaf의 주요 목표는 개발 워크플로우에 우아하고 자연스러운 템플릿을 제공하는 것이다.

즉, 브라우저에서 올바르게 표시될 수 있고 정적 프로토타입으로도 작동하는 HTML을 제공하여 개발팀에서 더욱 긴밀한 협업을 가능하게 한다.

Spring Framework용 모둘과 즐겨쓰는 도구와의 다양한 통합 기능, 그리고 사용자가 직접 만든 기능을 플러그인으로 추가할 수 있는 기능을 갖춘 
Thymeleaf는 최신 HTML5 JVM웹 개발에 이상적이다.

### 타임리프 특징
- 서버 사이드 HTML 렌더링 (SSR)
  - 타임리프는 백엔드 서버에서 HTML을 동적으로 렌더링 하는 용도로 사용된다.
- 네츄럴 템플릿
  - 타임리프로 작성한 파일은 HTML을 유지하기 때문에 웹 브라우저에서 파일을 직접 열어도 내용을 확인할 수 있고, 서버를 통해 뷰 템플릿을 거치면 동적으로 변경된 결과를 확인할 수 있다.
- 스프링 통합 지원
  - 타임리프는 스프링과 자연스럽게 통합되고, 스프링의 다양한 기능을 편리하게 사용할 수 있게 지원한다.

### 타임리프 기본 기능
- 타임리프 사용 선언: \<html xmlns:th="http://www.thymeleaf.org">
- 기본 표현식(간단한 표현)
  - 변순 표현식: ${...}
  - 선택 변수 표현식: *{...}
  - 메시지 표현식: #{...}
  - 링크 URL 표현식: @{...}
  - 조각 표현식: ~{...}
- 기본 표힌식(리터럴)
  - 텍스트: 'text'
  - 숫자: 0, 1, 2
  - 불린: true, false
  - 널: null
  - 리터럴 토큰: one, sometext
- 기본 표현식(문자 연산)
  - 문자 합치기: +
  - 리터럴 대체: |The name is ${name}|
- 기본 표현식(산술 연산)
  - Binary operators: +, -, *, /, %
  - Minus sign(unary operator): -
- 기본 표현식(불린 연산)
  - Binary operators: and, or
  - Boolean negation(unary operator): !, not
- 기본 표현식(비교와 동등)
  - 비교: >, <, >=, <= (gt, lt, ge, le)
  - 동등연산: ==, != (eq ne)
- 기본 표현식(조건 연산)
  - If-then: (if) ? (then)
  - If-then-else: (if) ? (then) : (else)
  - Default: (value) ?: (defaultValue)
- 기본 표현식(특별한 토큰)
  - No-Operation: _

### 텍스트 - text, utext
타입리프의 가장 기본 기능인 텍스트를 출력하는 기능
- HTML의 콘텐츠에 데이터를 출력하는 경우
  - `th:text`
  - `<span th:text="${data}">`
- HTML 태그 속성이 아닌 HTML 콘텐츠 영역안에 직접 데이터 출력
  - `[[...]]`
  - `[[$data]]`
#### Escape
타임리프가 제공하는 `th:text`, `[[...]]` 는 기본적으로 이스케이프를 제공한다.
#### Unescape
이스케이프 기능을 사용하지 않으려면 `th:utext`, `[(...)]`을 사용한다.

### 변수 - SrpingEL
타임리프에서 변수를 사용할 때는 변수 표현식을 사용한다. `${...}`
- SpringEL 다양한 표현식 사용 (user, users, userMap)
  - Object
    - user.username
    - user['username']
    - user.getUsername
  - List
    - users[0].username
    - users[0]['username']
    - users[0].getUsername
  - Map
    - userMap['userA'].username
    - userMap['userA'].['username']
    - userMap['userA'].getUsername()

#### 지역 변수 선언
`th:with`를 사용하면 지역 변수를 선언해서 사용할 수 있다. `th:with="first=${users[0}"`

### 기본 객체들
타임리프는 기본 객체들을 제공한다.
- ${#request} - 스프링 부트 3.0부터 제공하지 않는다.
- ${#response} - 스프링 부트 3.0부터 제공하지 않는다.
- ${#session} - 스프링 부트 3.0부터 제공하지 않는다.
- ${#servletContext} - 스프링 부트 3.0부터 제공하지 않는다.
- ${#locale}

###  유틸리티 객체와 날짜
타임리프는 문자, 숫자, 날짜, URI 등을 편리하게 다루는 다양한 유틸리티 객체를 제공한다.
* #message : 메시지, 국제화 처리
* #uris : URI 이스케이프 지원
* #dates : java.util.Date 서식 지원
* #calendars : java.util.Calendar 서식 지원
* #temporals : 자바8 날짜 서식 지원
* #numbers : 숫자 서식 지원
* #strings : 문자 관련 편의 기능
* #objects : 객체 관련 기능 제공
* #bools : boolean 관련 기능 제공
* #arrays : 배열 관련 기능 제공
* #lists , #sets , #maps : 컬렉션 관련 기능 제공
* #ids : 아이디 처리 관련 기능 제공, 뒤에서 설명

### URL 링크
타임리프에서 URL을 생성할 때는 `@{...}` 문법을 사용한다.
- 단순한 URL: `@{/hello}` -> `/hello`
- 쿼리 파라미터
  - `@{/hello(param1=${param1}, param2=${param2})}` -> `/hello?param1=data1&param2=data2`
  - `()`에 있는 부분은 쿼리 파라미터로 처리된다.
- 경로 변수
  - `@{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})}` -> `/hello/data1/data2`
  - URL 경로상 변수가 있으면 `()`부분은 경로 변수로 처리된다.
- 경로 변수 + 쿼리 파라미터
  - `@{/hello/{param1}(param1=${param1}, param2=${param2})}` -> `/hello/data1?param2=data2`
  - 경로 변수와 쿼리 파라미터를 함꺼ㅔ 사용할 수 있다.

### 리터럴
리터럴은 소스 코드상에 고정된 값을 말하는 용어이다.
문자 리터럴은 원칙상 ' 로 감싸야 한다. 중간에 공백이 있어서 하나의 의미있는 토큰으로도 인식되지 않는다.
* 문자: 'hello'
* 숫자: 10
* 불린: true , false
* null: null

### 연산
타임리프의 연산은 자바와 크게 다르지 않다. HTML안에서 사용하기 때문에 HTML 엔티티를 사용하는 부분만 주의하면 좋다.

### 속성값 설정
타임리프는 주로 HTML 태그에 `th:*` 속성을 지정하는 방식으로 동작한다.

`th:*`로 속성을 적용하면 기존 속성을 대체한다. 기존 속성이 없으면 새로 만든다.

- 속성 추가
  - `th:attrappend` : 속성 값의 뒤에 값을 추가한다.
  - `th:attrprepend` : 속성 값의 앞에 값을 추가한다.
  - `th:classappend` : class 속성에 자연스럽게 추가한다
- checked 처리
  - HTML에서 `checked=false`인 경우에도 checked 속성이 있기 때문에 checked 처리가 되어버린다.
  - 이런 부분에서 `true`,`false` 값을 주로 사용하는 개발자 입장에서는 불편하다.
  - 타임리프의 `th:checked`는 값이 `false`인 경우 속성 자체를 제거한다.

### 반복
타임리프에서 반복은 `th:each`를 사용한다.
- `<tr th:each="user : ${users}">`
- 반복의 두번째 파라미터를 설정해서 반복의 상태를 확인할 수 있다.
  - `<tr th:each="user, userStat : ${users}">`
  - 두번째 파라미터는 생략 가능한데 생략하면 지정한 변수명 + Stat 으로 지정된다.
  - index : 0부터 시작하는 값
  - count : 1부터 시작하는 값
  - size : 전체 사이즈
  - even , odd : 홀수, 짝수 여부( boolean )
  - first , last :처음, 마지막 여부( boolean )
  - current : 현재 객체

### 조건부 평가
타임 리프의 조건식 `th:if`, `th:unless`, `th:switch`, `th:case="*"`

타임리프는 해당 조건이 맞지 않으면 태그 자체를 렌더링 하지 않는다.

### 주석
1. 표준 HTML 주석 `<!-- -->`: 표준 HTML 주석은 타임리프가 렌더링 하지 않고 그대로 남겨둔다.
2. 타임리프 파서 주석 `<!--/* */-->`: 타임리프 파서 주석은 타임리프의 진짜 주석이다. 렌더링에서 주석 부분을 제거한다.
3. 타임리프 프로토타입 주석 `<!--/*/ /*/-->`: HTML파일을 그대로 열면 렌더링하지 않고 타임리프 렌더링을 거치면 정상 렌더링 된다.

### 블록
`th:block`은 HTML 태그가 아닌 타임리프의 유일한 자체 태그다. 렌더링시 제거된다.

### 자바스크립트 인라인
타임리프는 자바 스크립트에서 타임리프를 편리하게 사용할 수 있는 자바 스크립트 인라인 기능을 제공한다.

`<script th:inline="javascript">`

#### 텍스트 렌더링
인라인 사용하면 문자타입인 경우 `"`를 포함해준다. 추가로 자바스크립트에서 문제가 될 수 있는 문자가 포함되어 있으면 이스케이프 처리도 해준다.

#### 자바스크립트 내추럴 템플릿
타임리프는 HTML 파일을 직접 열어도 동작하는 네추럴 템플릿 기능을 제공한다. 자바스크립트 인라인 기능을 사용하면 주석을 활용해서 이 기능을 사용할 수 있다.
인라인 사용하지 않으면 정말 순수하게 그대로 해석을 해버려 내추럴 템플릿 기능이 동작하지 않는다.

#### 객체
타임리프의 자바스크립트 인라인 기능을 사용하면 객체를 JSON으로 자동 변환해준다.

### 템플릿 조각, 레이아웃
웹 페이지를 개발할 때는 공통 영역이 많이 있다. 예를 들어서 상단 영역이나 하단 영역, 좌측 카테고리 등등 여러 페이지에서 함께 사용하는 영역들이 있다.
이런 부분을 복사해서 사용한다면 변경시 여러 페이지를 다 수정해야 하므로 상당히 비효율 적이다. 타임리프는 문제 해결을 위해 템플릿 조각과 레이아웃 기능을 지원한다.

