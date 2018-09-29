# 타입스크립트 모듈 사용하기

## 개요

typescript는 정적타입 언어이기 때문에 일반적인 javascript로 작성된 모듈을 사용할 수 없다.  
typescript로 프로젝트를 진행 할 경우 typescript를 지원하지 않는 모듈에 대해서 사용방법을 정리한다.
여기에는 ts 타입 작성법은 다루지 않는다. 쉽다면 쉽고 어렵다면 어렵다.

## 구분

크게 3가지로 구분할 수 있다.
1. 모듈 자체에서 typescript를 지원하는 경우
  * `*.d.ts`의 이름으로 그 모듈에 타입이 정의 되어 있다.
2. DefinitelyTyped 프로젝트
  * 프로젝트의 types에서 확인 할 수 있다.
3. 로컬에서 사용해서 작성하기

기타. typscript모듈의 설정

### 자체적으로 지원할 경우

 모듈에서 타입을 정의하는 파일인 `*.d.ts`가 작성되어 있다면 그냥 불러오면 사용할 수 있다.

### 생태계 DefinitelyTyped

[DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) 프로젝트가 있다.
원래 모듈의 작성자가 typescript지원을 하지 않는 경우에 typescript에서 사용가능한 모듈로 작성할 경우에 대해서 위의 프로젝트에 사용하려는 모듈에 대해서 타입을 정의 해놓고 공유한다.

해당 프로젝트에 대한 설명이 한글로 있다. 타입을 정의할 파일에 대한 폼과 룰이 있다.

위의 프로젝트에 기여하면 수시간내에 `@type/${모듈명}`으로 npm에 배포된다고 한다.

기여자가 라이센스를 가지고 있으머 꽤나 활발하다. 크고 유명한 프로젝트들 또한 이 프로젝트를 통해 typescript가 지원되었다.

### 로컬에서 사용해 작성하기

지원하지 않는 모듈들에 대해서 직접적으로 작성하는 2번째 방법이다. 위의 방법은 프로젝트 도중에 바로바로 사용하기에는 문제가 있다. 바로바로 배포가 되어 사용하지 못한다는 것이 문제다.

이 방법은 로컬에 작성을 하고 사용하는 방법이다.

임의의 폴더를 만들고 해당 모듈에 대한 타입을 작성해두면 typescript로서 사용 할 수 있다.


```
//tsconfig.json
{
  ...
  "compilerOptions": {
    ...
    "typeRoots": [
      "./@types"
    ],
    "paths": {
      "*": [
        "./@types/*",
        "*"
      ]
    },
    ...
  }
}
```

위의 설정이 필요하다. 공식 문서에서는 paths에 대한 설정이 없어서 꽤나 삽질이 있었다.


#### 예시

caller 모듈을 작성한다. ts설정은 위와 같다.

es5 사용시

```
var caller = require('caller')
```


타입 파일 작성
```
//@types/caller/index.d.ts

declare module "caller" {
    export = caller;

    function caller(depth?: number): string;

    namespace caller {
    }

}
```

사용

```
import * as caller from 'caller'

caller()
```

### 설정을 바꾸기

typescript에서 타입이 정의가 안된 모듈들도 사용 할 수 있는 설정이 있다.


```
//tsconfig.json
{
  ...
  "compilerOptions": {
    ...
    "noImplicitAny": true,
    ...
  }
}
```

이 부분이다. noImplicitAny이 false 일 경우 타입이 작성되지 않는 것들에 대해서 리턴타입이 any으로서 작동하는 설정이 있다.
