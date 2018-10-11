# eslint 적용

## 개요

최근 대규모 업데이트가 끝나고 대표님과의 약속으로 얻어낸 유지보수 기간에 적용하였다.  

코드를 좀 더 명확하게 사용하기 위한 도구이다. 즉, 클린코드를 위한 도구이다.
나의 단점으로 잔 실수가 많은 점에 대해서 많은 도움이 되었다.  

예를 들면

```
callback && callback()
```

다음과 같은 코드는 아래코드보다 간결할지는 모르겠지만 아래가 좀 더 명확한 코드라고 할 수 있다.

```
if(callback){
  callback()
}
```

다른 간단한 예로는 이런것도 있다. (변수명 재사용)

```
let a = 1;
function someTing(){
  let a = 2;
}

```

위와 같은 경우에는 스코프 때문에 컴파일,작동에는 문제가 되지 않는다. 하지만 코드를 작성하는 사람에게 하여금 혼란이 올 수 있는 여지가 있으므로 잘 못된 코드라고 명시해준다.  
tab indent라던가 spacing등의 간단한 룰부터 좀 더 기능적인 부분까지 교정해주기까지 한다.  
모두가 같은 코드스타일을 사용하게 되기 때문에 여럿이서 코드 스타일을 일관되게 맞추는 기에도 좋다.

### 설치

eslint 설치  
```
yarn add -dev eslint
```

리엑트를 개발하고 있는 환경으로서 추가로 설치해야 하는 사항들이다.  

```
yarn add -dev eslint-config-airbnb babel-eslint eslint-plugin-react eslint-plugin-import eslint-jsx-a11y
```

### 환경 설정 방법

크게 두가지 방법으로 작성된다.

다른 node설정파일과 같이 `package.json` 안에 `eslintConfig`의 키값으로 설정을 작성하는 방법과
`.eslintrc`파일에 json방식으로 작성하는 방식이 있다. 다른 파일이름으로 작성하여 설정파일을 지정해주어도 된다.

설정에 대한 설명은 [여기](https://eslint.org/docs/user-guide/configuring)를 참고 한다.


나의 설정은 아래와 같다.  
```
{
  "parser": "babel-eslint",
  "extends": "airbnb",
  "plugins": [
    "react",
    "jsx-a11y",
    "import"
  ],
  "rules": {
    "template-curly-spacing": "off",
    ...
  },
  "globals": {
    "gtag": true,
    "fbq": true,
    "gaUtil": true
  },
  "env": {
    "browser": true,
    "jest": true,
    "node": true
  }
}
```

env부분에서는 browser환경이기 때문에 발생하는 변수인 window나 document같은 것들을 지원해준다.
jest나 다른 여러 유명 모듈에 대해서도 지원해주기 때문에 필요한 것들은 바로바로 적용해 사용하면 된다.
커스텀으로 글로벌 변수를 사용한다면, 혹은 글로벌 변수를 사용하는 라이브러리를 사용한다면 위와 같이 globals부분에 작성해 사용 할 수 있다.



#### 관련 모듈, 플러그인들

사용한 플러그인 위주로 설명한다. 아래 플러그인들은 eslint-config-airbnb를 사용하기 위해 필요한 것들이다.

##### babel-eslint

babel환경에서 eslint를 사용할 수 있게 해준다. 즉, babel로 작성된 문법을 해석할 수 있게 해준다.

##### eslint-plugin-react

리엑트에 관련한 룰들을 적용한다. 예를 들면 react 라이프 사이클를 기반으로 코드 작성 순서를 결정한다.

```
class App extends React.Component {
  static displayName = "...";

  constructor() {
    //...
  }

  componentWillMount() {
    //
  }

  componentDidMount() {
    //
  }

  myfunction() {
    //..
  }

  render() {
    //...
  }
}

```

`displayName, propTypes, contextTypes, childContextTypes, mixins, statics, defaultProps, constructor, getDefaultProps, state, getInitialState, getChildContext, getDerivedStateFromProps, componentWillMount, UNSAFE_componentWillMount, componentDidMount, componentWillReceiveProps, UNSAFE_componentWillReceiveProps, shouldComponentUpdate, componentWillUpdate, UNSAFE_componentWillUpdate, getSnapshotBeforeUpdate, componentDidUpdate, componentDidCatch, componentWillUnmount` 순서대를 가지고 있다.  

이 외에도 propTypes 작성, 그에 따른 defaultProps 작성, 사용하지 않은 props, state 제외 등의 룰을 가지고 있다.  

##### eslint-plugin-import

import구문과 관련된 linter 플러그인이다. linter가 없이 오랫동안 프로젝트가 진행되어 왔기 때문에 기존의 코드들에서 import export 구분에 대해서 정리가 필요를 느꼈기에 적용했다.

##### eslint-plugin-jsx-a11y

위에 설명한 `eslint-plugin-react`의 문서에서 추천한 플러그인이기도 하다. jsx의 html구문 작성을 좀더 명확하게 하는데 도움이 된다. 예를 들면 a 테그는 그 이름의 의미를 href 속성으로 하여금 역활을 하기 때문에 필수로 작성이 되어야 한다던가, button 테그에 대해서는 타입을 정확하게 명시하게 한다.



#### 후기

작업 시작 후 약 2주일에 걸쳐서 linter를 수정하였다. 당연히 알고 있던 레거시와 같은 것이기 때문에 크게 놀라지도 않았다. 진작 적용해야하는 작업을 뒤늦게 했음이 안타까울 뿐이였다.
