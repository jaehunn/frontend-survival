# Environment

## Q1. 패키지 의존성에 대해서

package.json 으로 프로젝트가 의존하는 패키지 목록을 관리할 수 있다.

협업하는 개발자에게 이 프로젝트가 어떤 패키지를 사용하는지, 어떤 버전을 사용하는지 공유할 수 있다.

npm install 을 진행할 때, --save-dev 옵션을 지정할 수 있다.

개발 의존성 패키지로 명시하는 것이고, 개발 단계에서만 필요한 패키지를 뜻한다. package.json 파일의 devDependencies 속성에 나열된다.

반대로 dependencies 속성에 나열되는 패키지들은 --save-dev 옵션을 붙히지않고 설치한 패키지를 의미한다. 프로덕션 환경에서 필요한 패키지로 어플리케이션이 구동되기 위한 패키지다.

즉, 개발 의존성 패키지는 사용자가 어플리케이션을 사용하면서 필요하지않은 패키지고, 빌드시 패키지를 제외한다.

peerDependencies 라는 것도 있다.

peer 는 동료라는 의미를 가지는데. 이 프로젝트를 사용할 프로젝트에게 패키지의 버전을 알려주는 용도로 사용된다.

예를 들어, react 17 를 사용하는 프로젝트(A) 를 외부 프로젝트들에게 공개한다고 하면, 외부 프로젝트(B) 에서는 호환성을 위해서 react 17 버전을 사용하도록 해야한다.

* B > A > react 17

## Q2. 의존성 트리

package-lock.json 은 package.json 으로 정의된 패키지들을 설치하면 node_modules 디렉토리의 상태에 따라 자동 생성된다.

package-lock.json 은 협업하는 개발자들에게 동일한 의존성 트리를 제공하도록 돕는다. 협업하는 개발자들에게 공유되어야하는 파일이다. (git)

NPM 은 어떤 방식으로 의존성 트리에 명시된 패키지를 탐색할까.

의존성 트리가 다음과 같이 구성되어있다고 해보자.

* A 라는 패키지는 C 라는 패키지를 의존하고 있고, (A > C)
* B 라는 패키지는 C 라는 패키지를 의존하고 있다. (B > C)

C 는 공교롭게도 두 곳에서 관리되어 패키지가 중복된다.

`npm dedup` 명령어는 의존성 트리를 flat 하게 만든다.

```console
// 만약 node_modules 에 있는 패키지들의 비중을 알고 싶으면 다음 명령어를 사용해보자.
du -sh ./node_modules/* | sort -nr | grep '\dM.*'
```

간혹 `npm install` 을 하다보면, package-lock.json 이 업데이트되는 상황이 발생하는데. package.json 에 ^1.1.0 과 같은 시멘틱 버저닝을 사용하고 있기 때문이다. package-lock.json 에 명시된대로 install 을 수행하고 싶다면, `npm ci` 를 사용해보자.

---
Reference

* <https://yceffort.kr/2020/11/javascript-dependency-hell>
* <https://toss.tech/article/node-modules-and-yarn-berry>
* <https://velog.io/@johnyworld/Peer-Dependencies-%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC>
