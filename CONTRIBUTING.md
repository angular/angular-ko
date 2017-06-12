# Angular.io 한글화 작업에 기여하기 

## 한글화 규칙
1. 언어, 프레임워크, 라이브러리 등의 이름은 영문으로 표기합니다. 
1. 명사의 복수형은 기본적으로 단수 표현으로 옮깁니다.
1. 기타 자세한 번역 가이드는 [여기](https://github.com/angular/angular-ko/blob/master/ko-trans-guide.md)를 참고하세요.

## 작업 규칙
- 문단 단위의 영문 원문 위에 한 줄 공백을 두고 한글 번역문을 추가합니다. 
- 이 작업흐름은 싱크 문제를 해결할 뿐 아니라, 원문와 번역문이 나란히 있기 때문에 번역과 검토 작업을 쉽게 해 줍니다.
- 제목 등 문법표기가 명확한 경우에는 공백을 두지 않고 바로 위에 추가합니다. 
- 추후 한글을 기본으로 영문을 토글하여 보여주는 스크립트를 추가할 예정입니다.
- 한글로 번역할 필요가 없는 경우에도 스크립트의 올바른 적용을 위해 원문을 복사하여 번역문 자리에 삽입합니다.

## 커밋 규칙
- 번역의 경우: Trans(xxx.jade): line xxx
- 리뷰의 경우: Review(xxx.jade): line xxx

##  개발 설정(Development Setup)
이 사이트는 node와 npm에 많이 의존하고 있습니다.

1. 최신버전의 node(적어도 v.5 이상)와 npm을 사용하시기 바랍니다. 설치되어 있지 않다면 [nvm](https://github.com/creationix/nvm)을 이용해 해당 버전을 설치하세요.

1. npm package를 *전역으로* 설치하세요 : `npm install -g harp gulp`

1. 이 repo와 [angular source code repo](https://github.com/angular/angular), 그리고 [dart-lang/angular2 source code repo](https://github.com/dart-lang/angular2)를 같은 폴더에 클론하세요.
클론된 3개의 repo는 반드시 같은 폴더 내에 각각 **angular**와 **angular-dart**라는 이름으로 있어야 합니다.

1. `angular.io/`의 기본폴더로 이동하세요.

1. `npm install`을 실행해 *모든 문서들*의 로컬 패키지들을 설치하세요. > `node-sass`는 별도로 다시 빌드해야 합니다.: `npm rebuild node-sass`

##  개발 설정(Development Setup) - Ubuntu 16.04 기준

1. apt-get 을 통해서 npm 을 설치하세요.

    sudo apt-get install npm

1. Angular 리포지토리를 클론하세요.

    git clone https://github.com/angular/angular.git

1. 2번에서 클론했던 동일한 폴더에 번역을 진행하는 프로젝트를 클론하세요.

    예시) git clone https://github.com/17-1-SKKU-OSS/angular-ko.git

1. angular-ko 디렉토리로 이동하세요.

    cd angular-ko

1. 필요한 라이브러리들을 설치하세요.

    npm install

1. harp 및 gulp@3.9.0을 설치하세요, 버전이 맞지 않으면 동작하지 않습니다.

    npm install -g harp gulp@3.9.0

1. node-sass를 리빌드 하세요.

    npm rebuild node-sass

1. gulp로 웹 서버를 실행시키세요.

    gulp serve-and-sync

1. 웹 브라우저로 페이지에 접근해보세요.

    기본 주소 : http://localhost:3000/

## 내용 구성(Content Development)
모든 문서의 내용은 Jade의 [구문](http://jade-lang.com/reference/)으로 쓰여졌습니다.
공백이 중요한 언어의 엄격한 기준에 유의하시기 바랍니다.
내용을 편집할 때 *타이핑하면서* 변한 것을 확인하기 위해서
`gulp serve-and-sync` 명령어 [아래 참조](#serve-and-sync)를 사용하기를 강력하게 추천합니다.

이 문서는 특정 스타일과 믹스인을 사용하고 있습니다.
해당 내용에 대해서는 [스타일가이드 문서](https://angular.io/docs/ts/latest/styleguide.html)를 참고하세요.

jade문서 파일들은 `public/docs`아래 각 언어별 폴더에 있습니다.
예를 들면, 타입스크립트 문서는 모두 `public/docs/ts/latest`에 있습니다.
예시)
- `public/docs/ts/latest/quickstart.jade`
- `public/docs/ts/latest/guide/architecture.jade`
- `public/docs/ts/latest/cookbook/component-communication.jade`
- `public/docs/ts/latest/tutorial/toh-pt5.jade`

> **중요**: 절대 `public/docs/ts/_cache`안에 있는 파일들은 변경하지 마세요. 캐시된 파일들은 나누어진 작업흐름에 따라 업데이트 됩니다. 

### Local server with watches and browser reload
 1. 루트 폴더인 `angular.io/`로 현재폴더를 변경하세요
 1. `gulp serve-and-sync` 를 실행하세요.
 1. localhost:3000으로 브라우저가 실행되고, 변경사항은 자동으로 반영됩니다.

<a id="serve-and-sync"></a>
만약 개발가이드(dev guide)와 같이 문서들 중 일부만 동작시킬 거라면, 파일시스템 중 일부만 감시(watch)하도록 세부적인 gulp task를 사용할 수 있습니다.

* `gulp serve-and-sync` : 모든 로컬 Jade/Sass파일, API 소스와 예저들, 그리고 개발가이드 파일 감시(watch)
* `gulp serve-and-sync-api` : API 소스와 예제 파일들만 감시(watch)
* `gulp serve-and-sync-devguide` : 개발가이드(dev guide)파일만 감시
* `gulp build-and-serve` : 로컬 Jade/Sass 파일만 감시

## 사용 기술(Technology Used)
- Angular 1.x: Angular의 제품 준비 버젼
- Angular Material: Angular.js의 재료디자인(Material Design) 구현
- Gulp: 노드 기반 툴
- Harp: 전처리가 내장된 정적 웹 서버
- Sass: 전문가 수준의 CSS 확장언어
- Normalize: 브라우저 간 HTML 기본 스타일의 일관성을 유지하도록 돕는 CSS
- Grids: 사용자맞춤형 Sass/CSS 그리드 프레임워크
- Prettify: 자바스크립트 모듈과 CSS 소스코드의 신택스 하이라이트
- Icomoon: 사용자 지정 기본 아이콘 글꼴

## 기타
- 더 적극적으로 번역에 참여하고 싶다면 on.yoon7@gmail.com로 메일을 보내주시기 바랍니다.


