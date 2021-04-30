# 📚 React

## 📌 React란?

- 사용자 인터페이스를 만들기 위한 JavaScript 라이브러리
- 선언형, 컴포넌트 기반

## 📌 함수형 컴포넌트와 클래스형 컴포넌트

* 과거에는 클래스형 컴포넌트를 주로 사용했다. 2019년 v16.8부터 함수형 컴포넌트에 리액트 `훅(hook)`을 지원해주게 되면서 공식 문서에서 함수형 컴포넌트와 훅을 함께 사용할 것을 권장하고 있다.

### 선언방식

* 클래스형 컴포넌트

  ```jsx
  import React, { Component } from 'react';
  
  class App extends Component {
    render() {
      const name = '리액트';
      return <div>{name}</div>;
    }
  }
  
  export default App;
  ```

  * class 키워드 필요
  * Component를 상속 받아야 함.
  * `render()` 메소드가 반드시 있어야 함.

* 함수형 컴포넌트

  ```jsx
  import React from 'react';
  
  function App() {
    const name = '리액트';
    return <div>{name}</div>;
  }
  
  export default App;
  ```

### 차이점

* 클래스형 컴포넌트
  * state 기능 및 라이프 사이클 기능을 사용할 수 있으며 임의 메서드를 정의할 수 있다.
  * render 함수가 꼭 있어야 하며, 그 안에서 보여줘야할 JSX를 반환해야 한다.

* 함수형 컴포넌트
  * 클래스형 컴포넌트보다 선언하기 편하고, 메모리 자원을 덜 사용한다.
  * 과거에는 함수형 컴포넌트에서 state와 라이프사이클 API를 사용할 수 없다는 단점이 있었는데, 이는 리액트 훅이 도입되면서 해결되었다.

### 함수형 컴포넌트 선언

* 일반적인 함수 선언 방식과 ES6의 arrow function 방식이 존재한다.

* 일반 함수 선언 방식과 화살표 함수 선언 방식의 차이는 무엇일까?

  * 예제

  ```jsx
  function BlackDog() {
    this.name = '흰둥이';
    return {
      name: '검둥이',
      bark: function() {
        console.log(this.name + ': 멍멍!');
      }
    }
  }
  
  const blackDog = new Blackdog();
  blackDog.bark(); // 검둥이: 멍멍!
  
  function WhiteDog() {
    this.name = '흰둥이';
    return {
      name: '검둥이',
      bark: () => {
        console.log(this.name + ': 멍멍!');
      }
    }
  }
  
  const whiteDog = new Whitedog();
  whiteDog.bark(); // 흰둥이: 멍멍!
  ```

  🌟 **일반 함수는 자신이 종속된 객체를 this로 가리키며, 화살표 함수는 자신이 종속된 인스턴스를 가리킨다.**

### 기타

* 함수형 컴포넌트든 클래스형 컴포넌트든 state를 직접 조작하는 것이 아닌, setState나 useState와 같은 setter 함수를 반드시 사용해서 조작해야 한다.
* 클래스형 컴포넌트는 다른 말로 `Stateful 컴포넌트` , 함수형 컴포넌트는 `Stateless 컴포넌트` 라고 하기도 한다.
  * 클래스형 컴포넌트는 로직과 상태를 컴포넌트 내에서 구현하기 때문에 stateful로 불리는 것이며 상대적으로 복잡한 UI 로직을 가지고 있다.
  * 함수형 컴포넌트는 state를 사용하지 않고 단순하게 데이터를 받아서(props) UI에 뿌려주기 때문에 stateless라고 불리는 것이다.

### 정리

* 클래스형
  * state, lifeCycle 관련 기능 사용가능
  * 메모리 자원을 함수형 컴포넌트보다 조금 더 사용함.
  * 임의 메서드 정의 가능
* 함수형
  * state, lifeCycle 관련 기능 사용불가능 ➡ Hook을 통해서 해결
  * 메모리 자원을 클래스형 컴포넌트보다 덜 사용함.
  * 컴포넌트 선언이 편리

## 📌 Rendering Elements

* element는 React앱의 가장 작은 단위로 화면에 표시할 내용을 기술합니다.

### DOM에 엘리먼트 렌더링하기

* React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있다.

