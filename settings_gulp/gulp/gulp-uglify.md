# gulp-uglify

- with **gulp-concat**

  - gulp-uglify : 파일에 포함된 주석, 공백 등을 제거하는 등 용량을 줄이고 압축을 해줍니다.

  - gulp-concat: 컴파일, 압축 등의 작업을 거친 파일들을 원하는 파일에 합쳐줍니다.

## 설명

### 1. 모듈 설치

> 작업에 필요한 Plugin 설치 

```
npm install gulp-uglify --save-dev
npm install gulp-concat --save-dev
```

### 2. 모듈 불러오기

> Gulp 사용 및 자동화를 위해 필요한 모듈을 변수에 선언

```
const uglify = require('gulp-uglify'),
      concat = reauire('gulp-concat');
```

### 3. 경로 설정

> 필요에 따라 유연하게 경로 지정

```
// 압축이 필요한 js 경로
const jsSrc = "src/project/_js/";
const jsPaths = {
 jsUi: jsSrc + 'ui/*.js',
 jsUtils: jsCrc + 'utils/*.js'
}

// 압축과 합쳐진 js 파일이 담길 경로
const jsDist = 'src/project/js';
```

### 4. minify 함수 생성

> 이미지가 추가되면 기존 이미지 스프라이트를 지우고, 새로 생성한다.

```
const minify = () => {
 return(
  gulp
    // 하위 디렉터리 내의 자바스크립트 파일을 가져온다.
   .src(jsPaths.jsUi, { sourcemaps: true })

   // 상단에서 가져온 js 파일들을 병합하고 해당 이름으로 파일을 생성
   .pipe( concat('conbined.js') ) 

   // 압축 uglify 실행
   .pipe(uglify())

   // 해당 디렉터리 경로에 담아준다.
   .pipe(gulp.dest(jsDist), { sourcemaps: true })
   .pipe(browserSync.reload({stream:true}))
);
}
```

### 5. watch

> 파일 내용의 변경을 감지하여, 변경 되었을 시 즉시 반영

```
const watch = () =>{
	gulp.watch(jsPaths.jsUi, minify);
}
	 

exports.build = gulp.parallel( minify, watch);

```

## 기타

### 나의 생각

- 


### 참고 블로그

- [npmjs](https://www.npmjs.com/package/gulp-concat)

- [uglify, concat](https://webclub.tistory.com/469)


