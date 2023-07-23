# Environment

## NPM (Node Package Manager)

Node.js (JavaScript) 패키지를 관리하는 도구.

* 프로젝트에 사용될 패키지 목록은 package.json 파일로 관리된다.
* dependencies 는 어플리케이션에서 구동되어야하는 패키지
* devDependencies 는 빌드 이전에서만 구동되는 패키지
* peerDependencies 는 내 프로젝트에서 사용하는 패키지 버전을 외부 프로젝트가 내 프로젝트를 사용할 때 호환시키기 위해 패키지 버전을 알려주기위한 용도로 사용한다.
  * `--save-dev` 옵션을 줘서 설치한다. (`-D` 옵션과 동일)
* `npm install` 시, package-lock.json 이 생성된다.
  * package-lock.json 은 의존성 트리를 나타내며, 협업자들에게 공유되어야한다. (Git)
  * `npm i` 했을 때, package.json 의 [시멘틱 버저닝](https://docs.npmjs.com/cli/v6/using-npm/semver)을 보고 package-lock.json 이 달라지기도 하는데, 이 때는 package-lock.json 에 명시된대로 설치하는 `npm ci` 명령어를 사용하면 된다.
* node_modules 는 의존성 패키지 중복이 발생한다.
  * NPM 에서는 Hoisting 으로 중복되는 패키지를 한 곳으로 끌어올린다.
  * 개발자가 설치하지않아서 사용할 수 없었던 패키지가 끌어올려지면서 갑자기 사용되어진다.
  * 사용하다가 특정 패키지를 제거했을때 갑자기 사용할 수 없게되는 상황이 발생한다 (유령 의존성 패키지)
  * 이런 문제를 해결하기 위해 Yarn Berry 는 PnP(Plug'n'Play) 를 사용한다. ([참고 자료](<https://toss.tech/article/node-modules-and-yarn-berry>))

## JavaScript Module System

* 어플리케이션의 크기가 커지면, 파일을 여럭 개로 분리해야한다. 이 분리된 파일을 모듈이라고 부른다.
* `<script type="module">` 은 브라우저가 이 스크립트가 모듈이라는 것을 인지하게 돕는다.
* 모듈은 보통 여러개로 제공되어 한 데 묶는 번들러를 사용하게 된다.
* 번들러는 Entry 모듈을 지정하고, 의존 관계에 따라 하나의 큰 파일을 만들어낸다.
* tree-shaking 으로 쓰이지않는 모듈을 제거하기도하고, 최신 문법을 바벨을 통해 호환성을 위한 낮은 버전의 스크립트로 변환하기도 한다.
* 번들링한 결과물은 type="module" 이 필요없어진다. import, export 를 사용하지않는 ES Module (>= ES6) 이 아닌 낮은 버전의 스크립트로 변환되기 때문이다.

---
Reference

* <https://docs.npmjs.com/cli/v6/using-npm/semver>
* <https://yceffort.kr/2020/11/javascript-dependency-hell>
* <https://velog.io/@johnyworld/Peer-Dependencies-%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC>
* <https://toss.tech/article/node-modules-and-yarn-berry>
* <https://ko.javascript.info/modules-intro>
* <https://ko.javascript.info/modules-intro#ref-1022>
* <https://www.youtube.com/watch?v=mee1QbvaO10>