* React 엘리먼트를 루트 DOM 노드에 렌더링하려면 둘 다 [`ReactDOM.render()`](https://ko.reactjs.org/docs/react-dom.html#render)로 전달하면 된다.

  ```jsx
  const element = <h1>Hello, world</h1>;
  ReactDOM.render(element, document.getElementById('root'));
  ```

### 랜더링 된 엘리먼트 업데이트하기

* React 엘리먼트는 불변객체이다. 엘리먼트를 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할 수 없다.
* 지금까지의 내용을 바탕으로 하면 UI를 업데이트 하는 유일한 방법은 엘리먼트를 새로 생성하고 이를 `ReactDOM.render()`로 전달하는 것이다.

## 📌 Components 와 Props

* 컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 살펴볼 수 있다.

### 함수 컴포넌트와 클래스 컴포넌트

* 컴포넌트를 정의하는 가장 간단한 방법은 Javascript 함수를 작성하는 것이다.

  * 함수형 컴포넌트

  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```

  * 클래스형 컴포넌트

  ```jsx
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}</h1>;
    }
  }
  ```

### 컴포넌트 렌더링

* React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼 수 있습니다.

  ```jsx
  const element = <Welcome name="Sara" />;
  ```

* React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달한다. 이 객체를 “props”라고 한다.

* 예시) 페이지에 “Hello, Sara”를 렌더링

  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  
  const element = <Welcome name="Sara" />;
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
  ```

  1. `<Welcome name="Sara" />` 엘리먼트로 `ReactDOM.render()`를 호출합니다.
  2. React는 `{name: 'Sara'}`를 props로 하여 `Welcome` 컴포넌트를 호출합니다.
  3. `Welcome` 컴포넌트는 결과적으로 `<h1>Hello, Sara</h1>` 엘리먼트를 반환합니다.
  4. React DOM은 `<h1>Hello, Sara</h1>` 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트합니다.

  💥 **주의사항** 💥

  **컴포넌트의 이름은 항상 대문자로 시작한다.**

  React는 소문자로 시작하는 컴포넌트를 DOM 태그로 처리한다. 예를 들어 `<div />`는 HTML div 태그를 나타내지만, `<Welcome />`은 컴포넌트를 나타내며 범위 안에 `Welcome`이 있어야 한다.

### props는 읽기 전용

* 함수 컴포넌트나 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안된다.

  💥 **주의사항** 💥

  **모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다.**

## 📌 State 와 Lifecycle

> state는 클래스형 컴포넌트에서만 사용할 수 있고, 함수형 컴포넌트에서는 사용할 수 없다.

* state와 Lifecycle은 1초마다 실행되는 Clock 컴포넌트 예제를 통해 알아보도록 하자.

* 예제) Clock 컴포넌트

  ```jsx
  function Clock(props) {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
  
  function tick() {
    ReactDOM.render(
      <Clock date={new Date()} />,
      document.getElementById('root')
    );
  }
  
  setInterval(tick, 1000);
  ```

### 함수에서 클래스로 변환하기

다섯 단계로 `Clock`과 같은 함수 컴포넌트를 클래스로 변환할 수 있다.

1. `React.Component`를 확장하는 동일한 이름의 [ES6 class](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)를 생성한다.

2. `render()`라고 불리는 빈 메서드를 추가한다.

3. 함수의 내용을 `render()` 메서드 안으로 옮긴다.

4. `render()` 내용 안에 있는 `props`를 `this.props`로 변경한다.

5. 남아있는 빈 함수 선언을 삭제한다.

   ```jsx
   class Clock extends React.Component {
     render() {
       return (
         <div>
           <h1>Hello, world!</h1>
           <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
         </div>
       );
     }
   }
   ```

### 클래스에 로컬 State 추가하기

1. `render()` 메서드 안에 있는 `this.props.date`를 `this.state.date`로 변경합니다.

