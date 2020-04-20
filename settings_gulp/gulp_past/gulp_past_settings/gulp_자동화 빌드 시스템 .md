## Gulp

- 자동화 빌드 시스템

- 생산성을 높이고, 개발자들의 수고를 덜어줄 수 있는 유용한 도구로 Grunt, Gulp, Brunch, Bower 등이 있다.

- 사용자들이 반복적으로 수행하게 되는 일인, 자바스크립트와 CSS를 온라인 툴이나 기타 툴을 사용하여 파일의 용량을 줄이기 위해 압축,
병합을 시도한 후 수정 작업이 발생할 경우, 또 다시 일련의 반복작업을 하게 되는 것이 다반사인데, 이러한 반복적인 할 일들을
자동으로 대신 처리해주는 것이 자동화 빌드 시스템이다.

- sttaming build system을 표방하고 있다. 즉, Node의 스트림 기능으로 인해 이득을 얻는 빌드 시스템!!

    * Node.js는 이벤트 루프에 기반한 비동기 I/O를 제공한다.
    파일 시스템에서 읽기/쓰기 작업을 할 때나 HTTP 요청을 전달할 때 Node.js는 노드는 응답을 기다리는 동안 다른 이벤트들을 처리할 수 있는데, 
    이를 non-blocking I/O 라고 부른다. 
    Stream은 이보다는 더 확장된 개념으로 메모리 버퍼와 대역폭을 절약할 수 있는 이벤트 기반의 I/O 인터페이스를 제공하는 것을 말하는데,
    예를 들어, 스트림은 대용량 파일의 파일 같은 경우, 파일 전체를 모두 로드하기 전에 메모리 버퍼를 절약하기 위해 무엇인가 다른 일을 빠르게 처리할 수 있다.
    그래서 우리는 파일이 전체로 로드될 때까지 기다릴 필요없이 파일을 일부를 쓰거나 어떤 처리를 할 수 있게 되는 것입니다.
    * node.js의 특징인 event-driven, non-blocking I/O 를 바탕으로, 요청 후 한번에 결과를 받는 것이 아니라 이벤트로 중간중간 전달받는 방식을 stream이라고 하는데,
    이 stream 을 기반으로 하고 있기 때문에 실제로 작업 속도도 비교적 더 빠른 것으로 알려져있다.
    
- Gulp의 기능
    1. 웹 서버를 동작한다.
    
    2. Sass를 css로 컴파일 한다.
    
    3. 편집기 툴에서 파일을 저장할 때마다 웹브라우저를 reload하여 새로고침 없이 브라우저를 갱신한다.
    
    4. 배포를 위한 css, js, fonts, images 등 리소스를 최적화 한다. 
    
- 만약 운영으로 빌드한다면, 자바스크립트를 압축하고, 또 CSS 전처리기인 Sass 파일을 컴파일 하고, 코드에 오류는 없는지 체크를 하고 싶을 것이다.
이러한 작업을 수동으로 명령하지 않고, Gulp task를 작성하여 실행할 수 있다.


### A. 설치 방법  
    
1. gulp는 node.js의 스트림 기능을 기반으로 하고있기 때문에, node.js가 설치되어 있어야 한다.

    * Node.js는 자바스크립트를 개발언어로 사용하는 소프트웨어 플랫폼이다.
    구글 크롬 웹브라우저와 웹 브라우저에 탐재된 V8 엔진 위에서 동작하고, 프론트 측이 아닌, 서버 측에서 실행되는 서버사이드 언어이다.
    그리고 설치 과정 중에 npm package manage가 있는데, 이를 NPM이라고 하는데, Node.js 기반의 패키지 모듈을 관리하는 도구이다.

2. 설치가 끝나면 CLI에서 node --version을 실행하면, Node.js의 버전을 출력할 것이다.

    * CMD는 window 운영체제에서 기본으로 제공하는 명령어 기반 인터페이스(CLI) 도구이다.
    * MAC 에서는 terminal 등이 있다.

3. Node.js 기반의 모듈인 Gulp 패키지를 설치할 수 있다.
    
    * gulp 패키지 모듈을 설치하려면, NPM을 이용하여 손쉽게 설치할 수 있는데, 앞서 Node.js를 설치하는 과정 중에 npm의 설치 항목을 확인할 수 있다.
    * npm -v으로 잘 설치 되었는지 확인한다.
    
4. npm 관리도구를 이용해서, npm install gulp -global 로 패키지를 다운 받는다.

    * global은 아무 곳에서 gulp 명령어를 사용, 실행할 수 있도록 로컬 컴퓨터에 전역적(global) 설치를 하라고 npm에게 알려주는 명령어이다.
    * gulp -v 으로 gulp.js 버전을 확인할 수 있다.
    
5. gulp.js(gulp 모듈 패키지)를 사용자 프로젝트 디렉토리에 로컬 설치하기

