# Import

## 설명

- 목적이나 기능에 따라서 각각 분리한 scss 파일들을 하나의 scss파일에 import 시켜 단일 css 파일로 병합한다.

- 본인의 목적에 따라서 css 파일을 2 ~ 3개로 나누어 import해도 무방하다.

```
// SCSS
@import "foo.scss";

// 확장자 생략 가능
@import "foo";

// 2개 이상의 scss 파일도 import 
@import "header", "gnb", "footer";
```

### 특징

- **partial**

  - 파일 이름 앞에 _(underscore)를 붙이면, @import로 가져오면 컴파일 시 css 파일로 컴파일 하지 않는다.

  - 즉, _를 붙인 scss파일은 import를 수행하되 css로의 컴파일은 수행하지 말라는 의미를 가진다. 따라서 최종적으로 compile을 수행할 Sass파일에서 import를 하면, 그 최종 파일에서만 compile을 하게 된다.

  ```
  // SCSS

  // underscore scss
  _varialbes.scss
  _header.scss
  _sidebar.scss
  _footer.scss

  // import scss
  style.scss
    @import "variables"
    @import "header"
    @import "sidebar"
    @import "footer"

  // compile
  style.css
  ```

- webpack이나 Parcel, Gulp 같은 일반적인 빌드툴에서는 partial 기능이 필요가 없다.

## 기타

### 참고 블로그

- [sass-guidelin](https://sass-guidelin.es/ko/)

- [HEROPY-Tech-scss](https://heropy.blog/2018/01/31/sass/)

- [poiemaweb-scss](https://poiemaweb.com/sass-basics)