2. 초기 `this.state`를 지정하는 [class constructor](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes#Constructor_(생성자))를 추가합니다.

3. `<Clock />` 요소에서 `date` prop을 삭제합니다.

   ```jsx
   class Clock extends React.Component {
     constructor(props) {
       super(props);
       this.state = {date: new Date()};
     }
   
     render() {
       return (
         <div>
           <h1>Hello, world!</h1>
           <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
         </div>
       );
     }
   }
   
   ReactDOM.render(
     <Clock />,
     document.getElementById('root')
   );
   ```

### 생명주기 메서드를 클래스에 추가하기

* 많은 컴포넌트가 있는 애플리케이션에서 컴포넌트가 삭제될 때 해당 컴포넌트가 사용 중이던 리소스를 확보하는 것이 중요하다.
* `componentDidMount()` 메서드는 컴포넌트 출력물이 DOM에 렌더링 된 후에 실행된다.

1. `<Clock />`가 `ReactDOM.render()`로 전달되었을 때 React는 `Clock` 컴포넌트의 constructor를 호출합니다. `Clock`이 현재 시각을 표시해야 하기 때문에 현재 시각이 포함된 객체로 `this.state`를 초기화한다. 나중에 이 state를 업데이트할 것이다.

2. React는 `Clock` 컴포넌트의 `render()` 메서드를 호출한다. 이를 통해 React는 화면에 표시되어야 할 내용을 알게 된다. 그 다음 React는 `Clock`의 렌더링 출력값을 일치시키기 위해 DOM을 업데이트한다.

3. `Clock` 출력값이 DOM에 삽입되면, React는 `componentDidMount()` 생명주기 메서드를 호출한다. 그 안에서 `Clock` 컴포넌트는 매초 컴포넌트의 `tick()` 메서드를 호출하기 위한 타이머를 설정하도록 브라우저에 요청한다.

4. 매초 브라우저가 `tick()` 메서드를 호출한다. 그 안에서 `Clock` 컴포넌트는 `setState()`에 현재 시각을 포함하는 객체를 호출하면서 UI 업데이트를 진행한다. `setState()` 호출 덕분에 React는 state가 변경된 것을 인지하고 화면에 표시될 내용을 알아내기 위해 `render()` 메서드를 다시 호출합니다. 이 때 `render()` 메서드 안의 `this.state.date`가 달라지고 렌더링 출력값은 업데이트된 시각을 포함합니다. React는 이에 따라 DOM을 업데이트한다.

5. `Clock` 컴포넌트가 DOM으로부터 한 번이라도 삭제된 적이 있다면 React는 타이머를 멈추기 위해 `componentWillUnmount()` 생명주기 메서드를 호출한다.

   ```jsx
   class Clock extends React.Component {
     constructor(props) {
       super(props);
       this.state = {date: new Date()};
     }
   
     componentDidMount() {
       this.timerID = setInterval(
         () => this.tick(),
         1000
       );
     }
   
     componentWillUnmount() {
       clearInterval(this.timerID);
     }
   
     tick() {
       this.setState({
         date: new Date()
       });
     }
   
     render() {
       return (
         <div>
           <h1>Hello, world!</h1>
           <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
         </div>
       );
     }
   }
   
   ReactDOM.render(
     <Clock />,
     document.getElementById('root')
   );
   ```

### State를 올바르게 사용하기

1. 직접 state를 수정하지 않고, `setState()`를 사용하기!

   직접 state를 수정할 경우, 컴포넌트를 다시 렌더링하지 않는다.

   `this.state`를 지정할 수 있는 유일한 공간은 바로 constructor이다.

2. state 업데이트는 비동기적일 수도 있다.

   React는 성능을 위해 여러 `setState()` 호출을 단일 업데이트로 한꺼번에 처리할 수 있다.

   따라서 state를 업데이트 할 때, state 값에 의존하지 않도록 설계해야한다.

   **예시)**

   ```jsx
   // Wrong
   this.setState({
     counter: this.state.counter + this.props.increment,
   });
   ```

   위 코드는 업데이트에 실패할 수도 있기 때문에 인자로 넘겨주는 것이 좋다.

   ```jsx
   // Correct
   this.setState((state, props) => ({
     counter: state.counter + props.increment
   }));
   ```

3. state 업데이트는 병합된다.

   `setState()`를 호출할 때 React는 제공한 객체를 현재 state로 병합한다.

### 데이터는 아래로 흐른다

* state는 종종 로컬 또는 캡슐화라고 불린다.
* state가 소유하고 설정한 컴포넌트 이외에는 어떠한 컴포넌트에도 접근할 수 없다.
* 컴포넌트는 자신의 state를 자식 컴포넌트에 props로 전달할 수 있다.
* 하위 컴포넌트는 상위 컴포넌트의 state를 받을 수 있으나, 어디에서 왔는지는 알 수 없다.
* 일반적으로 이를 “하향식(top-down)” 또는 “단방향식” 데이터 흐름이라고 한다.
* 모든 state는 항상 특정한 컴포넌트가 소유하고 있으며 그 state로부터 파생된 UI 또는 데이터는 오직 트리구조에서 자신의 “아래”에 있는 컴포넌트에만 영향을 미친다.

## 📌 Events 처리하기

* React 엘리먼트에서 이벤트를 처리하는 방식은 DOM 엘리먼트에서 이벤트를 처리하는 방식과 매우 유사하다.

* React 엘리먼트의 문법 차이

  * React의 이벤트는 소문자 대신 캐멀 케이스(camelCase)를 사용한다.
  * JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러를 전달한다.

* 예제)

  * HTML

    ```html
    <button onclick="activateLasers()">
      Activate Lasers
    </button>
    ```

    ```html
    <a href="#" onclick="console.log('The link was clicked.'); return false">
      Click me
    </a>
    ```

  * React

    ```jsx
    <button onClick={activateLasers}>
      Activate Lasers
    </button>
    ```

    ```jsx
    function ActionLink() {
      function handleClick(e) {
        e.preventDefault();
        console.log('The link was clicked.');
      }
    
      return (
        <a href="#" onClick={handleClick}>
          Click me
        </a>
      );
    }
    ```

    🌟 React에서는 `false`를 반환해도 기본 동작을 방지할 수 없다. 반드시 `preventDefault`를 명시적으로 호출해야 한다. 

* React를 사용할 때 DOM 엘리먼트가 생성된 후 리스너를 추가하기 위해 `addEventListener`를 호출할 필요가 없다. 대신, 엘리먼트가 처음 렌더링될 때 리스너를 제공하면 된다.

