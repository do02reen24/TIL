# 📚 SLASH 21

##  [🔗](https://www.youtube.com/watch?v=DHPeeEvDbdo) Micro-frontend React, 점진적으로 도입하기

> 주제: 토스팀에서 Django MVC 프로젝트가 Micro-frontend React  프로젝트로 탈바꿈하는 이야기

### 1. Django MVC 프로젝트에 점진적으로 React를 도입한 방법

* 빠르게 프로젝트를 도입하기 위해 `create-react-app`을 사용함 (추후 설정을 다시 바꿔야했기 때문에 좋지 않은 선택이었음)
* `webpack-bundle-tracker`와 `django-webpack-loader` 를 도입함.

### 2. 마이크로 프론트엔드 아키텍처를 도입한 이유와 후기

* 도입 이유: 높은 의존성과 긴 빌드 시간
  1. 기존의 거대한 소스 코드를 독립적인 패키지들로 분리(유지보수가 이루어지는 단위로 분리. 인프라 패키지, 라이브러리 패키지, 서비스 패키지)
  2. yarn2 Workspace Plugin을 통해 구현중

* 장점: 소스 코드부터 빌드 설정까지 완벽한 격리. 의존성 지옥 탈출.  빌드 속도 최적화

### 3. 프론트엔드 빌드 시간을 효과적으로  단축한 비법

* 빌드 시간을 줄이는 가장 좋은 방법? 빌드 자체를 하지 않는 것
* 소스 코드가 바뀐 패키지만 빌드하고 나머지는 기존 빌드 결과물을 재사용
* 소스 코드가 바뀌었는지는 어떻게 알 수 있을까? Git의 commit ID를 활용. 이전 커밋의 해시와 현재 커밋의 해시를 비교함.
* 기존  빌드 결과물을 Git에 압축하여 저장해두었음
* (Yarn2의 Zero-Installs이 동작하는 방식과 비슷함)
* 빌드 속도가 최대 15배까지 빨라지는 효과를 얻을 수 있었음

### 마이크로 프론트 아키텍처란?

* 마이크로 프론트엔드는 마이크로  서비스처럼 전체 화면을 작동할 수 있는 단위로 나누어 개발한 후 서로 조립하는 방식이다.
* 장점)
  * 작고, 응집력 있고 유지보수성을 가지는 코드베이스를 가질 수 있다.
  * 분리배포가 용이하고, 자율적인 팀 조직운영이 수월해진다.
  * 프론트엔드 개발을 점진적 업그레이드 또는 재작성이 수월해진다.
* 단점)
  * 배포 번들 사이즈가 커질 수 있다.
  * 서로 간의 개발 환경 차이로 복잡도가 올라간다.
  * 운영이 복잡해진다.

## [🔗](https://www.youtube.com/watch?v=FvRtoViujGg&t=9s) 프론트 엔드 웹 서비스에서 우아하게 비동기 처리하기

* 비동기 프로그래밍 > 순서가 보장되지 않은 상황
* async-await 코드의 장점: '성공하는 경우'만 다루고, '실패하는 경우'는 catch절에서 분리해 처리한다. '실패하는 경우'에 대한 처리를 외부에 위임할 수 있다.
* 좋은 코드의 특징)
  * 성공, 실패의 경우를 분리해 처리할 수 있다.
  * 비즈니스 로직을 한눈에 파악할 수 있다.
* 어려운 코드의 특징)
  * 실패, 성공의 경우가 서로 섞여 처리된다.
  * 비즈니스 로직을 파악하기 어렵다.
* 프론트엔드 웹 서비스에서 지금까지의 비동기 처리들은..?
  * 비동기를 처리하는 부분을 정의한다.
  * 컴포넌트에서 로딩과 에러 처리를 동시에 수행한다.
* React의 비동기 처리는 어렵다.
  * 성공하는 경우에만 집중해 컴포넌트를 구성하기 어렵다
  * 2개 이상의 비동기 로직이 개입할 때, 비즈니스 로직을 파악하기 점점 어려워진다.
* **React Suspense for Data Fetching**
  * 아직은 실험버전에서만 사용가능하다.
  * 목표)
    * 성공한 경우에만 집중할 수 있는
    * 로딩 상태와 에러 상태가 분리된
    * 동기와 거의  같게 사용할 수 있는
  * 에러 상태와 로딩 상태는 어떻게 분리되는가?
    * 컴포넌트를 '쓰는 쪽'에서 로딩 처리와 에러 처리를 한다.
    * 로딩 상태는 가장 가까운 'Suspense'의 'Fallback'으로 그려진다.
    * 에러 상태는 가장 가까운 'ErrorBoundary'가 componentDidCatch()로 처리한다.
  * React Suspense를 사용하면 로딩과 에러 처리를 바깥으로 위임하며 비동기 작업을 동기와 똑같이 처리할 수 있다.
* 웹 서비스의 코드 복잡도를 낮춘 방법
  * Hooks
    * 실제 상태 관리, 메모이제이션 등의 작업은 컴포넌트를 감싸는 React 프레임워크가 수행
  * Suspense
    * 실제 로딩 상태, 에러 상태 처리는 컴포넌트를 감싸는 부모 컴포넌트가 수행
  * try-catch
    * 실제 에러 처리는 컴포넌트를 감싸는 부모 함수가 수행
