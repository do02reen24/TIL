# 📚 TypeScript

## 📌 TypeScript란?

- 자바스크립트에 타입을 부여한 언어
- 자바스크립트와 달리 브라우저에서 실행하려면 파일을 한번 변환(컴파일)해주어야 한다.
- 사용 이유
  - **에러의 사전방지** : 의도하지 않은 코드의 동작을 예방할 수 있다.
  - 코드 가이드 및 자동 완성(**개발 생산성 향상**) : VSCode에서 해당 타입에 대한 API를 미리보기로 띄워줄 수 있고, 따라서 API를 다 일일이 치는 것이 아니라 tab으로 빠르고 정확하게 작성해나갈 수 있다.

## 📌 기본 타입

> `:`를 이용하여 자바스크립트 코드에 타입을 정의하는 방식을 타입 표기(Type Annotation)라고 한다.

- String

  ```ts
  let str: string = 'hi';
  ```

- Boolean

  ```ts
  let isLoggedIn: boolean = false;
  ```

- Number

  ```ts
  let num: number = 10;
  ```

- Object

- Array

  ```ts
  let arr: number[] = [1,2,3];
  ```

  ```ts
  let arr: Array<number> = [1,2,3];
  ```

- Tuple 

  - 배열의 길이가 고정되고 각 요소의 타입이 지정되어 있는 배열 형식
  - 정의하지 않은 타입, 인덱스로 접근할 경우 오류가 발생한다.

  ```ts
  let arr: [string, number] = ['hi', 10];
  ```

- Enum

  - 특정 값(상수)들의 집합을 의미한다.

  ```ts
  enum Avengers { Capt, IronMan, Thor }
  let hero: Avengers = Avengers.Capt;
  ```

  - 인덱스 번호로도 접근할 수 있다.

  ```ts
  enum Avengers { Capt, IronMan, Thor }
  let hero: Avengers = Avengers[0];
  ```

  - 이넘의 인덱스를 사용자 편의로 변경하여 사용할 수도 있다.

  ```ts
  enum Avengers { Capt = 2, IronMan, Thor }
  let hero: Avengers = Avengers[2]; // Capt
  let hero: Avengers = Avengers[4]; // Thor
  ```

- Any

  - 모든 타입에 대해서 허용한다는 의미를 갖고 있다.

  ```ts
  let str: any = 'hi';
  let num: any = 10;
  let arr: any = ['a', 2, true];
  ```

- Void

  - 변수에는 `undefined`와 `null`만 할당하고, 함수에는 반환 값을 설정할 수 없는 타입

  ```ts
  let unuseful: void = undefined;
  function notuse(): void {
    console.log('sth');
  }
  ```

- Null

- Undefined

- Never

  - 함수의 끝에 절대 도달하지 않는다는 의미를 지닌 타입
  - (절대 함수의 끝까지 실행되지 않는다는 의미)

## 📌 함수

- 타입스크립트에서는 함수의 인자를 모두 필수 값으로 간주한다. 즉, 정의된 매개변수의 값만 받을 수 있고 추가로 인자를 받을 수 없다는 의미이다. 이 특성은 정의된 매개변수의 개수만큼 인자를 넘기지 않아도 되는 자바스크립트의 특성과는 반대된다. 이런 특성을 살리고 싶다면 `?` 를 사용하면 된다.
- 매개변수 초기화는 ES6 문법과 동일하다.

## 📌 인터페이스

```ts
interface 인터페이스_이름 {
  속성: 타입;
}
```

- 인터페이스는 상호 간에 정의한 약속 혹은 규칙을 의미한다.

- 타입스크립트에서의 인터페이스는 보통 다음과 같은 범주에 대해 약속을 정의한다.

  - 객체의 스펙(속성과 속성의 타입)
  - 함수의 파라미터
  - 함수의 스펙(파라미터, 반환 타입 등)
  - 배열과 객체를 접근하는 방식
  - 클래스

- 인터페이스를 인자로 받아 사용할 때 항상 인터페이스의 속성 개수와 인자로 받는 객체의 속성 개수를 일치시키지 않아도 된다.

- 인터페이스에 정의된 속성, 타입의 조건만 만족한다면 객체의 속성 개수가 더 많아도 상관 없다.

- 인터페이스에 선언된 속성 순서를 지키지 않아도 된다.

- **옵션 속성(`?`)**

  - 단순히 인터페이스를 사용할 때 속성을 선택적으로 적용할 수 있다는 것 뿐만 아니라 인터페이스에 정의되어 있지 않은 속성에 대해서 인지시켜줄 수 있다.

- **읽기 전용 속성(`readonly`)**

  - 읽기 전용 속성은 인터페이스로 객체를 처음 생성할 때만 값을 할당하고 그 이후에는 변경할 수 없는 속성을 의미한다.

  ```ts
  interface CraftBeer {
    readonly brand: string;
  }
  ```

  - 배열을 선언할 때 `ReadonlyArray<T>` 타입을 사용하면 읽기 전용 배열을 생성할 수 있다. `ReadonlyArray`로 선언하면 배열의 내용을 변경할 수 없다.