## 📌 조건부 Rendering

* React에서는 원하는 동작을 캡슐화하는 컴포넌트를 만들 수 있다. 이렇게 하면 애플리케이션의 상태에 따라서 컴포넌트 중 몇 개만을 렌더링할 수 있다.

* React의 조건부 렌더링은 Javascript에서의 조건 처리 연산처리와 같이 동작한다.

* 예제) 로그인 여부에 따라 컴포넌트 중 하나를 보여주기

  ```jsx
  function UserGreeting(props) {
    return <h1>Welcome back!</h1>;
  }
  
  function GuestGreeting(props) {
    return <h1>Please sign up.</h1>;
  }
  
  function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;
    if (isLoggedIn) {
      return <UserGreeting />;
    }
    return <GuestGreeting />;
  }
  
  ReactDOM.render(
    // Try changing to isLoggedIn={true}:
    <Greeting isLoggedIn={false} />,
    document.getElementById('root')
  );
  ```

### 엘리먼트 변수

* 엘리먼트를 저장하기 위해 변수를 사용할 수 있다.
* 출력의 다른 부분은 변하지 않은 채로 컴포넌트의 일부를 조건부로 렌더링 할 수 있다.

### 논리 && 연산자로 If를 인라인으로 표현하기

* JSX의 표현식을 사용하여 엘리먼트를 쉽게 조건부로 표현할 수 있다.

  ```jsx
  function Mailbox(props) {
    const unreadMessages = props.unreadMessages;
    return (
      <div>
        <h1>Hello!</h1>
        {unreadMessages.length > 0 &&
          <h2>
            You have {unreadMessages.length} unread messages.
          </h2>
        }
      </div>
    );
  }
  
  const messages = ['React', 'Re: React', 'Re:Re: React'];
  ReactDOM.render(
    <Mailbox unreadMessages={messages} />,
    document.getElementById('root')
  );
  ```

### 조건부 연산자로 If-Else 구문 인라인으로 표현하기

* 엘리먼트를 조건부로 렌더링하는 다른 방법은 조건부 연산자인 `condition ? true : false` 를 사용하는 것이다.

* 예제)

  ```jsx
  render() {
    const isLoggedIn = this.state.isLoggedIn;
    return (
      <div>
        The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
      </div>
    );
  }
  ```

  ```jsx
  render() {
    const isLoggedIn = this.state.isLoggedIn;
    return (
      <div>
        {isLoggedIn
          ? <LogoutButton onClick={this.handleLogoutClick} />
          : <LoginButton onClick={this.handleLoginClick} />
        }
      </div>
    );
  }
  ```

### 컴포넌트가 렌더링하는 것을 막기

* 가끔 다른 컴포넌트에 의해 렌더링될 때 컴포넌트 자체를 숨기고 싶을 때는 렌더링 결과를 출력하는 대신 `null`을 반환하면 해결할 수 있다.

## 📌 Lists 와 Keys

### 여러개의 컴포넌트 렌더링 하기

* 엘리먼트 모음을 만들고 중괄호 `{}`를 이용하여 JSX에 포함시킬 수 있다.

* 예제)

  ```jsx
  const numbers = [1, 2, 3, 4, 5];
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
                                
  ReactDOM.render(
    <ul>{listItems}</ul>,
    document.getElementById('root')
  );
  ```

### 기본 리스트 컴포넌트

* 일반적으로 컴포넌트 안에서 리스트를 렌더링한다.

* 예제)

  ```jsx
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      <li>{number}</li>
    );
    return (
      <ul>{listItems}</ul>
    );
  }
  
  const numbers = [1, 2, 3, 4, 5];
  ReactDOM.render(
    <NumberList numbers={numbers} />,
    document.getElementById('root')
  );
  ```

  위 코드는 각 항목에 `key`를 넣어야 한다는 경고를 표시한다.

  🌟 **key** 는 엘리먼트 리스트를 만들 때 포함해야 하는 특수한 문자열 attribute 이다.

  ```jsx
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      <li key={number.toString()}>
        {number}
      </li>
    );
    return (
      <ul>{listItems}</ul>
    );
  }
  ```

  위와 같이 key를 지정해줄 수 있다.

### key

* key는 React가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 돕는다.
* key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 한다.
* Key를 선택하는 가장 좋은 방법은 리스트의 다른 항목들 사이에서 해당 항목을 고유하게 식별할 수 있는 문자열을 사용하는 것이다. 대부분의 경우 데이터의 ID를 key로 사용한다.
* 렌더링 한 항목에 대한 안정적인 ID가 없다면 최후의 수단으로 항목의 인덱스를 key로 사용할 수 있다.
  * 항목의 순서가 바뀔 수 있는 경우 key에 인덱스를 사용하는 것은 권장하지 않는다.
  * 이로 인해 성능이 저하되거나 컴포넌트의 state와 관련된 문제가 발생할 수 있다.

