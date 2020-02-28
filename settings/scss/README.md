# Scss

## 세팅

### gulp4.0으로 세팅하기(기존 gulp3.0 삭제)

```
# 전역에 설치한 Gulp 제거
$ npm uninstall gulp --global
$ npm uninstall gulp-cli -g

# 프로젝트에 설치한 Gulp 제거
$ npm uninstall gulp --save-dev

# 캐시 삭제
$ npm cache clean # for npm < v5

# Gulp CLI 설치
$ npm install gulpjs/gulp-cli --global

# 프로젝트에 Gulp 4.0 설치
$ npm install gulpjs/gulp.git#4.0 --save-dev
```

## 정보

### gulp4.0 추가된 기능

- **function의 사용, task module 내보내기**

```
// gulp3.0
gulp.task('myTask', function(){
	//task
})

// gulp4.0
function myTask(){
	//task
}

//내보내기
function html(done){
	done();
}

function css(done){
	done();
}

exports.css = css;
exports.default = gulp.series(html, css)
```

- **Series와 Parallel**

	- Series(): Task를 순차적으로 실행한다.

```
const { series } = require('gulp');

function html(done){
	done();
}

function css(done){
	done();
}

exports.build = gulp.series(html, css);
```

- Parallel(): Task를 병렬로 실행한다.

```
const { parallel } = require('gulp');

function html(done){
	done();
}

function css(done){
	done();
}
exports.build = parallel(html, css);
```

- Series, Parallel 함께 사용하기
```
function html(){
	//task
}
function css(){
	//task
}
function js(){
	//task
}
exports.build = gulp.series(js, parallel(html, css))

	=== gulp.task('js', ['html', 'css'])
```

- **Sourcemaps 기본지원**

	- 소스맵을 기본적으로 지원하기 때문에 gulp-sourcemaps 모듈을 사용하지 않아도 된다.


### 참고한 블로그

- https://stackoverflow.com/questions/33429727/how-do-i-install-gulp-4

- https://programmingsummaries.tistory.com/393

