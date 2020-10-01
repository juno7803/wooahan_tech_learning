## 우리들의 고민

- "네트워킹" 이 없다. 시니어가, 선임이 없다
- 코드 품질, 아키텍쳐, 설계 기술? redux를 쓰고있는데, mobx가 좋더라, 어떤걸 써야할까??

## 도구

요즘의 프로그래밍은 "도구"를 익히는 것이 요점인 것 같다

- Typescript, React, redux .. etc

## 목표, 바램, 기대

- 상태 (State): 상태를 관리하는 것이 주 목표
- 환경 (Env): 개발하는 환경, 누구와 일하는가, 어떤 환경에서 개발하는가
- 제품 (Product): 어떤 mission을 해결하기 위함, mission을 잘 이해하는게 그 도구를 잘 쓰는 비결!
- 목표 (Mission)
- 코드 (Quality): code의 퀄리티를 높이기 위한 방법
- 상대적 (E=mc^2)

리덕스, 몹엑스 등이 왜 나온 도구인지, 목적에 맞춰서 잘 사용한다는 게 중요

도구의 저작자가 어떻게 사용했음 좋겠다 와 별개로 다른 방식으로 사용할 수 있는 가도 중요!!

---

# 우아한 테크러닝의 키워드

1. **Typescript**

타입스크립트 공식문서에서 유용하게 사용 (ts→js playground) : ([https://www.typescriptlang.org/play](https://www.typescriptlang.org/play))

2. **React : (**[https://reactjs.org/](https://reactjs.org/))

3. **상태관리**

- redux([https://redux.js.org/](https://redux.js.org/))
- redux-saga([https://redux-saga.js.org/](https://redux-saga.js.org/))
- mobx([https://mobx.js.org/README.html](https://mobx.js.org/README.html))

4. **스타일**

- **Blueprint.js :** ([https://blueprintjs.com/](https://blueprintjs.com/))

    타입스크립트가 적용되어 있고, 컴포넌트는 어떻게 만드는게 좋을지 에 대해 공부하기 좋음

- **antdesign**

5. **테스팅 관점 ("**Testing Library") : ([https://testing-library.com/](https://testing-library.com/))

6. **예제 코드 :** [https://codesandbox.io/index2](https://codesandbox.io/index2)

---

## TypeScript

 javascript의 **superset** 이지만 js보다 크고, 많은 기능을 가지고 있다!

### Type을 지정하는 방법

1. **타입 추론**을 통한 암시적인 타입 지정

```jsx
let foo = 10; // (타입을 추론)
```

2. 명시적인 타입 지정

```jsx
let foo: number = 10; // (타입을 명시)
foo = false; // Error
```

**명시적**인 타입과 **암시적**인 타입? : **명시적**이고 읽기 쉬운 코드가 더 좋고 안정적이라고 생각한다!

es6의 spread문법을 통한 예시

```jsx
function bar(){
	argument;
} // 암시적

function bar(..args){
} // 명시적

bar(10,20)
```

가변인자도 spread 문법을 이용하여 명시적으로 나타내는 것처럼 명시적으로 나타내는것이 추세!

### 타입 별칭

```jsx
type Age = number; // type Alias

let age: Age = 10;
let weight: number = 72;

a = weight;
```

**타입 별칭** 은 타입에 별명을 붙여주는 것으로, 코드에 **가독성**을 올려줄 수 있다. ****

- 표현력을 향상시킬 뿐, 위 예시에선 근본은 `number`와 같다!
- 컴파일 타임에만 작동되는 요소이다!(javascript에서 **transpiling** 되지 않는 요소, 러닝타임까지 작동되는 요소가 아님)
- **transpile :** 한 언어로 작성된 소스 코드를 비슷한 수준의 추상화를 가진 다른 언어로 변환하는 것

    (**ex**: es6 → es5, typescript → javascript)

### 객체 타입

`변수: 타입` 의 형태로 `number` 타입의 `age`와 `string` 타입의 `name` 속성을 가지고 있어야 한다.

```jsx
type Foo = {
	age: number;
	name: string;
}

const foo: Foo = {
	age: 10,
	name: 'kim'
}
```

최종적인 타입은 primitive 한 type이 될 것이다!

- **primitive type** : 기본 자료형 (**ex**: number, string ...)

### interface

typeAlias를 사용할 때와 거의 동일하게 사용할 수 있다.

`union` 타입을 사용할 수 없지만, `extends`로 **상속** 개념을 사용할 수 있다.

```jsx
interface Bar {
	age: Age;
	name: string;
}

const bar: Bar = {
	age: 10,
	name: 'kim',
}
```

**Q/A)typeAlias와 interface 중 어떤 것을 써야 좋을까?**

- 정말 비슷하게 사용됨!(기본 data에 대한 typing)
- React의 props를 전달할 때 주로 type을 명시해 줌
- 용도가 거의 비슷하므로, 한 app에서 통일시켜주도록 하자

---

## React + Typescript

**cra :** `create-react-app` ****을 이용하여 프로젝트를 간단하게 생성할 수 있다.

```jsx
yarn create react-app "my-app" --template typescript // yarn

npx create-react-app "my-app" --template typescript // npx
```

`tsconfig.json` 파일에서 typescript의 옵션을 조정할 수 있다!

**cra**가 가장 무난한 옵션으로 파일을 생성하도록 도와준다

### 간단한 React 컴포넌트 만들기

```jsx
import React from "react";
import ReactDOM from "react-dom";

function App() {
    return (
        <h1>Tech Hello!</h1>
    );
}

ReactDOM.render(
    <React.StricMode>
        <App/>
    </React.StrictMode> /*{ 렌더링 될 컴포넌트 }*/,
    document.getElementById("root") /*{ 렌더링 된 컴포넌트를 넣을 HTML 요소 }*/
)
```

`ReactDOM`의 ****`render` 함수는 **가상돔**(`virtual dom`)에 컴포넌트를 그리는 함수이다

**렌더링될 컴포넌트** 와 **렌더링된 컴포넌트**를 넣을 HTML 요소가 들어간다.

### Babel을 통한 transpliing

`jsx`를 **transpiling** 하는 것이 **babel(**[https://babeljs.io/](https://babeljs.io/))이다!

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57c53a1f-a308-4afc-bf0d-3a06883b2279/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57c53a1f-a308-4afc-bf0d-3a06883b2279/Untitled.png)

(변환 전)                                                                       (변환 후)

작성한 `jsx` 코드가 **React**의 `createElement` 함수로 변환된다.

### App Component의 사용

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

interface AppProps{
	title: string;
	color: string
}

function App(props: AppProps){
	return(
		<h1>{ props.title }</h1>
	);
}
// immutable한 순수함수 형태

ReactDOM.render(
	<React.StrictMode>
		<App title="techHello?" color="red"/>
	</React.StrictMode>,
	document.getElementById('root')
);
// 최상위에서 한번만 호출되어야 함

```

외부에서 작성한 컴포넌트를 호출하여 사용할 수 있다.

`App` 컴포넌트에서 속성으로 적은 것들을 `props` 라고 하며 상위 컴포넌트에서 하위 컴포넌트로 줄 수 있다.

- `props`는 외부와 소통하는 `interface`느낌이므로 `interface`가 좀 더 어울림

## 전역 상태관리

전역으로 상태 관리를 담당하는 대표적인 아키텍처로 `flux` 아키텍쳐가 존재한다.

`flux` 아키텍쳐를 기반으로 한 `redux` 와 `mobx` 라는 **상태관리 라이브러리**가 현재 대표적으로 사용된다! 

`mobx`는 `redux`의 대체품이라기 보단, 상태를 바라보는 관점이 다른, 패러다임이 다른 도구이다.

앞으로 나올 강의에서 모두 다룰 예정!!