### Key로 컴포넌트 추출하기

* 키는 주변 배열의 context에서만 의미가 있습니다.

* 예시)

  * 예를 들어 `ListItem` 컴포넌트를 추출한 경우 `ListItem` 안에 있는 `<li>` 엘리먼트가 아니라 배열의 `<ListItem />` 엘리먼트가 key를 가져야 한다.

    ```jsx
    function ListItem(props) {
      const value = props.value;
      return (
        // 틀렸습니다! 여기에는 key를 지정할 필요가 없습니다.
        <li key={value.toString()}>
          {value}
        </li>
      );
    }
    
    function NumberList(props) {
      const numbers = props.numbers;
      const listItems = numbers.map((number) =>
        // 틀렸습니다! 여기에 key를 지정해야 합니다.
        <ListItem value={number} />
      );
      return (
        <ul>
          {listItems}
        </ul>
      );
    }
    
    const numbers = [1, 2, 3, 4, 5];
    ReactDOM.render(
      <NumberList numbers={numbers} />,
      document.getElementById('root')
    );
    ```

    ```jsx
    function ListItem(props) {
      // 맞습니다! 여기에는 key를 지정할 필요가 없습니다.
      return <li>{props.value}</li>;
    }
    
    function NumberList(props) {
      const numbers = props.numbers;
      const listItems = numbers.map((number) =>
        // 맞습니다! 배열 안에 key를 지정해야 합니다.
        <ListItem key={number.toString()} value={number} />
      );
      return (
        <ul>
          {listItems}
        </ul>
      );
    }
    
    const numbers = [1, 2, 3, 4, 5];
    ReactDOM.render(
      <NumberList numbers={numbers} />,
      document.getElementById('root')
    );
    ```

    🌟 `map()` 함수 내부에 있는 엘리먼트에 key를 넣어 주는 게 좋다.

### Key는 형제 사이에서만 고유한 값이어야 한다.

* Key는 배열 안에서 형제 사이에서 고유해야 하고 전체 범위에서 고유할 필요는 없다.
* 두 개의 다른 배열을 만들 때 동일한 key를 사용할 수 있다.

### JSX에 map() 포함시키기

* JSX를 사용하면 중괄호 안에 모든 표현식을 포함 시킬 수 있으므로 `map()` 함수의 결과를 인라인으로 처리할 수 있다.

## 📌 Forms

* HTML의 폼 엘리먼트는 폼 엘리먼트 자체가 내부 상태를 가지기 때문에 React의 다른 DOM 엘리먼트와는 조금 다르게 동작한다.
* HTML의 폼은 제출하면 새로운 페이지로 이동하는 기본 HTML 폼 동작을 수행한다.
* React에서 동일한 동작을 원하면 그냥 사용하면 된다.
  * 그러나 대부분의 경우, Javascript 함수로 폼의 제출을 처리하고 사용자가 폼에 입력한 데이터에 접근하도록 하는 것이 편리하다.
  * 이를 위한 표전 방식은 `제어 컴포넌트(controlled components)` 라고 불리는 기술을 이용하는 것이다.

### 제어 컴포넌트(Controlled Componenet)

* HTML에서 `<input>`, `<textarea>`, `<select>`와 같은 폼 엘리먼트는 일반적으로 사용자의 입력을 기반으로 자신의 state를 관리하고 업데이트한다.
* React에서는 변경할 수 있는 state가 일반적으로 컴포넌트의 state 속성에 유지되며 `setState()`에 의해 업데이트된다.

* 제어 컴포넌트를 사용하면, input의 값은 항상 React state에 의해 결정된다. (코드를 조금 더 작성해야 한다는 의미이지만,) 다른 UI 엘리먼트에 input의 값을 전달하거나 다른 이벤트 핸들러에서 값을 재설정할 수 있다.

### 다중 입력 제어하기

* 여러 `input` 엘리먼트를 제어해야할 때, 각 엘리먼트에 `name` 어트리뷰트를 추가하고 `event.target.name` 값을 통해 핸들러가 어떤 작업을 할 지 선택할 수 있게 해준다.

* 예시)

  ```jsx
  class Reservation extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        isGoing: true,
        numberOfGuests: 2
      };
  
      this.handleInputChange = this.handleInputChange.bind(this);
    }
  
    handleInputChange(event) {
      const target = event.target;
      const value = target.type === 'checkbox' ? target.checked : target.value;
      const name = target.name;
  
      this.setState({
        [name]: value
      });
    }
  
    render() {
      return (
        <form>
          <label>
            Is going:
            <input
              name="isGoing"
              type="checkbox"
              checked={this.state.isGoing}
              onChange={this.handleInputChange} />
          </label>
          <br />
          <label>
            Number of guests:
            <input
              name="numberOfGuests"
              type="number"
              value={this.state.numberOfGuests}
              onChange={this.handleInputChange} />
          </label>
        </form>
      );
    }
  }
  ```