* 대수적 효과: 어떤 코드 조각을 감싸는 맥락으로 책임을 분리하는 방식
* 기타 공유하고 싶은 키워드: React Concurrent Mode, useTransition, useDeferredValue

## [🔗](https://www.youtube.com/watch?v=EP7g5R-7zwM) JavaScript Bundle Diet

* Bundle 사이즈가 중요한 이유: 웹사이트의 로딩 속도는 고객 획득에 영향을 준다.
* 바이트별로 보면, 자바스크립트는 같은 크기의 이미지나 웹폰트보다 브라우저가 처리하는 비용이 많이 든다.
* Bundle 사이즈 줄이기

### 1. 원인 찾기

* 용량이 큰 라이브러리는 더 가벼운 라이브러리로 대체하고, 용도가 겹치는 라이브러리는 하나의 라이브러리로 통일하는 것이 좋다.
* **Webpack Analyse** : 가장 다양한 정보를 주지만 사용법이 복잡하고 느리다.
* **Webpack Visualizer** : 깔끔한 시각화를 보여주지만 기능이 부족하다.
* **Webpack Bundle Analyzer** : 용량별로 시각화를 해주어 어떠한 라이브러리가 많이 사용되고 있는지 알 수 있으며, 사이드바를 이용해 검색과 필터링도 가능하다. 직접 사용하지 않지만 번들에 포함된 라이브러리들을 확인할 수 있다.

### 2. 라이브러리 중복 줄이기

* npm의 특성상 같은 라이브러리지만 버전이 다른 경우가 존재하기도 한다. (Dependency conflict)
* **npm dedupe** : 중복된 모듈을 줄일 수 있는 명령어
* yarn에서는 이러한 문제를 라이브러리 설치과정에서 완벽히 처리해주기 때문에 신경쓸 필요가 없다고 쓰여있지만 완벽하지는 않기 때문에 **yarn deduplicate** 라이브러리를 이용하여 문제를 해결할 수 있다.
* **lodash**를 이용하여 줄일 수 있음. (lodash는 생각보다 용량이 크다.)
* 라이브러리의 중복을 피했다면 꼭 필요한 코드만 사용하도록 수정(import)해야 한다.

### 3. 더 가벼운 라이브러리 사용하기

* webpack은 브라우저와 node 환경을 최대한 맞추기 위해 필요한 경우 polyfill을 추가하기도 한다. 라이브러리 용량 자체는 적었지만, 사용후 polyfill이 추가되어 더 느려지는 경우가 있으므로 주의해야 한다.
* 설치전, 라이브러리 비교를 위해 **Bundle Phobia**라는 웹 사이트를 활용할 수 있다. 해당 사이트를 통해 다운로드 속도, 각 버전별 용량을 쉽게 확인할 수 있다. 또한 라이브러리의 디펜던시를 미리 확인해볼 수도 있다.

### 4. 더 가벼운 라이브러리 만들기

* **tree-shaking** : 나무를 흔들면 과일이 떨어지는 것처럼 불필요한 코드를 정적분석을 통해 제거하는 기술이다. tree-shaking이 지원된다면 정말로 사용 중인 코드만 번들에 포함되기 때문에 더 가벼운 번들을 만들 수 있다.
* webpack은 rollup에 비해 Side Effects 판단을 어려워하는편
* 라이브러리를 만들 때에는 webpack에게 side effect 여부를 알려줘야 한다. webpack은 package.json의 sideEffects란 필드를 참고해 어떤 파일에 side effect가 있는지를 확인한다.
* 컴파일 툴을 잘 고르는 것도 중요하다.

**기타**

* 라이브러리의 용량을 더 이상 줄일 수 없다면, 무거운 라이브러리의 영향을 최소화하는 것이 중요하다. (Granular Chunks, Dynamic Import 등)

## [🔗](https://www.youtube.com/watch?v=edWbHp_k_9Y) 실무에서 바로 쓰는 Frontend Clean Code

### 1. 실무에서 클린 코드의 의의

* 유지보수 시간의 단축

### 2. 안일한 코드 추가의 함정

* 하나의 목적인 코드가 흩뿌려져 있기 때문에 나쁜 코드가 되어버린다.
* 하나의 함수가 여러 가지 일을 하게 된다.
* 함수의 세부 구현 단계가 제각각이다.
* 리팩토링
  * 함수 세부 구현 단계 통일
  * 하나의 목적인 코드는 뭉쳐 두기
  * 함수가 한 가지 일만 하도록 쪼개기
* **클린 코드 !== 짧은 코드**
* **클린 코드 === 원하는 로직을 빠르게 찾을 수 있는 코드**

### 3. 로직을 빠르게 찾을 수 있는 코드

* 응집도를 높인다.
  * 무엇을 뭉쳐야 하는가? 당장 몰라도되는 디테일한 요소들
  * 뭉치면 답답한 코드들? 코드 파악에 필수적인 핵심 정보
  * 핵심 데이터와 세부 구현 나누기
  * 선언적 프로그래밍: '무엇'을 하는 함수인지 빠른 이해 가능
* 단일책임 원칙에 의거하여 쪼개준다.
* 추상화 단계를 조정해서 핵심 개념을 필요한 만큼만 노출해야 한다.
  * 추상화 수준이 섞여 있으면 코드를 파악하기 어렵다.

### 4. 액션 아이템

* 담대하게 기존 코드 수정하기
* 큰 그림 보는 연습하기
* 팀과 함께 공감대 형성하기
* 문서로 적어 보기



