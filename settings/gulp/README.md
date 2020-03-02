# Gulp

## 설명

- Gulp는 생산성을 높이고 개발자들의 수고를 덜어줄 수 있는 유용한 자동화 빌드 시스템으로 이 외에도 Grunt, Jenkins 등이 있다. 

- Javascript를 압축하고 CSS 전처리기인 Sass 파일을 컴파일하고, 이미지 스프라이트 생성, 코드에 오류는 없는지 체크하는 등의 반복적인 작업을 자동으로 처리해준다.

## 세팅

### node.js 와 npm 확인 및 설치하기

- gulp는 node.js의 스트림 기능을 기반으로 하기 때문에 node.js가 함께 설치되어야 한다.

	- [node.js DOWNLOADS](https://nodejs.org/en/download/)

	- 요청 후 한번에 결과를 받는 것이 아니라 이벤트로 중간중간 전달받는 방식을 stream이라고 한다.

	- Node.js 는 자바스크립트를 개발 언어로 사용하는 소프트웨어 플랫폼으로 구글 크롬 웹브라우저와 안드로이드 웹브라우저에 탑재된 V8 엔진 위에서 동작하고, 프론트측이 아닌 서버측에서 실행되는 서버사이드 언어(Server Side Language)이다.

- node.js를 설치하면 npm, npx가 자동으로 설치된다.

```
// 버전 확인
node -v
npm -v
npx -v

// 작업할 해당 프로젝트 경로로 들어가서 package.json 생성
npm init

// enter
```

### gulp4.0으로 세팅하기(기존 gulp3.0 삭제)

- 기존의 설치되어 있던 gulp3.0 버전에서 gulp 4.0으로 변경하여 다시 세팅해보자.

```
// 전역에 설치한 Gulp 제거
$ npm uninstall gulp --global
$ npm uninstall gulp-cli -g

// 프로젝트에 설치한 Gulp 제거
$ npm uninstall gulp --save-dev

// 캐시 삭제
$ npm cache clean # for npm < v5

// Gulp Cli 설치
$ npm install gulpjs/gulp-cli --global

// 작업할 해당 프로젝트에 Gulp 4.0 설치
$ npm install gulpjs/gulp.git#4.0 --save-dev

// package.json 경로에 gulpfile.js 파일 생성
$ mkdir gulpfile.js

// gulp 버전 확인
gulp -v
```

## 정보

### gulp4.0 추가된 내용

- 보편적으로 ES6를 사용하기 때문에 var 대신 let, const 를 사용해서 작업하고, 구조분해할당을 이용해서 gulp의 각 함수를 사용해서 작업한다.

- gulp.task 메서드 대신 function(const)를 사용한다.

- **lastRun()**

	> 반복되는 빌드 속도를 개선하기 위한 방법 중 하나로, 빌드할 때 마다 모든 파일을 처리하는 것이 아니라, 변경된 사항만 처리한다.
	>
	> watch가 적용된 Task에 유용하다. src 함수에 옵션을 추가하여 적용한다.

	```
	// 예 
	const minify = () => {
	return(
	 gulp
	  .src(jsPaths.jsUi, {since(lastRun:(minify))})
	 );
	}
	```

- **Sourcemaps 기본지원**

	> 소스맵을 기본적으로 지원하기 때문에 gulp-sourcemaps 모듈을 사용하지 않아도 된다.
	>
	> watch가 적용된 Task에 유용하다. src 함수에 옵션을 추가하여 적용한다.

	> sourcemaps?
	>
	> 소스맵(sourcemaps)은 코드상의 위치를 알려주는 것을 말한다. scss를 컴파일을 하게되면 css, html이 수정이 되는데 이런 수정된 위치를 알 수 없다. 이 때 sourcemaps를 설정하게 되면 scss 파일의 위치를 알려주기 때문에 유용하게 사용할 수 있다. 즉, 변형된 코드의 어느 부분이 기존 소스 코드의 어느 부분에 해당하는 지에 대한 정보가 담긴다.
	>
	> 예) sourceMappingURL=data:application/json;base64,

	```
	// 예
	const scssUilts = () => {
	return (
	 gulp
	  .src(scssPath.cssUi, {sourcemaps: true})
	 )
	}
	```

- **function(const)의 사용, module 내보내기**

	> Task 실행 순서를 통제할 수 있는 API를 제공한다.run-sequence 모듈을 사용하지 않아도 된다.

	```
	// gulp3.0
	gulp.task('myTask', function(){
	 //task
	})

	// gulp4.0
	function myTask(){
	 //task
	}

	// gulp4.0 - ES6
	const mySecondTask = () => {
	 //task
	}

	// 내보내기
	exports.css = css;
	exports.default = series(html, css)
	```

- **Series와 Parallel**

	> Series() : Task를 순차적으로 실행한다.

	```
	const { series } = require('gulp');

	const html = (done) =>{
	 done();
	}

	const css = (done) => {
	 done();
	}

	exports.build = gulp.series(html, css);
	```

	> Parallel():  Task를 병렬로 실행한다.

	```
	const { parallel } = require('gulp');

	const html = (done) => {
 	 done();
	}

	const css = (done) => {
 	 done();
	}
	exports.build = parallel(html, css);
	```

	> Series(), Parallel() 함께 사용하기

	```
	const html = () => {
	 //task
	}
	const css = () => {
	 //task
	}
	const js = () => {
	 //task
	}
	exports.build = gulp.series(js, parallel(html, css))

	=== gulp.task('js', ['html', 'css'])
	```

## 확인 필요

### 부족한 부분

- gulp3.0의 기능, gulp4.0에서 추가된 기능을 정확히 파악하는데 한계가 있는 것 같아 좀 더 공부가 필요

	- lastRun() 이해를 못함

	- gulp.watch function으로 쓰는 방법

	- symlink, regisrty, vynl ... 정리 필요

## 참고 블로그

- [gulp DOCS](https://gulpjs.com/docs/en/getting-started/quick-start)

- [gulp setting](https://stackoverflow.com/questions/33429727/how-do-i-install-gulp-4)

- [gulp setting](https://programmingsummaries.tistory.com/393)