## 📌 HOOKs API

### ✔ Hooks을 사용할 때의 장점

* React 컴포넌트를 개발할 때 클래스 방식의 컴포넌트를 사용하지 않아도 된다.
* 함수형태의 일관된 컴포넌트 표현이 가능하다.
* Life cycle 관리가 단순해진다.

-----

## 📌 Hook 파헤치기

### Hook의 등장

#### 재사용이 어려워요...

* 예전의 React에서는 컴포넌트에 재사용 가능한 행동을 붙이는 방법을 제공하지 않았다. 이것을 해결하기 위해서 render props, 고차 컴포넌트 같은 패턴이 등장했다. 하지만 이런 패턴을 사용할 때 컴포넌트를 재구성해야하며 코드 추적이 어렵다는 문제가 있었다.

* Hook을 사용하면 **컴포넌트로부터 상태 관련 로직을 추상화할 수 있다.** 
  * ➡ **Hook은 계층 변화 없이 상태 관련 로직을 재사용할 수 있도록 도와준다.**

#### 복잡한 컴포넌트를 이해하기 어려워요...

* 유지하기 힘든 상태 관련 로직들과 사이드 이펙트가 있는 컴포넌트들을 유지해야 할 때가 있다. 각 생명주기 메서드(`componentDidMount`, `componentDidUpdate` 등)에는 자주 관련 없는 로직들이 섞여 있다. 
  * ➡ 이로 인해 버그가 쉽게 발생하고 무결성을 쉽게 해친다.
* 이전에는 상태 관련 로직이 한 곳에 있기 때문에 컴포넌트를 작게 만들거나 테스트하는 것이 어려웠다. 많은 사람들은 이를 해결하기 위해 상태 관리 라이브러리를 사용했는데, 종종 상태 관련 라이브러리가 너무 많은 추성화를 하여 컴포넌트 재사용을 더욱 어렵게 만들기도 하였다.
* 이에 대한 해결책으로 생명주기 메서드를 기반으로 쪼개는 데 초점을 맞추기보다, **Hook을 통해 로직에 기반을 둔 작은 함수로 컴포넌트를 나눈다.**

#### Class로 인한 혼동...

* Class는 코드의 재사용성과 코드 구성을 어렵게 만든다.
  * Class는 잘 축소되지 않고, 핫 리로딩을 깨지기 쉽고 신뢰할 수 없게 만든다.
* 이에 대한 해결책으로 Hook은 Class 없이 React 기능들을 사용하는 방법들을 알려준다.
* 개념적으로 React 컴포넌트는 함수에 더 가깝다.

## 📌 Hook 개요

### Hook이 뭔가요?

* Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 **"연동(hook into)"** 할 수 있게 해주는 함수이다.
* Hook은 클래스 안에서 작동하지 않는다.
* React는 `useState` 같은 내장 Hook을 몇 가지 제공한다.
  * 컴포넌트 간에 상태 관련 로직을 재사용하기 위해 Hook을 직접 만드는 것도 가능하다.

### State Hook

* 예시

  ```jsx
  import React, { useState } from 'react';
  
  function Example() {
    // "count"라는 새 상태 변수를 선언합니다
    const [count, setCount] = useState(0);
  
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }
  ```

* `useState`는 *현재의* state 값과 이 값을 업데이트하는 함수를 쌍으로 제공한다.

* 이 함수를 이벤트 핸들러나 다른 곳에서 호출할 수 있다.

* 이것은 class의 `this.setState`와 거의 유사하지만, 이전 state와 새로운 state를 합치지 않는다는 차이점이 있다.

* `useState`는 인자로 초기 state 값을 하나 받는다.

* 하나의 컴포넌트 내에서 State Hook을 여러 개 사용할 수도 있다.

  ```jsx
  function ExampleWithManyStates() {
    // 상태 변수를 여러 개 선언했습니다!
    const [age, setAge] = useState(42);
    const [fruit, setFruit] = useState('banana');
    const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
    // ...
  }
  ```

### Effect Hook

* React 컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 작업을 "side effects" 라고 한다.

  * 다른 컴포넌트에 영향을 줄 수도 있고, 렌더링 과정에서 구현할 수 없는 작업이기 때문이다.

* Effect Hook, 즉 `useEffect`는 함수 컴포넌트 내에서 이런 side effects를 수행할 수 있게 해준다.

  * React class의 `componentDidMount` 나 `componentDidUpdate`, `componentWillUnmount`와 같은 목적으로 제공되지만, 하나의 API로 통합된 것이다.

* 예시

  ```jsx
  import React, { useState, useEffect } from 'react';
  
  function Example() {
    const [count, setCount] = useState(0);
  
    // componentDidMount, componentDidUpdate와 비슷합니다
    useEffect(() => {
      // 브라우저 API를 이용해 문서의 타이틀을 업데이트합니다
      document.title = `You clicked ${count} times`;
    });
  
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }
  ```

