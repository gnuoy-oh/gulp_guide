# Extend

## 설명

- 확장 - 기존 스타일을 상속하고자 할 경우 @extend를 사용한다.

- **@extend 선택자;**

```
// SCSS
.btn{
  padding: 10px;
  background: blue;
}
.btn_danger{
  @extend .btn;
  background: red;
}

// css
.btn, .btn_danger{ 
  padding: 10px;
  background: blue;
}
.btn_danger{
  background: red;
}

```

### 특징

- @media 안에서 외부의 선택자를 extend 할 수 없다. 

- @extend를 사용하면 컴파일 후 자신의 셀렉터가 어디에 첨부될 것인지 예상하기 어렵고, 예상치 못했던 부작용이 발생할 수 있다. 따라서 @extend의 사용은 가급적 자제하고 Mixin은 사용하는 것을 추천한다.

## 기타

### 참고 블로그

- [sass-guidelin](https://sass-guidelin.es/ko/)

- [extend 부작용](https://sass-guidelin.es/ko/#extend)

- [HEROPY-Tech-scss](https://heropy.blog/2018/01/31/sass/)

- [poiemaweb-scss](https://poiemaweb.com/sass-basics)
