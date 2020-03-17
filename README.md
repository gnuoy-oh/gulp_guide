# 개인 역량 [Gulp, Scss]

개인 역량으로 정리한 공간입니다.

## 주제

워크 플로우 자동화 도구인 Gulp와 Css전처리기인 Scss를 사용하여 보다 빠르고 효율적인 업무를 합니다.

## 내용

### gulp Basic

- **CSS**

	- gulp-scss : SCSS를 CSS로 컴파일을 합니다.

	- gulp-cssnano : css 작성 시 실수할 수 있는 요소들, 불필요하게 길게 작성하는 요소들을 정리해줍니다.

	- gulp-autoprefixer : 브라우저 지원을 위해 자동 접두사를 추가합니다.

	- gulp-postCss : 자바스크립트로 작성된 플러그인인 postCss로 autoprefixer를 생성합니다.

- **Javascript**

	- gulp-uglify : 파일에 포함된 주석, 공백 등을 제거하는 등 용량을 줄이고 압축을 해줍니다.

- **image**

	- gulp.spritesmith-multi : png 파일 형식의 이미지를 스프라이트 자동화합니다.

	- gulp-svg-sprite : svg 이미지를 스프라이트 자동화합니다.

- **Common**

	- browser-sync : 파일 변경시에 이를 자동으로 감지해서 브라우저 Refresh를 수행합니다.

	- gulp-rename: 컴파일, 압축 등의 작업을 거친 파일의 이름을 변경합니다.

	- gulp-concat: 컴파일, 압축 등의 작업을 거친 파일들을 원하는 파일에 합쳐줍니다.

	- del : 특정 디렉토리를 삭제해줍니다.

	- merge-stream : 원하는 파일의 스트림을 병합합니다.

	- gulp-size : 해당 작업 파일 크기를 출력합니다. (Cli에 minifyjs 1.4kB 으로 출력)

  - gulp-util : 컬러 메시지등 로그를 쉽게 화면에 출력합니다.

---

### Scss Basic

- **Variables**

- **Nesting**

- **Mixin**

- **조건문과 반복문**

	- if else

	- for

	- while

	- each

- **Import / export**

- **Extend**

## 환경

- Gulp: 4.0.2

- nodejs: 10.16.2

## 폴더 구조

- src/

- gulpfile.js

- package.json

- node_modules/

- README.md

- settings_gulp/

	- README.md

	- gulp/

- settings_scss

	- README.md

	- scss/

## 기타

### 나의 생각

- postCss, cssnano 디테일하게 공부 필요

- scss 더 디테일하게 정리할 것

- gulp-svg 추가하자 
