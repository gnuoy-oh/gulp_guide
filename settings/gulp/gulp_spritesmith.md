# gulp.spritesmith-multi

- with **del, merge-stream**

## 설명

### 1. 모듈 설치

> 작업에 필요한 Plugin 설치 

```
// Cli install
npm install gulp.spritesmith-multi --save-dev
npm install del --save-dev
npm install merge-stream --save-dev
```

### 2. 모듈 불러오기

> Gulp 사용 및 자동화를 위해 필요한 모듈을 변수에 선언

```
// 모듈 변수 선언
const spritesmith = require('gulp.spritesmith-multi'),
	    del = require('del'),
	    merge = require('merge-stream');
```

### 3. 경로 설정

> 필요에 따라 유연하게 경로 지정

```
// 분리되어 있는 이미지 파일 경로
const imgSrc = 'src/project/image/_sprite/icon/*.png';
// 이미지 스프라이트 파일 담길 경로
const spriteImg = 'src/project/image/sprite';
// 이미지 스프라이트 css 파일 담길 경로
const spriteImgCss= 'src/project/_sass/utils';
```

### 4. sprite 함수 생성

> 기존에 존재하는 스프라이트 이미지을 삭제하고, 자동 이미지스프라이트 생성

```
// clean sprite
const cleanSprite = () => {
	return del(spriteImg);
}

//image sprite
const autoSprite = () => {
	let opts= {
		spritesmith: function(options, sprite, icons){
			options.imgPath =  `src/project/image/sprite/${options.imgName}`;
			options.cssName = `_icon_comm.scss`;
			options.cssTemplate = null;
			options.cssSpritesheetName = "ico_comm";
			options.padding = 4;
			options.cssVarMap =  function(sp) {
				sp.name = `${sp.name}`;
			};
			return options;
		}
	};
	let spriteData = gulp
		.src(imgSrc, { sourcemaps: true })
		.pipe(spritesmith(opts))
		.on('error', function (err) {
			console.log(err)
		});

	let imgStream = spriteData.img.pipe(gulp.dest(spriteImg));
	let cssStream = spriteData.css.pipe(gulp.dest(spriteImgCss));
 
	return merge(imgStream, cssStream);
}
```

### 5. watch

> 파일 내용의 변경을 감지하여, 변경 되었을 시 즉시 반영

```
function watch() {
  // paths.utilsCss가 수정이 되었을 경우 바로 scssUtils를 실행한다.
 gulp.watch(paths.utilsCss, scssUtils);
}
  
exports.build = gulp.parallel(scssUtils, watch);

```

### 6. package.jon 추가할 내용

> autoprefix 설정: 브라우저 지원 범위 지정

```
// package.json
"browserslist": [
 "last 2 versions",
 ">1%"
]
// gulpfile.js 내부에 지정을 하니 경고창이 발생해서 package.json에 설정
```

### 정보

### 궁금한 부분 

- autoprefix 관련해서 디테일하게 공부 필요!


### 참고 블로그

- [Autoprefixer](https://evilmartians.com/chronicles/autoprefixer-7-browserslist-2-released)

- [gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer)

- [postCss - autoprfixer](https://medium.com/jung-han/postcss-%ED%86%A0%EC%8A%A4%ED%8A%B8%ED%8C%8C%EC%9D%BC-%EC%A0%81%EC%9A%A9%EA%B8%B0-86cd33ba6aa9)

- [postCss](https://medium.com/@FourwingsY/postcss-%EC%86%8C%EA%B0%9C-727310aa6505)