* `useEffect`를 사용하면, **React는 DOM을 바꾼 뒤에 “effect” 함수를 실행한다.**

* Effects는 컴포넌트 안에 선언되어있기 때문에 props와 state에 접근할 수 있다.

* 기본적으로 React는 매 렌더링 이후에 effects를 실행한다. (첫 번째 렌더링도 포함한다.)

* Effect를 “해제”할 필요가 있다면, 해제하는 함수를 반환해주면 된다. 이는 선택적이다(optional). 

* `useState`와 마찬가지로 컴포넌트 내에서 여러 개의 effect를 사용할 수 있다.

* Hook을 사용하면 구독을 추가하고 제거하는 로직과 같이 서로 관련 있는 코드들을 한군데에 모아서 작성할 수 있다.

  * 반면 class 컴포넌트에서는 생명주기 메서드(lifecycle methods) 각각에 쪼개서 넣어야만 했다.

### 🌟 Hook 사용 규칙

- **최상위(at the top level)**에서만 Hook을 호출해야 힌다. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하지 말아야 한다.
- **React 함수 컴포넌트** 내에서만 Hook을 호출해야 한다. 일반 JavaScript 함수에서는 Hook을 호출해서는 안 된다.
  - Hook을 호출할 수 있는 곳이 딱 한 군데 더 있는데 바로 직접 작성한 **custom Hook** 내이다.

### 나만의 Hook 만들기

* 컴포넌트 간에 상태 관련 로직을 재사용하려면 기존에는 `higher-order components` 와 `render props` 를 사용하였다. Custom Hook에서는 이 둘과 달리 컴포넌트 트리에 새 텀포넌트를 추가하지 않고 이것을 가능하게 할 수 있다.
* 각 컴포넌트의 state는 완전히 독립적이다.
* Hook은 state 그 자체가 아니라, *상태 관련 로직*을 재사용하는 방법이다.
* 실제로 각각의 Hook *호출*은 완전히 독립된 state를 가진다. 그래서 심지어는 한 컴포넌트 안에서 같은 custom Hook을 두 번 쓸 수도 있다.
* Custom Hook은 기능이라기보다는 컨벤션(convention)에 가깝다. **이름이 ”`use`“로 시작하고, 안에서 다른 Hook을 호출한다면 그 함수를 custom Hook이라고 부를 수 있다.**

### 기타 내장 Hook

* `useContext` : 컴포넌트를 중첩하지 않고도 React context를 구독할 수 있게 해준다.
* `useReducer` : 복잡한 컴포넌트들의 state를 reducer로 관리할 수 있게 해준다.

## 📌 State Hook 사용하기

### state 변수 선언하기

* 클래스에선 어떻게 사용했을까?

* 예시)

  ```jsx
  class Example extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        count: 0
      };
    }
  ```

   constructor 안에서 `this.state`를 `{ count: 0 }`로 설정함으로써 `count`를 `0`으로 초기화했다.

* 함수 컴포넌트는 this를 가질 수 없는데 어떻게 선언할까? `useState` Hook을 직접 컴포넌트에 호출한다.

* 예시)

  ```jsx
  import React, { useState } from 'react';
  
  function Example() {
    // 새로운 state 변수를 선언하고, 이것을 count라 부르겠습니다.
    const [count, setCount] = useState(0);
  ```

  * `useState`는 클래스 컴포넌트의 `this.state`가 제공하는 기능과 똑같다.
  * 일반적으로 일반 변수는 함수가 끝날 때 사라지지만, state 변수는 React에 의해 사라지지 않는다.
  * `useState()`Hook의 인자로 넘겨주는 값은 state의 초기 값이다.
  * 2개의 다른 변수를 저장하기를 원한다면 `useState()`를 두 번 호출해야 한다.
  * `useState`는 state 변수, 해당 변수를 갱신할 수 있는 함수 이 두 가지 쌍을 반환한다.
  * 예시에서 `count` 변수의 값을 갱신하려면 `setCount`를 호출하면 된다.

## 📌 Effect Hook 사용하기

* 데이터 가져오기, 구독(subscription) 설정하기, 수동으로 리액트 컴포넌트의 DOM을 수정하는 것까지 이 모든 것이 **side effects** 라고 한다.

* 🌟 리액트의 class 생명주기 메서드에 친숙하다면, `useEffect` Hook을 `componentDidMount`와 `componentDidUpdate`, `componentWillUnmount`가 합쳐진 것으로 생각해도 좋다.
* 리액트 컴포넌트에는 일반적으로 두 종류의 side effects가 있다.
  * 정리(clean-up)가 필요한 것
  * 정리(clean-up)가 필요하지 않은 것

### 정리(Clean-up)를 이용하지 않는 Effects

* **리액트가 DOM을 업데이트한 뒤 추가로 코드를 실행해야 하는 경우가 있다.**

  * 예시) 네트워크 리퀘스트, DOM 수동 조작, 로깅 등은 정리(clean-up) 등

