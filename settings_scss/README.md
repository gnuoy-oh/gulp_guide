# Sass(Syntactically Awsome StyleSheets)

## 설명

- Sass는 CSS pre-processor(전처리기)로서 CSS의 한계와 단점을 보완하여 가독성이 높고, 코드 재사용에 유리한 CSS를 생성하기 CSS의 확장이라고 할 수 있다.

	- Variables

	- 조건문과 반복문

	- Import / export

	- Nesting

	- Mixin

	- Extend


## Sass 환경 설치

- 웹 브라우저에서는 직접 동작하지 않으므로, SCSS로 작성한 전처리기를 웹에서 동작 가능한 표준의 CSS로 컴파일을 해야한다.

### gulp-sass

- [markup_nathalie의 gulp-sass설치](https://github.kakaocorp.com/nathalie-my/makrup_nathalie/blob/master/settings_gulp/gulp/gulp-scss.md)

### node-sass

- Node.js를 컴파일러인 LibSass에 바인딩한 라이브러리로, npm global install하여 사용한다.

	```
	// Global Install
	npm install -g node-sass

	// 버전 확인
	node-sass -v 

	node-sass 4.12.0  (Wrapper) [JavaScript]
	libsass   3.5.4 (Sass Compiler) [C/C++]
	```

- **compile**

	1. foo.scss 파일을 sass-project 폴더에 생성한다.

	2. 컴파일 할 SCSS 파일의 경로와 컴파일 후, 생성될 css 파일의 경로를 지정한다.

	```
	cd scss-project

	// 특정 파일을 특정 파일 이름으로 컴파일 하는 방법
	node-sass foo.scss > var.css

	// 폴더 내의 모든 파일을 컴파일 하는 방법
	node-sass src/sass --output dist/css
	```

- **style**: scss 파일을 컴파일하여 css 파일을 생성할 때 4가지 스타일을 지정할 수 있다.

	1. nested: sass형식과 유사하게 nested된 css 파일이 생성된다. (기본값)

	```
	node-sass --output-style nested src/scss --output dist/css
	```

	2. expanded: 표준적인 스타일의 css파일이 생성된다.

	```
	node-sass --output-style expanded src/scss --output dist/css
	```

	3. compact: 여러 룰셋을 한 줄로 나타내는 스타일의 css파일이 생성된다.

	```
	node-sass --output-style compact src/scss --output dist/css
	```

	4. comporessed: 가능한 빈공간이 없는 압축된 스타일의 css파일이 생성된다.

	```
	node-sass --output-style compressed src/scss --output dist/css
	```

- **watch**: scss파일의 변경을 감지하여 변경될 때마다 scss파일을 컴파일하여 파일을 자동 업데이트 한다.

	1. 파일 단위의 watch

	```
	cd my-project

	node-sass --watch src/scss/foo.scss --output dist/css
	```

	2. 폴더 단위의 watch

	```
	cd my-project

	node-sass --watch src/scss --output dist/css
	```

### Ruby Sass

- Window 기준 Ruby Installer 설치 필요

- Mac 기준 npm install

```
// install
gem install sass

// 버전 확인
Sass -v

Sass 3.5.1
```

## 정보

### **Sass와 SCSS 의 차이**

- SCSS는 CSS 구문과 완전히 호환되도록 새로운 구문 도입해 만든 Sass의 모든 기능을 지원하는 CSS의 상위 집합니다. 즉, SCSS는 CSS와 거의 같은 문법으로 Sass를 지원한다.

- SCSS는 중괄호(**{}**)와 세미콜론(**;**)을 사용한다.

```
//Sass
.list
  width: 100px
  float: left
  li
    color: red
    background: url("./image.jpg")
    &:last-child
      margin-right: -10px

// SCSS
.list {
  width: 100px;
  float: left;
  li {
    color: red;
    background: url("./image.jpg");
    &:last-child {
      margin-right: -10px;
    }
  }
}
```

## 기타

### 나의 생각

- 

### 참고 블로그

- [sass-guidelin](https://sass-guidelin.es/ko/)

- [HEROPY-Tech-scss](https://heropy.blog/2018/01/31/sass/)

- [poiemaweb-scss](https://poiemaweb.com/sass-basics)
