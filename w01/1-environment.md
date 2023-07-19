# Environment

프론트엔드 생태계는 현재 빠르게 변화하고 있다. 오늘 유행하던 것이 내일이면 유행이 지나있을 수도 있다. 따라서 우리는 개발환경을 구성하는 도구의 쓰임새와 전체적인 맥락을 파악하는 것이 변화를 적응하는데에 중요하다.

## Node.js

Node.js 는 JavaScript 런타임이다. 런타임이라고 하면, 자바스크립트가 실제 구동될 수 있는 환경을 뜻한다.

우리는 자바스크립트로 이루어진 프론트엔드 개발환경을 구성할 것이기 때문에, 자바스크립트가 구동될 수 있는 환경인 Node.js 를 먼저 설치해야한다.

[fnm](https://github.com/Schniz/fnm) 이라는 툴을 사용하면, Node.js 를 손쉽게 설치 및 관리할 수 있다.

1. 먼저 fnm 을 설치해준다.

```console
curl -fsSL https://fnm.vercel.app/install | bash
```

2.그 다음 Node.js 를 fnm 을 이용하여 설치한다.

```console
# fnm install {Node version}

fnm install --lts
```

lts 라고 하면, long term support 라고 해서, 안전성에 중점을 둔 버전이라고 보면 된다.

## 프로젝트 생성하기

Node.js 를 설치했다면, 이제 프로젝트를 본격적으로 만들어보자.

1. 먼저 프로젝트 폴더를 생성해준다.

```console
mkdir my-app

cd my-app
```

2.프로젝트에 진입하였으면, 자바스크립트 패키지들을 관리하는 설정파일을 생성하자.

```console
npm init -y
```

여기서 우리는 NPM 이라는 패키지 매니저를 사용할 것이다. -y 옵션을 주면, 기본적인 설정 물음에 대해서 동의한다는 것을 의미한다. 현재 package.json 파일이 생성된 것을 볼 수 있다.

3..gitignore 파일을 생성해준다.

```console
touch .gitignore
```

4..gitignore 파일에 패키지들이 설치되는 node_modules 폴더를 명시한다. 이렇게 되면 git 은 설치되는 패키지들을 추적하지 않게 되고, 패키지들이 원격 저장소에 올라가는 상황을 방지할 수 있다.

```text
# .gitignore

node_modules
```

지금까지 내용으로 우리는 앞으로 설치할 자바스크립트 도구들을 관리할 수 있는 프로젝트를 만들었다.

## 개발 도구 설치하기

타입스크립트를 사용해서 개발할 것이기 때문에, 타입스크립트를 설치하고 설정파일을 생성해보자.

```console
npm install -D typescript

npx tsc --init
```

npm install 명령어로 개발 도구를 설치할 수 있다.

-D 옵션은 devDependency 를 의미하고, 개발 당시에만 사용되는 패키지를 의미한다. 타입스크립트는 그대로 동작할수는 없고, 빌드 때 자바스크립트로 변환되어서 동작하기 때문에 개발 당시에만 필요한 패키지다. -D 옵션을 사용하지 않으면, 실제 운영 환경에서 설치되어야하는 패키지를 의미한다.

npx 는 node 5.2.0 버전 이상부터 사용할 수 있는 명령어다. NPM 레지스트리(서버)에 올라가 있는 패키지들을 우리의 컴퓨터에 글로벌 설치를 하지않아도 사용할 수 있도록 돕는다. tsc 는 타입스크립트의 컴파일러를 의미하는데, 타입스크립트 패키지를 설치해야 구동이 가능하다. 실제 우리는 타입스크립트를 프로젝트에 설치하였지 전역으로 설치하지않았다. 글로벌로 설치한 패키지를 확인하려면 `npm list -g` 를 입력하면 된다.

npx tsc --init 를 하게되면, 타입스크립트 관련 설정파일이 생성된다. (`tsconfig.json`)

옵션에 대한 설정은 타입스크립트 파트에서 더 자세히 다뤄보자. ([TypeScript 파트](2-typescript.md))

우리는 개발을 혼자하지 않을때가 훨씬 많다. 그래서 우리는 일관성있는 코드 규칙을 적용할 필요가 있고, 이때 사용하는 도구가 ESLint 다.

```console
npm install -D eslint

npx eslint --init
```

타입스크립트 설치와 마찬가지로 개발환경 패키지로 다운로드해주고, npx 를 통해 eslint 설정파일을 생성해준다. (`.eslintrc.js`)

설정파일이 .js 확장자로 생성되어서 자바스크립트 형식으로 설정방법을 적용할 수 있다. 만약 .eslintrc 형식으로 파일 이름을 가져가게되면, JSON 형식으로 설정파일을 다룰 수 있다.

ESLint 역시 자세한 설정 방법은 다음 파트에서 다뤄보자. ([ESLint 파트](6-eslint.md))

이후에 테스팅 도구인 Jest 를 설치할텐데 미리 설정 파일에 `jest: true` 를 설정해주면 도움이 된다.

```json
module.exports = {
 env: {
  browser: true,
  es2021: true,
  jest: true,
 },

 ...
}
```

가장 핵심이 되는 리액트를 설치해보자.

```console
npm i react react-dom

npm i -D @types/react @types/react-dom
```

install 약어로 i 를 쓸 수도 있다.

react 와 react-dom 을 설치해주었다. 리액트의 패러다임에 대해서는 이후 파트에서 더 자세히 알아볼텐데 ([React 파트](3-react.md)) react 는 우리가 작성한 리액트 코드를 react-dom 패키지에 전달하게 된다. 변경된 사항을 react-dom 이 실제 브라우저 DOM 에 반영하게 되는 작업을 하게 된다. 그래서 두 패키지를 설치해준 것이다.

@types 가 붙은 패키지를 추가로 설치해주었는데, 타입스크립트 정의가 들어간 패키지다. 거의 대부분의 자바스크립트 패키지들이 @types 라는 prefix 가 붙은 타입 정의 패키지를 제공하고 있다. 우리는 타입스크립트로 개발을 진행할 것이고, 타입스크립트의 강력함은 타입스크립트 파트에서 더 알아보자.

이제 테스팅 도구를 설치해보자.

```console
npm i -D jest @types/jest @swc/core @swc/jest \
    jest-environment-jsdom \
    @testing-library/react @testing-library/jest-dom
```

리액트를 테스트하는 가장 보편적인 도구는 Jest 와 React Testing Library 를 많이 쓴다. Jest 는 테스트 프레임워크고, React Testing Library(RTL) 은 jsdom 이라고 하는 라이브러리를 통해서 브라우저 DOM 에 대한 테스트를 진행하는 라이브러리다.

테스트에 대한 자세한 내용은 이후 파트에서 더 알아보자. ([Testing Library 파트](4-testing-library.md))

그 다음 Jest 에 대한 설정 파일을 생성해준다.

```console
touch jest.config.js
```

아래와 같은 테스트 설정 양식을 작성해주자. 설정 관련 내용은 이후 파트에서 더 알아보자.

```json
module.exports = {
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: [
    '@testing-library/jest-dom/extend-expect',
    './jest.setup',
  ],
  transform: {
    '^.+\\.(t|j)sx?$': ['@swc/jest', {
      jsc: {
        parser: {
          syntax: 'typescript',
          jsx: true,
          decorators: true,
        },
        transform: {
          react: {
            runtime: 'automatic',
          },
        },
      },
    }],
  },
  testPathIgnorePatterns: [
    '<rootDir>/node_modules/',
    '<rootDir>/dist/',
  ],
};
```

마지막으로 프론트엔드 파일들을 한데 묶어주는 번들러라는 도구를 설치할 것이다. 그 중에서 설정이 간편한 Parcel 이라는 도구를 사용할 것이다.

```console
npm i -D parcel
```

그리고 `package.json` 파일의 scripts 속성에 다음의 스크립트를 추가해보자.

```json
"scripts": {
    "start": "parcel --port 8080",
    "build": "parcel build",
}
```

이제 프로젝트를 구동시켜보자. 프로젝트를 구동시키는 명령어는 scripts 속성에 정의되어야한다.

정의한 scripts 들은 `npm run {scripts}` 을 통해 실행될 수 있다.

```console
npm run start
```

실행을 해보면 다음과 같은 에러를 마주한다.

```console
unknown: Could not find entry: /Users/bangjaehun/workspace/frontend-survival/w01/my-app/
```

이유는 파일의 시작점을 찾을 수 없기 때문에 발생했다.
`package.json` 에 명시된 `main` 속성은 Node 를 사용할때 시작이 되는 모듈을 의미한다. 근데 우리는 port 를 열어서 웹 서버를 구동시킬것이기 떄문에 index.js 가 아닌 index.html 을 띄워야한다. `main` 대신 `source` 속성에 `index.html` 을 적용해보자.

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "",
  "source": "index.html",

  ...
}
```

이렇게 프로젝트에 기본적인 개발환경 설정을 마무리했다. 현재는 아무런 개발코드가 없어서 index.html 을 parcel 을 통해 띄운 것이 전부다. 본격적으로 리액트와 타입스크립트로  개발해보기전에 타입스크립트와 리액트에 대해서 한번 알아보도록 하자.
