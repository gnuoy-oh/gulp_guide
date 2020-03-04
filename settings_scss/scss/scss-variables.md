# Variables

## 설명

- Sass는 선언을 중첩할 수 있다.

- 상위 선택자 선언의 반복을 피할 수 있고, 좀 더 편리하게 자식 셀렉터를 기술 할 수 있다.

```
//SCSS
.container{
  width: 100%;
  .area_content{
    padding: 20px;
    ul {
      overflow: hidden;
    }
  }
}

//css
.container{width: 100%;}
.container .area_content{padding: 20px;}
.container .area_content ul{overflow: hidden;}

```

### 부모 요소 참조하기

- 중첩 안에서 &는 부모 선택자를 참조하여 치환한다.

```
// 예1

// SCSS
.btn{
  position: relative;
  &:after{
    content: '.';
    position: absolute;
    top: 0;
    left: 0;
  }
}

//css
.btn{position: relative};
.btn:after{content:'';position: absolute;top: 0;left: 0;}


// 예2

//SCSS
.text{
  &-small{font-size: 12px;}
  &-medium{font-size: 16px;}
  &-large{font-size: 20px;}
}

//css
.text-small{font-size: 12px;}
.text-medium{font-size: 16px;}
.text-large{font-size: 20px;}
```

### 중첩 벗어나기

- 중첩을 벗어나고 싶을 때 @at-root 키워드를 사용한다.

- 중첩 안에서 생성하되, 중첩 밖에서 사용해야 하는 경우에 유용하다.

```
// SCSS
ul{
  $w: 100px;
  $h: 50px;
  li{
    width: $w;
    height: $h;
  }

  @at-root .box{
    width: $w;
    height: $h;
  }
}

// css
ul li{width: 100px; height: 50px;}
.boa{width: 100px; height: 50px;}

// 오류의 예
.list {
  $w: 100px;
  $h: 50px;
  li {
    width: $w;
    height: $h;
  }
}

// Error
.box {
  width: $w;
  height: $h;
}
```

### 속성에서도 중첩을 사용하기

- css속성도 중첩이 가능하다.

```
// SCSS
.area_content{
  font: {
    weight: bold;
    size: 12px;
    family: sans-serif;
  }
  margin: {
    top: 10px;
    bottom: 20px;
  }
}

// css
.area_content{
  font-weight: bold;
  font-size: 12px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-bottom: 20px;
}
```

## 기타

### 참고 블로그

- [sass-guidelin](https://sass-guidelin.es/ko/)

- [HEROPY-Tech-scss](https://heropy.blog/2018/01/31/sass/)

- [poiemaweb-scss](https://poiemaweb.com/sass-basics)