- 객체 선언과 관련된 타입 체킹

  - 타입스크립트는 인터페이스를 이용하여 객체를 선언할 때 좀 더 엄밀한 속성 검사를 진행한다.

  - 타입 추론을 무시하고 싶다면 아래와 같이 선언한다.

    ```ts
    interface CraftBeer {
      brand?: string;
    }
    
    function brewBeer(beer: CraftBeer) {
      // ..
    }
    
    let myBeer = { brandon: 'what' }';
    brewBeer(myBeer as CraftBeer);
    ```

  * 인터페이스에서 정의하지 않은 속성들을 추가로 사용하고 싶을 때는 아래와 같은 방법을 사용한다.

    ```ts
    interface CraftBeer {
      brand?: string;
      [propName: string]: any;
    }
    ```

- 클래스 타입

  - 타입스크립트에서도 클래스가 일정 조건을 만족하도록 타입 규칙을 정의할 수 있다.

    ```ts
    interface CraftBeer {
      beerName: string;
      nameBeer(beer: string): void;
    }
    
    class myBeer implements CraftBeer {
      beerName: string = 'Baby Guinness';
      nameBeer(b: string) {
        this.beerName = b;
      }
      constructor() {}
    }
    ```

  - 클래스와 마찬가지로 인터페이스도 인터페이스 간 확장이 가능하다.

    ```ts
    interface Person {
      name: string;
    }
    interface Developer extends Person {
      skill: string;
    }
    let fe = {} as Developer;
    fe.name = 'josh';
    fe.skill = 'TypeScript';
    ```

* 하이브리드 타입

  * 자바스크립트의 유연하고 동적인 타입 특성에 따라 인터페이스 역시 여러가지 타입을 조합하여 만들 수 있다.

    ```ts
    interface CraftBeer {
      (beer: string): string;
      brand: string;
      brew(): void;
    }
    
    function myBeer(): CraftBeer {
      let my = (function(beer: string) {}) as CraftBeer;
      my.brand = 'Beer Kitchen';
      my.brew = function() {};
      return my;
    }
    
    let brewedBeer = myBeer();
    brewedBeer('My First Beer');
    brewedBeer.brand = 'Pangyo Craft';
    brewedBeer.brew();
    ```

## 📌 이넘

- 특정 값들의 집합을 의미하는 자료형

- 타입스크립트에서는 문자형 이넘과 숫자형 이넘을 지원한다.

- 숫자형 이넘

  ```ts
  enum Direction {
    Up = 1,
    Down,
    Left,
    Right
  }
  ```

  * 숫자형 이넘을 선언할 때 초기 값을 주면 초기 값부터 차례로 1씩 증가한다.
  * 초기 값을 주지 않으면 0부터 차례로 1씩 증가한다.

- 문자형 이넘

  ```ts
  enum Direction {
      Up = "UP",
      Down = "DOWN",
      Left = "LEFT",
      Right = "RIGHT",
  }
  ```

  - 문자형 이넘은 이넘 값 전부 다 특정 문자 또는 다른 이넘 값으로 초기화 해줘야 한다.

- 복합 이넘

  - 기술적으로 이넘에 문자와 숫자를 혼합하여 생성할 수 있다. (하지만 권장되는 방법은 아니다.)

- 런타임 시점에서의 이넘 특징

  - 이넘은 런타임시에 실제 객체 형태로 존재하게 된다.

- 컴파일 시점에서의 이넘 특징

  - 이넘이 런타임 시점에서는 실제 객체지만 `keyof` 를 사용할 때 주의해야 한다.
  - 일반적으로 `keyof`를 사용해야 되는 상황에서는 `keyof typeof`를 사용해라.

  ```ts
  enum LogLevel {
    ERROR, WARN, INFO, DEBUG
  }
  
  // 'ERROR' | 'WARN' | 'INFO' | 'DEBUG';
  type LogLevelStrings = keyof typeof LogLevel;
  
  function printImportant(key: LogLevelStrings, message: string) {
      const num = LogLevel[key];
      if (num <= LogLevel.WARN) {
         console.log('Log level key is: ', key);
         console.log('Log level value is: ', num);
         console.log('Log level message is: ', message);
      }
  }
  printImportant('ERROR', 'This is a message');
  ```

* 리버스 매핑

  * 리버스 매핑은 숫자형 이넘에만 존재하는 특징이다.
  * 이넘의 key로 value를 얻을 수 있고 value로 key를 얻을 수도 있다.

  ```ts
  enum Enum {
    A
  }
  let a = Enum.A; // 키로 값을 획득 하기
  let keyName = Enum[a]; // 값으로 키를 획득 하기
  ```

## 📌 연산자를 이용한 타입 정의

- Union Type
  - JS의 OR 연산자(`||`)와 같이 A이거나 B이다 라는 의미의 타입이다.
  -  `|` 연산자를 이용하여 타입을 여러 개 연결하는 방식

- Intersection Type

  - 여러 타입을 모두 만족하는 하나의 타입

  ```ts
  interface Person {
    name: string;
    age: number;
  }
  interface Developer {
    name: string;
    skill: number;
  }
  type Capt = Person & Developer;
  ```

  ```ts
  {
    name: string;
    age: number;
    skill: string;
  }
  ```
  - `&` 연산자를 이용해 여러 개의 타입 정의를 하나로 합치는 방식

