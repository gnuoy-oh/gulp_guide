# Variables

## 설명

- 반복적으로 사용되는 값을 변수로 지정할 수 있다.

- 변수 앞에 항상 $를 붙인다.

```
$변수이름: 속성값;

//SCSS
$color-error: #ff7564;
$url-image: "asset/images";

.area_content{
  color: $color-error;
  background: url($url-image + 'bg.png');
}
```

### 특징

- **변수 유효범위** - 변수는 선언된 블록({})내에서만 유효범위를 가진다.

  - 전역에서 선언하면 자유롭게 사용할 수 있다. 

  ```
  .box1 {
    $color: #111;
    background: $color;
  }
  // Error
  .box2 {
    background: $color;
  }
  ```

- **변수 재 할당** - 변수에 변수를 할당할 수 있다.

  ```
  $red: #FF0000;
  $blue: #0000FF;

  $color-primary: $blue;
  $color-danger: $red;

  .box {
    color: $color-primary;
    background: $color-danger;
  }
  ```

- **전역 설정** - !global

  - !global 플래그를 사용하면 변수의 유효범위를 전역으로 설정할 수 있다.

- **초깃값 설정** - !default

  - !default를 사용하면 할당되지 않은 변수의 초깃값을 설정한다.

  - 할당되어있는 변수가 있다면, 변수가 기존 할당 값을 사용한다.

## 기타

### 참고 블로그

- [sass-guidelin](https://sass-guidelin.es/ko/)

- [HEROPY-Tech-scss](https://heropy.blog/2018/01/31/sass/)

- [poiemaweb-scss](https://poiemaweb.com/sass-basics)