- 대게 전역적으로 gulp를 설치했다 하더라도, 개별적인 프로젝트 에서 gulp를 사용하려면 로컬 설치가 필요하다!!!

- 이유는, 인터넷이 되지 않는 환경에서 전역에 설치한 gulp를 복사에서 설치할 수 있기 때문이다. 

    1. 시작하기에 앞 서, 사용자 프로젝트 디렉토리를 하나 생성하도록 한다.
    
    2. CLI에서 해당 디렉토리로 이동한 후 gulp 명령어를 실행해 보도록 한다.
    
    3. gulp // local gulp not found 메세지가 출력되면서 현재 디렉토리에서 로컬 gulp를 찾을 수 없다는 메시지가 뜸
        
        -이는 gulp 패키지가 설치되어 있어야만 gulp를 사용할 수 있다는 것을 의미함. 
    
    4. npm install gulp --save-dev
    
        - --save -dev : gulp와 관련된 디펜던시들은 애플리케이션 개발 과정까지만 필요하다. 
        
                - 디펜던시(의존성)?
                    
                    - 만약 제이쿼리를 사용하면, 제이쿼리를 불러온 다음에 문법을 사용한다. 이렇듯, 내가 사용하는 스크립트가
                    제이쿼리에 의존하고 있다면, 제이쿼리에 의존성을 가지고 있다고 할 수 있다.
                    
                    - 그래서 모듈을 설치할 때 (npm install) --save -dev 명령어를 입력하면, 개발할 때만 의존(dependendcies)하는 모듈로 기술된다.
                    
                    - 보통 개발 당시에만 gulp 플러그인 패키지가 필요하고, 배포 시에는 gulp 패키지 모듈은 서비스를 받는 사용자에게 필요가 없기 때문에, 
                    개발할 때만 의존하도록 --save-dev를 사용한다.
                    
                    - 만약 npm install gulp --seve 라고 하면, 배포할 때도 의존하는 모듈로 기슬된다.
                    
                    - --save-dev는 -D로 줄여서, --save 는 -S 로 사용할 수 있다.
            
    5. 사용자 프로젝트 디렉토리에 gulp를 로컬설치가 끝나면 Node 모듈을 관리하는, [node_modules] 디렉토리와 그 내부에는
    Gulp 모듈 패키지 디렉토리가 생성된다.
    
    6.  npm init (npm 초기화를 설정한다!)
    
        - npm init을 먼저 실행하고 4번 실행해도 무방하다.
    
        - NPM 명령어인 npm init은 초기화 명령어로, 사용자에게 질문을 하며 대답을 받는 형식으로, package.json 파일을 생성한다.
        
        - package.json은 배포(publish) 할 때 반드시 필요한 파일이다.
        
        - package.json 파일을 직접 생성할 수도 있지만, 처음 사용할 때는 초기화 명령어로 생성하는 것이 일반적이다.
    
        - name 을 시작으로 version, decription, 등의 여러 정보가 나오는데, enter를 눌러준다.
        
        - 마지막 is this ok ? 라는 질문이 나타나는데, enter를 누르면 package.json이 생성된다.
        
        - package.json 파일을 열면, 질문에 답변한 내용이 문서에 포함되어 있으며, 필요없는 부분은 삭제하여 정리할 수 있다.
        
    7. 이제 사용자 프로젝트 디렉터리에 gulp 설치를 마쳤으며, gulp가 수행할 일의 정의는 gulpfile.js 문서에 작성해야 한다.
    
        - 생성한 폴더 바로 아래에 gulpfile.js를 만들어야 한다.
    
            - 예시
            
                var gulp = require('gulp'); // gulp 모듈 호출
                
                gulp.task('defaulp', function(){
                
                    console.log('gulp default 일이 수행되었습니다~');
                    
                });
                
                작성 후, CLI에서 gulp default 를 명령하면 문자열이 출력, 수행이 된다!!!
                