*  Hook을 이용한 예시

  ```jsx
  import React, { useState, useEffect } from 'react';
  
  function Example() {
    const [count, setCount] = useState(0);
  
    useEffect(() => {
      document.title = `You clicked ${count} times`;
    });
  
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }
  ```

* useEffect Hook을 이용하여 우리는 리액트에게 컴포넌트가 렌더링 이후에 어떤 일을 수행해야하는 지 알려준다.

* `useEffect`를 컴포넌트 안에서 불러내는 이유는 무엇일까?
  * `useEffect`를 컴포넌트 내부에 둠으로써 effect를 통해 `count` state 변수(또는 그 어떤 prop에도)에 접근할 수 있게 된다.
  * 함수 범위 안에 존재하기 때문에 특별한 API 없이도 값을 얻을 수 있다.
  * Hook은 자바스크립트의 클로저를 이용하여 리액트에 한정된 API를 고안하는 것보다 자바스크립트가 이미 가지고 있는 방법을 이용하여 문제를 해결한다.
* `useEffect`는 기본적으로 첫번째 렌더링과 이후의 모든 업데이트에서 기본적으로 매번 수행된다.

### 정리(clean-up)를 이용하는 Effects

* 정리(clean-up)가 필요하지 않은 side effect를 보았지만, 정리(clean-up)가 필요한 effect도 있다.

  * 예로 외부 데이터에 **구독(subscription)을 설정해야 하는 경우**가 있다.

  * 이런 경우에 메모리 누수가 발생하지 않도록 정리(clean-up)하는 것은 매우 중요하다.

  * Hook을 이용한 예시

    ```jsx
    import React, { useState, useEffect } from 'react';
    
    function FriendStatus(props) {
      const [isOnline, setIsOnline] = useState(null);
    
      useEffect(() => {
        function handleStatusChange(status) {
          setIsOnline(status.isOnline);
        }
        ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
        // effect 이후에 어떻게 정리(clean-up)할 것인지 표시합니다.
        return function cleanup() {
          ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
        };
      });
    
      if (isOnline === null) {
        return 'Loading...';
      }
      return isOnline ? 'Online' : 'Offline';
    }
    ```

* **effect에서 함수를 반환하는 이유는 무엇일까?** 이는 effect를 위한 추가적인 정리(clean-up) 메커니즘이다.

  * 모든 effect는 정리를 위한 함수를 반환할 수 있다.
  * 이 점이 구독(subscription)의 추가와 제거를 위한 로직을 가까이 묶어둘 수 있게 한다.
  * 구독(subscription)의 추가와 제거가 모두 하나의 effect를 구성하는 것이다.

### 정리

* effect에 정리(clean-up)가 필요한 경우에는 함수를 반환합니다.
* 정리(clean-up)가 필요없는 경우에는 어떤 것도 반환하지 않습니다.

## 📌 Hook 규칙

### 최상위(at the Top Level)에서만 Hook을 호출해야 한다

* 반복문, 조건문 혹은 중첩된 함수 내에서 Hook을 호출하면 안된다.
  * 이 규칙을 따르면 컴포넌트가 렌더링 될 때마다 항상 동일한 순서로 Hook이 호출되는 것이 보장된다.
  * 이러한 점은 React가 `useState` 와 `useEffect` 가 여러 번 호출되는 중에도 Hook의 상태를 올바르게 유지할 수 있도록 해준다.

### 오직 React 함수 내에서 Hook을 호출해야 한다

- ✅ React 함수 컴포넌트에서 Hook을 호출하자.
- ✅ Custom Hook에서 Hook을 호출하자.

### 기타

* 모든 렌더링에서 Hook의 호출 순서는 같다.
* Hook에 조건문이나 반복문을 써서 호출을 뛰어넘게 되면 Hook 다음에 호출되는 Hook이 순서가 하나씩 밀리면서 버그를 발생시키게 된다. **이것이 컴포넌트 최상위(the top of level)에서 Hook이 호출되어야만 하는 이유이다.** 

## 📌 자신만의 Hook 만들기

* 자신만의 Hook을 만들면 컴포넌트 로직을 함수로 뽑아내어 재사용할 수 있다.

* **사용자 정의 Hook은 이름이 `use`로 시작하는 자바스크립트 함수이다. 사용자 Hook은 다른 Hook을 호출할 수 있다.** 

* 이름은 반드시 `use`로 시작해야 한다.
* 사용자 정의 Hook은 *상태 관련 로직*(구독을 설정하고 현재 변숫값을 기억하는 것)을 재사용하는 메커니즘이지만 사용자 Hook을 사용할 때마다 그 안의 state와 effect는 완전히 독립적이다.
* Hook은 함수이기 때문에 Hook 사이에서도 정보를 전달할 수 있다.

## 💌 참고

- [React](https://ko.reactjs.org/)