- Union Type을 쓸 때 주의할 점

  ```ts
  interface Person {
    name: string;
    age: number;
  }
  interface Developer {
    name: string;
    skill: string;
  }
  function introduce(someone: Person | Developer) {
    someone.name; // O 정상 동작
    someone.age; // X 타입 오류
    someone.skill; // X 타입 오류
  }
  ```

  - 어느 타입이 들어오든 간에 오류가 안 나는 방향으로 타입을 추론하게 된다.
  - 별도의 타입 가드를 이용하여 타입의 범위를 좁히지 않는 이상 기본적으로 두 타입에 공통적으로 들어있는 속성에만 접근할 수 있게 된다.

## 📌 클래스

- Abstract Class : 추상 클래스는 특정 클래스의 상속 대상이 되는 클래스이며 좀 더 상위 레벨에서 속성, 메서드의 모양을 정의한다.

  ```ts
  abstract class Developer {
    abstract coding(): void; // 'abstract'가 붙으면 상속 받은 클래스에서 무조건 구현해야 함
    drink(): void {
      console.log('drink sth');
    }
  }
  
  class FrontEndDeveloper extends Developer {
    coding(): void {
      // Developer 클래스를 상속 받은 클래스에서 무조건 정의해야 하는 메서드
      console.log('develop web');
    }
    design(): void {
      console.log('design web');
    }
  }
  const dev = new Developer(); // error: cannot create an instance of an abstract class
  const josh = new FrontEndDeveloper();
  josh.coding(); // develop web
  josh.drink(); // drink sth
  josh.design(); // design web
  ```

## 📌 제네릭

- 재사용성이 높은 컴포넌트를 만들 때 자주 활용한다.

- 한가지 타입보다 여러가지 타입에서 동작하는 컴포넌트를 생성하는데 사용된다.

- **제네릭**이란 타입을 마치 함수의 파라미터처럼 사용하는 것을 의미한다.

  ```ts
  function getText<T>(text: T): T {
    return text;
  }
  ```

  배열을 받고 싶은 경우

  ```ts
  function logText<T>(text: T[]): T[] {
    console.log(text.length); // 제네릭 타입이 배열이기 때문에 `length`를 허용합니다.
    return text;
  }
  ```

  ```ts
  function logText<T>(text: Array<T>): Array<T> {
    console.log(text.length);
    return text;
  }
  ```

* 제네릭 타입

  ```ts
  function logText<T>(text: T): T {
    return text;
  }
  // #1
  let str: <T>(text: T) => T = logText;
  // #2
  let str: {<T>(text: T): T} = logText;
  ```

  ```ts
  interface GenericLogTextFn {
    <T>(text: T): T;
  }
  function logText<T>(text: T): T {
    return text;
  }
  let myString: GenericLogTextFn = logText; // Okay
  ```

* 제네릭 클래스

  ```ts
  class GenericMath<T> {
    pi: T;
    sum: (x: T, y: T) => T;
  }
  
  let math = new GenericMath<number>();
  ```

* 제네릭 제약 조건

  제네릭 함수에 어느 정도 타입 힌트를 줄 수 있는 방법이 있다.

  ```ts
  interface LengthWise {
    length: number;
  }
  
  function logText<T extends LengthWise>(text: T): T {
    console.log(text.length);
    return text;
  }
  ```

* 객체의 속성을 제약하는 방법

  ```ts
  function getProperty<T, O extends keyof T>(obj: T, key: O) {
    return obj[key];  
  }
  let obj = { a: 1, b: 2, c: 3 };
  
  getProperty(obj, "a"); // okay
  getProperty(obj, "z"); // error: "z"는 "a", "b", "c" 속성에 해당하지 않습니다.
  ```

## 📌 타입 추론

- 타입 추론이란 타입스크립트가 코드를 해석해 나가는 동작을 의미한다.
- 변수 선언, 변수 초기화, 속성, 인자의 기본 값, 함수의 반환 값 등을 설정할 때 타입 추론이 일어난다.

## 📌 타입 별칭

- 타입 별칭은 특정 타입이나 인터페이스를 참조할 수 있는 타입 변수를 의미한다.
- `interface`나 제네릭에도 타입 별칭을 사용할 수 있다.
- 타입 별칭은 새로운 타입 값을 하나 생성하는 것이 아니라 정의한 타입에 대해 나중에 쉽게 참고할 수 있게 이름을 부여하는 것이다.
- `type` vs `interface`
  - 타입 별칭과 인터페이스의 가장 큰 차이점은 타입의 확장 가능 / 불가능 여부입니다. 인터페이스는 확장이 가능한데 반해 타입 별칭은 확장이 불가능합니다. 따라서, 가능한한 `type` 보다는 `interface`로 선언해서 사용하는 것을 추천합니다.

## 💌 참고

* [TypeScript Handbook](https://www.typescriptlang.org/ko/docs/handbook/intro.html)

* [타입스크립트 핸드북](https://joshua1988.github.io/ts/)