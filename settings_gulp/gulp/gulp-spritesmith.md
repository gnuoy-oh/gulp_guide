 # gulp.spritesmith-multi

- with **del, merge-stream**

	- gulp.spritesmith-multi : 이미지 스프라이트 자동화합니다.

	- del : 특정 디렉토리를 삭제해줍니다.

	- merge-stream : 원하는 파일의 스트림을 병합합니다.

## 설명

### 1. 모듈 설치

> 작업에 필요한 Plugin 설치 

```
npm install gulp.spritesmith-multi --save-dev
npm install del --save-dev
npm install merge-stream --save-dev
```

### 2. 모듈 불러오기

> Gulp 사용 및 자동화를 위해 필요한 모듈을 변수에 선언

```
const spritesmith = require('gulp.spritesmith-multi'),
      del = require('del),
      merge = reauire('merge-stream);
```

### 3. 경로 설정

> 필요에 따라 유연하게 경로 지정

```
// 분리되어있는 이미지가 들어있는 경로
const imgSrc = 'src/project/image/_sprite/icon/*.png';

// 스프라이트 이미지가 담길 경로
const spriteImg = 'src/project/image/sprite';

// 스프라이트 이미지 css가 담길 경로 
const spriteImgCss= 'src/project/_sass/utils';
```

### 4. image-sprite 함수 생성

> 이미지가 추가되면 기존 이미지 스프라이트를 지우고, 새로 생성한다.

> 1. 기존에 생성된 스프라이트 이미지를 삭제

```
const cleanSprite = () => {
	return del(spriteImg);
}
```

> 2. 이미지 스프라이트 생성

```
const autoSprite = () => {

 // gulp 스프라이트 생성 시 옵션 설정
 let opts= {
  spritesmith: function(options, sprite, icons){
   // 이미지 스프라이트 생성 경로 
   options.imgPath =  `spriteImg/${options.imgName}`;

   // 생성되는 이미지 스프라이트 scss 파일명
   options.cssName = `_icon_comm.scss`;

   // 생성되는 scss 가이드 제공
   options.cssTemplate = null;

   // 전처리 템플릿의 스프라이트 시트 관련 변수에 사용할 이름
   options.cssSpritesheetName = "ico_comm";

   // 이미지 간 간격 설정
   options.padding = 4;

   // CSS 변수 이름을 사용자 정의
   options.cssVarMap =  function(sp) {
   sp.name = `${sp.name}`;
  };

  return options;
 }
};

let spriteData = gulp
 // 탐색 할 이미지 경로
 .src(imgSrc, { sourcemaps: true })

 // gulp 스프라이트 옵션 실행
 .pipe(spritesmith(opts))

 // gulp error 발생 시 콘솔 출력
 .on('error', function (err) {
 console.log(err)
});

let imgStream = spriteData.img.pipe(gulp.dest(spriteImg));
let cssStream = spriteData.css.pipe(gulp.dest(spriteImgCss));

// 이미지 추가 -> css 추가
return merge(imgStream, cssStream);
}

```

### 5. watch

> 파일 내용의 변경을 감지하여, 변경 되었을 시 즉시 반영

```
const watch = () =>{
 // imgSrc 수정이 되었을 경우 바로 cleanSprite, autoSprite를 실행한다.
 gulp.watch(imgSrc, cleanSprite);
 gulp.watch(imgSrc, autoSprite);
}
	 
exports.build = gulp.parallel( autoSprite, watch);
```

## 기타

### 나의 생각

- sprite option 설정하는 부분 디테일하게 파악 필요


### 참고 블로그

- [이미지 스프라이트 자동화 하기](https://dohoons.com/blog/1339/)

- [npmjs](https://www.npmjs.com/package/gulp.spritesmith-multi)

- [npmjs](https://www.npmjs.com/package/gulp.spritesmith)


