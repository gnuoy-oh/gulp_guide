# Gulp

## 세팅

### gulp4.0으로 세팅하기(기존 gulp3.0 삭제)

```
# 전역에 설치한 Gulp 제거
$ npm uninstall gulp --global
$ npm uninstall gulp-cli -g
# 프로젝트에 설치한 Gulp 제거
$ npm uninstall gulp --save-dev
# 캐시 삭제
$ npm cache clean # for npm < v5

# Gulp CLI 설치
$ npm install gulpjs/gulp-cli --global
# 프로젝트에 Gulp 4.0 설치
$ npm install gulpjs/gulp.git#4.0 --save-dev
```

### gulp4.0 추가된 기능

### 참고한 블로그

- https://stackoverflow.com/questions/33429727/how-do-i-install-gulp-4

- https://programmingsummaries.tistory.com/393