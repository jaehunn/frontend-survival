# Bundler

## Q1. 왜 번들링 하는가

- 왜 자원을 하나로 묶는가.(html css js)
- html 과 css 가 js 안으로 들어오면서, js 가 절대적으로 커졌다.
- js 모듈들이 많아지고, 모듈 간 의존성과 js 를 요청하는 네트워크문제가 발생했다.
- 모듈 번들러는 네트워크 비용을 감소시키고, javascript 를 낮은 버전 js 로 트랜스파일한다. (왜? 낮은 버전을 지원하는 브라우저 호환성을 높이기위해)
- mode 에 대한 지원으로 개발모드와 운영모드로 나눌 수 있게 되었다. 운영에 배포하는 mode 에서는 코드의 보안을 위한 난독화, 코드 용량을 낮추기 위한 압축, 사용하지않는 의존성 트리의 모듈을 제거하는 트리쉐이킹을 지원한다.
