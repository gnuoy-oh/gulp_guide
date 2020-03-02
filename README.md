# 개인 역량 [Gulp, Scss]

팀 전략과제 대비 개인 역량으로 정리한 공간입니다.

## 주제

워크 플로우 자동화 도구인 Gulp와 Css전처리기인 Scss를 사용하여 보다 빠르고 효율적인 업무를 합니다.

## 내용

### gulp Basic

- **CSS**

	- gulp-scss : SCSS를 CSS로 컴파일을 합니다.

	- gulp-cssnano : css 작성 시 실수할 수 있는 요소들, 불필요하게 길게 작성하는 요소들을 정리해줍니다.

	- gulp-autoprefixer : 브라우저 지원을 위해 자동 접두사를 추가합니다.

	- gulp-postCss : 자바스크립트로 작성된 플러그인으로 autoprefixer를 생성합니다.

- **Javascript**

	- gulp-uglify : 파일에 포함된 주석, 공백 등을 제거하는 등 용량을 줄이고 압축을 해줍니다.

- **image**

	- gulp.spritesmith-multi : 이미지 스프라이트 자동화합니다.

- **Common**

	- browser-sync : 파일 변경 시 라이브 리로딩합니다.

	- gulp-rename: 컴파일, 압축 등의 작업을 거친 파일의 이름을 변경합니다.

	- gulp-concat: 컴파일, 압축 등의 작업을 거친 파일들을 원하는 파일에 합쳐줍니다.

---

### Scss Basic

- **중첩(Nesting)**

- **변수(Variables)의 사용**

- **mixin 를 사용한 Global Css 생성**

- **조건과 반복**

	- if else

	- for

	- while

	- each

## 환경

- Gulp: 4.0.2

- nodejs: 10.16.2

## 폴더 구조

- src/

	- gulpfile.js

	- package.json

- 프로젝트 작업 내용

	- settings/

		- gulp

		- scss

## 확인 필요

### 부족한 부분

- postCss, cssnano 디테일하게 공부 필요

- scss 더 디테일하게 정리할 것