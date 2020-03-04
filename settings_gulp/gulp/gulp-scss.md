# gulp-sass

- with **gulp-autoprefixer, gulp-rename, gulp-postCss, culp-cssnono**

  - gulp-scss : SCSS를 CSS로 컴파일을 합니다.

  - gulp-cssnano : css 작성 시 실수할 수 있는 요소들, 불필요하게 길게 작성하는 요소들을 정리해줍니다.

  - gulp-autoprefixer : 브라우저 지원을 위해 자동 접두사를 추가합니다.

  - gulp-postCss : 자바스크립트로 작성된 플러그인인 postCss로 autoprefixer를 생성합니다.

  - gulp-rename: 컴파일, 압축 등의 작업을 거친 파일의 이름을 변경합니다.

## 설명

### 1. 모듈 설치

> 작업에 필요한 Plugin 설치 

```
npm install gulp-sass --save-dev
npm install gulp-rename --save-dev
npm install autoprefixer --save-dev
npm install cssnano --save-dev
npm install gulp-postCss --save-dev
```

### 2. 모듈 불러오기

> Gulp 사용 및 자동화를 위해 필요한 모듈을 변수에 선언

```
const sass = require("gulp-sass"),
      rename = require("gulp-rename"),
      autoprefixer = require("autoprefixer"),
      cssnano = require("cssnano"),
      postcss = require("gulp-postcss");
```

### 3. 경로 설정

> 필요에 따라 유연하게 경로 지정

```
// 담겨있는 scss 파일 상위 경로
const src = "src/project/_sass";

// 담겨있는 scss 파일 하위 경로
const paths = {
 utilsCss: src + "/utils/*.scss",
 layoutCss: src + "/layout/*.scss"
};

// 컴파일된 css가 담길 경로
const dist = "src/project/css";

// scss compile 되는 방식 
const sassOptions = {
 outputStyle: "compact",
 indentType : "tab",
 indentWidth : 1,
 precision: 6,
 sourceComments: false
}
```

### 4. scss 함수 생성

> scss컴파일 작업과 동시에 파일 이름 변경, autoprexifer 작업

```
const scssUtils = () => {
 return (
  gulp
  .src(paths.utilsCss, { sourcemaps: true })

  // scss 옵션 설정
  .pipe(sass(sassOptions))
  .on("error", sass.logError)

  // autoprefixer 적용, cssnano 실행
  .pipe(postcss([autoprefixer({}), cssnano()]))

  // 원하는 이름으로 수정
  .pipe(rename('utils.css'))
  .pipe(gulp.dest(dist), { sourcemaps: true })
  .pipe(browserSync.stream())
  .pipe(browserSync.reload({stream:true}))
 );
}
```

### 5. watch

> 파일 내용의 변경을 감지하여, 변경 되었을 시 즉시 반영

```
function watch() {
  // paths.utilsCss가 수정이 되었을 경우 바로 scssUtils를 실행한다.
 gulp.watch(paths.utilsCss, scssUtils);
}
  
exports.build = gulp.parallel(scssUtils, watch);

```

### 6. package.jon 추가할 내용

> autoprefix 설정: 브라우저 지원 범위 지정

```
"browserslist": [
 "last 2 versions",
 ">1%"
]
// gulpfile.js 내부에 지정을 하니 경고창이 발생해서 package.json에 설정
```

## 기타

### 나의 생각

- autoprefix 관련해서 디테일하게 파악 필요


### 참고 블로그

- [gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer)

- [postCss - autoprfixer](https://medium.com/jung-han/postcss-%ED%86%A0%EC%8A%A4%ED%8A%B8%ED%8C%8C%EC%9D%BC-%EC%A0%81%EC%9A%A9%EA%B8%B0-86cd33ba6aa9)

- [postCss](https://medium.com/@FourwingsY/postcss-%EC%86%8C%EA%B0%9C-727310aa6505)