### B. task  
 
 - 자바스크립트 파일을 조합하는 task에 대한 문법이다.
 
 - 전체 프로세스를 살펴보면, gulp는 gulp.src()를 통해 파일을 읽어오고, gulp.pipe 에서 수행된 일련의 작업들을 통해 결과물로 파일을 쓰게 되는 과정을 거친다. 
        
        //gulp 모듈 호출 
        var gulp = require('gulp');
        
        //gulp의 concat 패키지 모듈 호출
        var concat = require('gulp-concat');
        
        //...
        
        //gulp.task() 를 사용해 combine:js 테스크를 정의
        gulp.task('combine:js', ['lint-js'], function (){
            return gulp.src('/project/js/**/*.js')
                .pipe(concat('scriptAll.js'))
                .pipe(gulp.dest('progect/dist/js'));
        });
        
        //...
        
        gulp.task('default', ['combine:js']);
    
    - 위의 문법에 대해 살펴보자
    
           //gulp 모듈 호출 
           
           var gulp = require('gulp');
           
           //gulp의 concat 패키지 모듈 호출
           
           var concat = require('gulp-concat');
        
        - gulpfile을 사용하기 위해서는 제이쿼리 객체를 호출하듯이 require 해야할 필요가 있다.
        
        - 그리고, 다음 행의 gulp-concat의 패키지 모듈을 사용하기 위해서는 반드시 npm 으로 사용하려는 gulp 모듈 패키지를 설치해야 한다.
        
        - 다음과 같이 설치할 수 있다.
        
            - npm install gulp-concat --save-dev
        
    - gulp.task
    
            //gulp.task() 를 사용해 combine:js 테스크를 정의
            gulp.task('combine:js', ['lint-js'], function (){
                return gulp.src('/project/js/**/*.js')
                    .pipe(concat('scriptAll.js'))
                    .pipe(gulp.dest('progect/dist/js'));
            });
                    
        - gulp.task(name, deps, func)
        
            - gulp.task()는 gulp가 수행할 일을 정의하고, 이 메소드는 세개의 전달인자를 받는다. 2번째 파라미터는 생략이 가능
            
                    - name : task의 이름을 지정하고, 이름에는 공백이 포함되서는 안된다.
                    
                    - deps : 현재 선언하고 잇는 task를 수행하기 전에, 먼저 실행되어야 하는 task들의 배열 목록을 작성할 수 있다.
                        위의 예제에서는 JavaScript 파일을 병합하는 task를 진행하기 전에 JavaScript Lint(자바스크립트 문법 검사)를 먼저 수행하도록 정의되어 있음.
                        물론 그 전에 lint-js task를 이 task보다 앞에 작성해주어야 먼저 수행할 수 있을 것이다.)
                        
                    - func : 실제 수행할 업무 프로세스를 정의하는 function 이다. (처리해야할 일을 정의)
                    
                    - 만약 선행되어야 하는 task가 없다면, 굳이 gulp.task(name, [], func)의 형태로 두번째 파라미터를 줄 필요가 없고,
                        gulp.task('name', func); 로 정의해도 정상적으로 task를 수행할 수 있다.
                        
    - gulp. src(files)
    
        - gulp 객체의 src()에 대한 파일이나, 파일의 경로를 배열 데이터 형식(배열 또는 string)으로 작성하도록 한다.
        
        - 즉, 해당 task의 대상이 되는 파일들을 지정해주는 역할을 한다.
        
              1. return gulp.src('/project/js/**/*.js')
              
              2. 'project/src/js/navigation.js',
                 'project/src/js/slider/*.js',
                 '!project/src/js/slider/slider-beta.js'
                 
        - 1. 예제에서 처럼 js/**/*.js는, js 폴더와 내부 폴더의 .js 파일들을 모두 찾아서 가져올 수 있다.
        
        - 2. navigation.js 파일과, slider 안에 있는 모든 .js 파일을 가져오며, ! 표시 되어 있는 것은 포함하지 말라는 의미이다.
          
    - gulp.pipe(...)
    
            .pipe(concat('scriptAll.js'))
    
        - gulp의 task는 pipe로 연결되는데, (node.js stream의 그 pipe와 같다) 작업 대상 파일들이 pipe를 따라 흘러가며 병렬로 동시에 여러 task를 수행하게 된다.
        
        - gulp의 스트리밍 기능으로 'pipe'는 gulp.src에서 대상으로 지정된 각 파일들을 stream 형태로 읽어들여 다음으로 거쳐야 할 플러그인 등으로 연결할 때 사용하게 된다.
        
        - pipe 메소드를 사용해서 task들의 결과물을 function에게 전달해 줄 수 있으며, pipe가 하는 일은, pipe로 stream간에 read와 write event 들을 연결해 주는 것이다.
        
        - pipe 체이닝으로 여러개의 pipe를 서로 연결하여 사용할 수도 있다.
       
    - gulp.dest()
    
            .pipe(gulp.dest('progect/dist/js'));
            
        - 해당 task의 결과물이 저장 될 경로를 지정하게 된다.
        
        - 위 task에서 gulp는 이 파일을 gulp.dest()로 보내게 되는데, 이를 통해 실제로 사용하게 될 output 파일로 떨궈지게 된다.
        
        - 즉, dest()는 전달받은 인자(문자열)을 토대로 파일이 출력될 목적지(destination)를 설정하는 역할을 한다.
        
    - gulp.task('default', []);
    
            gulp.task('default', ['combine:js']);
        
        - CLI에서 아무런 argument 없이 gulp 명령어만을 타이핑하여 실행했을 때, 기본 값으로 실행되는 task
        

#### 도움받은 블로그

- https://webclub.tistory.com/467

- https://recoveryman.tistory.com/285
        
        
                    
                    
        
        
        
        
        
 
    
