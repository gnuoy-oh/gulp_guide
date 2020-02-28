# gulp-sass

## 세팅

### code

```
//setting
npm install gulp-sass --save-dev
npm install gulp-rename --save-dev
npm install autoprefixer --save-dev

//start
var sass = require("gulp-sass"),
 rename = require("gulp-rename"),
 autoprefixer = require("autoprefixer");

// scss root
var src = "src/project/_sass";
var paths = {
 utilsCss: src + "/utils/*.scss",
 layoutCss: src + "/layout/*.scss"
};
var dist = "src/project/css";

// scss options
var sassOptions = {
 outputStyle: "compact",
 indentType : "tab",
 indentWidth : 1,
 precision: 6,
 sourceComments: false
}

//scss
function scssUtils() {
 return (
  gulp
  .src(paths.utilsCss, { sourcemaps: true })
  .pipe(sass(sassOptions))
  .on("error", sass.logError)
  .pipe(autoprefixer({}))
  .pipe(rename('utils.css'))
  .pipe(gulp.dest(dist), { sourcemaps: true })
  .pipe(browserSync.stream())
  .pipe(browserSync.reload({stream:true}))
 );
}

// watch
function watch() {
 gulp.watch(paths.utilsCss, scssUtils);
}
  
exports.build = gulp.parallel( scssUtils, watch);

//package.json add
"browserslist": [
 "last 2 versions",
 ">1%"
]
```
### 정보

### 궁금한 부분 

- AAA


### 참고한 블로그

- AAA

