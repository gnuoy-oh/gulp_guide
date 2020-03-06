# Mixin

## 설명

- 스타일 시트 전체에서 중복 기술을 방지하기 위해, 재사용 할 CSS 선언 그룹을 정의하는 기능이다.

- @mixin을 선언하고, @include으로 적용한다.

```
// SCSS
@mixin clearfix{
    &:after{
        content: '';
        display: block;
        clear: both;
        width: 100%;
    }
}

ul{
  @include clearfix;
}

// css
ul{
  &:after{
    content: '';
    display: block;
    clear: both;
    width: 100%
  }
}
```

### 특징

- **argument**를 사용할 수 있다.

  - 전역에서 선언하면 자유롭게 사용할 수 있다. 

  ```
  // SCSS
  @mixin list-dot( $top, $left, $width, $height, $bgColor ) {
      position: absolute;
      top: $top;
      left: $left;
      width: $width;
      height: $height;
      margin-top: -($width/2)px;
      border-radius: 50%;
      background-color: $bgColor;
  }

  ul{ 
    li{
      @include list-dot(0, 0, 4px, 4px, #08c);
    }
  }

  // css
  ul li {
      position: absolute;
      top: 0;
      left: 0;
      width: 4px;
      height: 4px;
      margin-top: -2px;
      border-radius: 50%;
      background-color: #08c;
  }
  ```

- **초깃값**을 설정할 수 있다.

  ```
  // SCSS
  @mixin circle($size: 10px) {
    width: $size;
    height: $size;
    border-radius: 50%;
  }

  .box {
    // 인자가 없으면 초기값을 사용한다.
    @include circle();
    background: #f00;
  }

  // css
  .box {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #f00;
  }
  ```

## 기타

### 참고 블로그

- [sass-guidelin](https://sass-guidelin.es/ko/)

- [HEROPY-Tech-scss](https://heropy.blog/2018/01/31/sass/)

- [poiemaweb-scss](https://poiemaweb.com/sass-basics)
