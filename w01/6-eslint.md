# ESLint

## Q1. ESLint 와 Prettier

- eslint 는 코드을 정적으로 분석한다. 규칙에 어긋나지않도록 돕는다.
- 팀의 컨벤션을 유지하는 기능도 있지만, 최신 트렌드 문법을 지원하기 위한 부분도 있다.
- `eslint-plugin-*` 은 `*` 와 관련된 룰을 정의한 패키지를 의미한다. (eslint-plugin-react).

```json
{
  "plugins": ["react"],
  "rules": {
    "react/jsx-uses-react": "error",
    "react/jsx-uses-vars": "error"
  }
}
```

- plugin 을 적용하고, 룰을 적용한다. 보통은 귀찮으니 recommended 를 사용한다.

```json
{
  "extends": ["plugin:react/recommended"]
}
```

- extends 를 하는 이유는 plugin:react/recommended 내 에서 plugin 을 적용하기 떄문이다. extends 가 더 상위 적용 옵션인 것을 알 수 있다.
- `eslint-config-*` 는 `*` 패키지들이나 룰들을 모아서 만든것을 의미한다. `eslint-plugin-*` 보다 상위 계층이다. extends 하면 된다.

```json
{
  "extends": ["airbnb"]
}
```

- `eslint-plugin-*` 는 `extends: [plugin:패키지네임/설정네임]`으로 사용할 수 있는데.
- `eslint-config-*` 는 바로 `*`를 써주기만 하면 된다.

- prettier 는 코드 포매팅 툴이다.
- .prettierrc 로 코드 포맷에 대한 설정을 둘 수 있다.
- vscode 사용자는 확장프로그램으로 prettier 가 프로젝트 패키지로 설치되어있지않아도 사용할 수 있는데 webstorm 을 사용하는 개발자는 패키지로 명시되어있지않아 코드 포맷의 불일치가 발생할 수 있다.
- prettier 패키지를 설치해서 package.json 에 prettier 를 사용한다는 것을 협업하는 개발자들에게 공유할 필요가 있다.
- 프로젝트 내 .prettierrc 룰이 먼저 적용된다.

Reference

- <https://yrnana.dev/post/2021-09-02-eslint/>
