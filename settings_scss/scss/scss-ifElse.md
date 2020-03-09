# 조건과 반복

## 설명

- Js 같은 제어문을 사용할 수 있는 기능을 제공한다.

### 특징

### if (condition, if_true, if_false)

- Js의 삼항 연산자와 비슷한 형태로, 조건의 값 (true, false)에 따라 두 개의 표현식 중 하나만 반환한다.

```
// SCSS
$type: nature;

span{
  color: if($type === nature, green, blue ); // color: green;
}
```

### @if(지시어)

- 조건에 따른 분기 처리가 가능하며 if - else 문과 유사하다.

```
@if(조건){ 
  /* 조건이 참일 경우 실행될 구문 */
}

@if(조건){ 
  /* 조건이 참일 경우 실행될 구문 */
} @else {
  /* 조건이 거짓일 경우 실행될 구문 */
}

@if(조건){ 
  /* 조건이 참일 경우 실행될 구문 */
} @else if(조건2) {
  /* 조건2가 참일 경우 실행될 구문 */
} @else{
  /* 조건이 거짓일 경우 실행될 구문 */
}
```

- 예시

```
// SCSS
$color: orange;
div {
  @if $color == strawberry {
    color: #FE2E2E;
  } @else if $color == orange {
    color: #FE9A2E;
  } @else if $color == banana {
    color: #FFFF00;
  } @else {
    color: #2A1B0A;
  }
}

// css
div {
  color: #FE9A2E;
}
```

### @for

- 반복문을 수행할 수 있다.

```
// 종료 단계까지 반복
@fot $변수 form 시작 through 종료 {
 // 반복할 구문
}

// 종료 한단계 전까지 반복
@fot $변수 form 시작 to 종료 {
 // 반복할 구문
}
```

- 예시

```
// SCSS
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}

// css
.item-1 {
  width: 2em;
}
.item-2 {
  width: 4em;
}
.item-3 {
  width: 6em;
}
```

### @each

- List와 map 데이터를 반복할 때 사용한다.

- for in 문과 유사하다.

```
@each $변수 in 데이터 {
  // 반복 내용
}
```

- 예시

```
// SCSS
$fruits: (apple, orange, banana, mango);

.fruits {
  @each $fruit in $fruits {
    li.#{$fruit} {
      background: url("/images/#{$fruit}.png");
    }
  }
}

// css
.fruits li.apple {
  background: url("/images/apple.png");
}
.fruits li.orange {
  background: url("/images/orange.png");
}
.fruits li.banana {
  background: url("/images/banana.png");
}
.fruits li.mango {
  background: url("/images/mango.png");
}
```

### while

- 조건이 false로 평가될 때까지 내용을 반복한다.

- 잘못된 조건으로 인해 컴파일 중 무한 루프에 빠질 수 있어서 권장하지 않는다.

```
@while 조건 {
  // 반복 내용
}
```

- 예시

```
// SCSS
$i: 6;
@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}

// css
.item-6 {
  width: 12em;
}

.item-4 {
  width: 8em;
}

.item-2 {
  width: 4em;
}
```

## 기타

### 참고 블로그

- [sass-guidelin](https://sass-guidelin.es/ko/)

- [extend 부작용](https://sass-guidelin.es/ko/#extend)

- [HEROPY-Tech-scss](https://heropy.blog/2018/01/31/sass/)

- [poiemaweb-scss](https://poiemaweb.com/sass-basics)
