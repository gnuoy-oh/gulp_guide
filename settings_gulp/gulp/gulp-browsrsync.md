# browser-sync

- browser-sync : 파일 변경시에 이를 자동으로 감지해서 브라우저 Refresh 를 수행할 수 있습니다. 

- node.js 기반의 어플리케이션으로 Gulp Plugin이 아닙니다.

## 설명

### 1. 모듈 설치

> 작업에 필요한 application 설치 

```
npm install browser-sync --save-dev
```

### 2. 모듈 불러오기

> Gulp 사용 및 자동화를 위해 필요한 모듈을 변수에 선언

```
const browserSync = require("browser-sync").create();
```

### 3. browser-sync 함수 생성

> 웹서버를 띄워서 작업해보자

```
const server = () => {
 return(
  browserSync.init({
  startPath: '/',
  server: {
  // 해당 폴더 기준으로 웹서버를 구동한다.
  baseDir: `src/project`, 

  // 디렉터리 구조를 기반으로 라우트를 구성한다
  directory: true, 
},
  // 해당 포트로 페이지를 확인한다.
  port: 4000,
  open: true,
  })
 )
}
```

### 4. watch

> 파일 내용의 변경을 감지하여, 변경 되었을 시 즉시 반영

```
const watch = () =>{
 gulp.watch("src/project/html/*.html");
}

exports.build = gulp.parallel( server, watch);

```
## 기타

### 나의 생각

- vscode에서 Live Server로 작업해도 된다.


### 참고 블로그

- [Browser-sunc Docs](https://browsersync.io/docs/gulp)

- [Browser-sync](https://webclub.tistory.com/473)
