# gulp-svg

- with **gulp-size, gulp-util**

  - gulp-svg-sprite : svg 이미지를 스프라이트 자동화합니다.

  - gulp-size : 해당 작업 파일 크기를 출력합니다. (Cli에 minifyjs 1.4kB 으로 출력)

  - gulp-util : 컬러, 메시지 등 로그를 쉽게 화면에 출력합니다.

## 설명

### 1. 모듈 설치

> 작업에 필요한 Plugin 설치 

```
npm install gulp-svg-sprite --save-dev
npm install gulp-size --save-dev
npm install gulp-util --save-dev
```

### 2. 모듈 불러오기

> Gulp 사용 및 자동화를 위해 필요한 모듈을 변수에 선언

```
const svgSprite = require('gulp-svg-sprite'),
      util = require('gulp-util'),
      size = reauire('gulp-size');
```

### 3. 경로 설정

> 필요에 따라 유연하게 경로 지정

```
//
const basePaths = {
 src: 'build/',
 dest: 'html/assets/',
};

//
const paths = {
 images: {
  src: basePaths.src + 'img/',
  dest: basePaths.dest + 'img/'
 },
 sprite: {
  src: basePaths.src + 'sprite/*',
  svg: 'img/sprite.svg',
  css: '../../' + basePaths.src + 'sass/src/_sprite.scss'
 },
 templates: {
 src: basePaths.src + 'tpl/'
 }
};
```

### 4. autoSpriteSvg 함수 생성

> svg sprite 생성

```
// 실시간 감지
const changeEvent = (evt) => {
	gutil.log('File', gutil.colors.cyan(evt.path.replace(new RegExp('/.*(?=/' + basePaths.src + ')/'), '')), 'was', gutil.colors.magenta(evt.type));
};

const autoSpriteSvg = () => {
  return (
    gulp
      .src(paths.sprite.src)
      .pipe(svgSprite({
       shape: {
        spacing: {
         padding: 5
        }
       },
       mode: {
        css: {
         dest: "./",
         layout: "diagonal",
         sprite: paths.sprite.svg,
         bust: false,
         render: {
          scss: {
           dest: "css/src/_sprite.scss",
           template: "build/tpl/sprite-template.scss"
          }
         }
        }
       },
       variables: {
        mapname: "icons"
        }
       }))
        .pipe(gulp.dest(basePaths.dest));
  )
}
```

### 5. watch

> 파일 내용의 변경을 감지하여, 변경 되었을 시 즉시 반영

```
const watch = () =>{
 gulp.watch(paths.sprite.src, ['sprite']).on('change', function(evt) {
  changeEvent(evt);
 });
}
	 

exports.build = gulp.parallel( sprite, watch);

```

## 기타

### SVG를 활용하는 방법

- **svg-sprite 이용**

  - mode: css으로 작업

- **symbol 이용**

  - mode: symbol으로 작업

### 나의 생각

- 주석 추가 필요, 이해 아직 다 못함 


### 참고 블로그

- [npmjs](https://www.npmjs.com/package/gulp-svg-sprite)
- [gulp+svg](https://www.liquidlight.co.uk/blog/creating-svg-sprites-using-gulp-and-sass/)
- [gitHub](https://github.com/liquidlight/sass-gulp-svg-sprite/blob/master/gulpfile.js)
- [gulp + scss](https://www.liquidlight.co.uk/blog/creating-svg-sprites-using-gulp-and-sass/)

