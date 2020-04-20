## Gulp

### C. Gulp 플러그인 사용하기  
 
-  웹 개발에 유용한 업무를 등록하는 과정을 알아보기, gulp 플러그인을 활용해보자! 

#### 1. gulp-concat

1. gulp-concat

        npm install gulp-concat --save-dev
        
    - 여러개의 자바스크립트 파일을 하나로 병합해 주는 플러그인이다.
    
    - 설치가 끝나면 [node_modules] 디렉터리에 gulp-concat 모듈 패키지가 생성된 것을 확인할 수 있다.
        
    - 여러개의 플러그인을 한꺼번에 내려받을 경우

            npm install gulp-concat gulp-uglify gulp-sass gulp-livereload --save-dev
        
    - CLI에서 위 명령어를 실행하면 gulp-concat, gulp-uglify, gulp-sass, gulp-livereload 총 네개를 한번에 내려 받는 것
    
2. gulp-concat 모듈을 호출하는 코드와, gulp.task() 메소드에 업무 이름을 부여하고 정의하기

    - script01.js / script02.js 이 두개의 파일을 병합하려고 하는 혐태

            //modules 호출
            var gulp = require ('gulp');
            
            //gulp의 concat 패키지 모듈 호출
            var concat = require('gulp-concat');
            
            //gulp.task()를 사용해 gulp-concat 업무 수행을 정의한다.
            //task의 이름은 가능하면 플러그인과 연관성 있는 이름을 정의하는 것이 좋다.
            //여기서는 concat:js라고 task 이름을 정의했음
            gulp.task('concat:js', function(){
            
                //gulp 객체의 src()에 병합하려는 자바스크립트 파일 경로를 배열 데이터 형식으로 추가했다.       
                return gulp.src(['project/src/js/script-01.js', 'project/src/js/script-02.js])
                
                //gulp-concat 모듈을 호출하여 참조한 concat() 함수에 병합한 후 생성할 파일 이름을 문자열로 전달했다.
                    .pipe( concat('conbined.js')
                    
                //gulp.dest()메소드가 수행되는데, 윗 라인에서의 pipe가 수행한 결과물이 출력될 목적지를 설정했다.
                    .pipe( gulp.dest('project/dist/js') );
            });
        
             //gulp.task('default', ['concat:js']);
             
    - 아래와 같이, CLI에서 gulp를 실행하면 폴더 내에 병합된 파일이 생성된다.

            gulp concat:js
        
    - 가장 하단, 주석을 지우고 CLI에서 gulp를 실행하면, gulp concat:js를 실행하지 않아도, gulp가 수행된다!        
            
            gulp.task('default', ['concat:js']);
    
        - 두번째 파라미터는 의존 모듈을 정의할 수 있는데, task('default')는 gulp 기본 명령어를 의미하고, 다른 task 네이밍을 배열로 전달함으로써
          gulp default인 gulp를 실행하게 될때, 의존성을 가진 task들을 먼저 수행하기 때문에 명시적으로 gulp concat:js를 작성할 필요가 없다.
          즉, 'default' 이름으로 정의된 task를 수행하게 된다.          
          
        - 또한 gulp 명령어를 실행하면 concat:js 업무가 시작해서 종료 할 때 까지 **밀리초(ms) 소요 되었다고 CLI창에 출력한다.
        
        - 즉, 자바스크립트 파일을 병합한 파일을 목적지게 생성하는데 **밀리초가 소요된 것이라고 할 수 있다.

3. 그런데, 병합할 파일 갯수가 늘어날 때마다 매번 배열 아이템을 추가해줘야 하는 번거로움이 발생할 것이다. 이러한 불편함을 해소하려면 자바스크립트 파일을 의미하는 문자열 (*.js) 으로 변경할 수 있다.

    - 아래와 같이 gulpfile.js를 변경하고 또 다른 script 파일을 하나 더 생성하여 CLI에서 gulp 명령어를 실행하면, 모든 스크립트 파일이 병합된 하나의 스크립트 파일을 얻을 수 있다.
    
            //modules 호출
            var gulp = require ('gulp');
            
            //gulp의 concat 패키지 모듈 호출
            var concat = require('gulp-concat');
               
               //gulp.task()를 사용해 gulp-concat 업무 수행을 정의한다.
               gulp.task('concat:js', function () {
               
                    return gulp.src(['project/src/js/*.js})
                     .pipe( concat('conbined.js')
                     .pipe( gulp.dest('project/dist/js') );
                        
            });
        
              gulp.task('default', ['concat:js']);
    
4. 하지만, 파일간의 병합이 알파벳 순서대로 병합되기 때문에 스크립트 처리 순서에 이슈가 발생할 수 있다. 

    - 그러므로 우선적으로 병합할 필요성이 있으면, 우선적으로 파일 경로를 먼저 제공한 다음 모든 파일을 의미하는 문자열을 배치하면, 특정 파일을 우선적으로 병합할 수 있다.

            var gulp = require('gulp');
            
            var concat = require('gulp-concat');
            
            gulp.task('concat:js' , function(){
            
                //우선적으로 병합 할 특정 파일을 먼저 작성
                return gulp.src(['project/src/js/script03' , 'project/src/js/*.js'])
                    .pipe( concat('conbined.js'))
                    .pipe(  dest('project/dist/js'));
                    
            });
            
            gulp.task('default', ['concat:js']);
            
    - CLI 에서 gulp를 수행하면, script03이 우선적으로 병합된다.
    
#### 2. javascript minify(uglify)

- 성능 최적화를 위한 작업 중 하나는 자바스크립트 파일을 Minify(Uglify, 난독화)하는 작업이다.

- 자바스크립트 파일에 포함된 주석, 공백 등을 제거하고 변수명 등 짧게 바꾸는 등의 작업을 거쳐 용량을 줄이고, 압축하여 자바스크립트 엔진이 보다 빠르게 자바스크립트 파일을 해석할 수 있도록 도와준다.

        npm install gulp-uglify --save-dev
    
    - 설치가 끝나면 이 플러그인을 사용해서 직접 파일을 다루는 빌드 작업을 해야한다.
    
          //gulp load 
          var gulp = require('gulp');
          
          //gulp의 conacat 패키지 로드
          var concat = require('gulp-concat');
          
          //uglify 플러그인 로드(호출)
          var uglify = require('gulp-uglify');
          
          
          //gulp.task()를 사용해서 gulp-concat 업무 수행을 정의한다.
          gulp.task('concat:js' , function(){
          
            return gulp
                //js 하위 디렉터리 내의 모든 자바스크립트 파일을 가져온다.
                .src(['project/src/js/**/*.js']) 
                
                //상단에서 참조한 concat 모듈을 호출하고, 병합할 파일 파일 네이밍을 정의한다.
                .pipe( concat('combine.js) )
                
                /*
                *======================================
                *파일을 병합한 후, uglify를 수행한다!!!
                *======================================
                */
                
                .pipe( uglify() )
                
                //위에서 수행한 task를 배포지(dist)에 파일을 생성한다.
                pipe( gulp.dest('project/dist/js') );
          
          } );
          
          // $gulp 명령어만 수행하기 위해 'default'로 정의, 의존 모듈 concat:js 정의
          //gulp default 를 수행하기 전에 concat:js 수행할 수 있도록 의존 모듈을 정의
          
          gulp.task('default', ['concat:js']);
          
    - 위 코드를 살펴보면, 자바스크립트 파일들을 병합한 후, 압축할 수 있도록 그 아래에 "pipe"를 연결한 후 내부에 uglify()함수를 적용했다.
    
    - 이렇게 작성하면 목적지(dist)에 파일을 생성하기 전에! 압축 과정을 수행하고, 목적지에 파일을 생성하게 된다.
    
          $ gulp
          
    - 위와 같이 gulp를 수행하면 병합, 압축된 결과를 확인할 수 있다.
    
    - 병합, 압축된 결과물은 주석이 사라지고 전달인자 값이 모두 알파벳 한 글자로 변경되어 있을 것이다.
    
          gulp.task('default', ['concat:js']);
          
            - task를 'default'로 정의한 후 의존 모듈인 concat:js 하나만 정의해 둔 것을 확인할 수 있다.
            - 만약 gulp-concat task 안에 uglify를 작성하지 않고 따로 task를 정의했다면, 아래와 같이 정의해야 한다.
            
          gulp.tafk('default' , ['concat:js' , 'uglify' ]);
          
            - 하지만 gulp-concat task 안에서 같이 사용하고 있다면, 기본 테스트를 정의한 후, 의존 모듈로 concat:js만 정의하면 된다.
            
    - 추가적으로, uglify() 함수가 처리하면서 기본 설정된 옵션 값에 따라 발생한 결과로 변수, 매개변수 등이 알파벳 한 글자로 변경되지 않도록
    하거나 주석을 보존하려면, 기본 옵션이 아닌, 옵션을 설정해 줄 필요가 있다.
    
    - mangle을 false로 설정하면, 알파벳 한 글자로 압축하는 과정을 수행하지 않으며
    
    - preserveCommtents의 옵션 값을 all 또는 some 으로 설정하면, 압축 과정에서 주석이 지워지지 않고 보존(preserve)된다.
    
        - all 값인 경우, 모든 주석이 보존되고, some 값일 때는 느낌표(!)가 붙은 주석만 보존된다. 
    
          var gulp = require('gulp');
          
          var concat = require('gulp-concat'),
              uglify = require('gulp-uglify');
              
          gulp.task('concat:js', function (){
          
            return gulp
            
                .src(['project/src/js/**/*.js'])
                
                .pipe( concat('conbine.js') )
                
                /**
                *==============================+ 
                * uglifiy 옵션값 정의 
                * ==============================+ 
                */
                
                .pipe(uglify ( {
                    mangle : false , // 알파벳 한 글자 압축 과정 설정 
                    
                    preserveComments : 'all' // 'all' , 또는 'some'
                
                }))
          
                .pipe( gulp.dest('project/dist/js') );
          
              });
              
              gulp.task('default', ['concat:js'];
              
#### 3. gulp-rename

- gulp-rename 모듈을 이용하여 병합, 압축한 파일을 먼저 출력한 후 압축 과정을 거쳐 이름을 바꿔서 출력하는 방법에 대해서 알아보자.

- 다시 말해, 압축하지 않은 파일과 압축한 파일 두 가지를 출력하는 것이다.

- 실무에서는 대개 압축된 파일에 min 접미사를 붙여 사용하는데, gulp-rename 모듈을 사용하여 간편하게 파일 이름을 바꿔서 출력할 수 있다.

       npm install gulp-name --save-dev
    
    - 설치가 완료되면, gulpfile.js 파일의 코드를 수정해보자.
    
          //gulp load 
          var gulp = require('gulp');
          
          //gulp 플러그인 호출
          var concat = require('gulp-concat'),
              uglify = require('gulp-uglify');
              rename = require('gulp-name'); // gulp-name 모듈 호출
              
              
          /** 
          * ==============================================================+ *
           파일 병합,압축 그리고 문법 검사까지 수행하는 테스크를 정의히기 때문에 
           * task 의 이름을 concat:js -> combine-js 로 변경(가독성 차원) 
           * ==============================================================+ 
          */
          
          gulp.task('combine-js' , function(){
            return gulp
            
                .src(['project/src/js/**/*.js'])
                
                .pipe(concat('combined.js'))
                
                /**
                * =============================
                * pipe에 파일 병합, 압축한 것을 먼저, 목적지에 생성
                * =============================
                */
                
                .pipe(gulp.dest('project/dist/js'))
                
                .pipe(uglify({|
                    mangle : true, //알파벳 한 글자 압축 과정 설정
                    preserveComments : 'all' // 'all' 또는 'some'
                
                }))
                
                /**
                * ==============================
                * pipe에 concat, uglify 을 수행한 후 rename 을 실행
                * ==============================
                */
                
                .pipe(rename('combined.min.js')) // min 네이밍으로 파일 생성
                .pipe(gulp.dest('project/dist.js') );
                
                });
                
                gulp.task('default', ['combine-js']);
                
    - 첫번째 task 부분의 name을 combile-js 로 변경하였다,
    
    - concat 과 uglify 를 수행하고, rename 까지 수행하는 task이기 때문에 가독성 차원에서 이름은 변경한 것 뿐이다.
    
    - gulp.dest() 호출하는 곳이 두 군데 보일 것이다.
    
        - 이는, 병합을 수행한 파일을 먼저 목적이(dist)에 생성하고, 
        
        - 그 다음 병합 / 압축을 모두 한 파일을 rename 함으로써 'combined.min.js' 네이밍을 정의한 후 목적이(dist)에 또 다시 파일을 생성한 것이다.
        
        - concat() 함수에 병합할 파일 네이밍을 문자열로 전달했듯이 rename() 함수에 변경할 파일 이름을 전달 인자로 작성한 것이다.
        
    - gulp 명령어를 실행하면, 아래처럼 두 개의 파일이 생성 된다.
    
            project/dist/js/combined.js
            project/dist/js/combined.min.js       
          
#### 4. watch

- 지속적인 관찰 업무 등록

- 지금까지는 uglify,concat,rename 플러그인을 이용해서 자바스크립트 파일을 최적화 하는 방법에 대해 살펴보았다.

- 한 두번은 괜찮지만, 개발 과정에서 번번한 수정으로 매번 javascript를 수정할 때마다 CLI에서 gulp task를 수행,실행 하는 것은 매우 비효율 적이고 귀찮을 일이다.

- 이런 불편한 경우를 위해 gulp는 파일에 변경이 있을 때마다 변경을 감지해서 task 를 실행할 수 있는 기능인 gulp.watch라는 메서드를 제공한다.

- 즉, 사용자가 파일만 변경하여 저장하면 자동으로 업무가 실행되기 때문에 지속적인 관찰 업무를 등록하게 되면, 자동으로 번거로운 일들을 처리할 수 있는데 이를 자동화(automation)이라고 한다.
    
      //gulp load
      var gulp = require('gulp');
      
      //gulp 플러그인 호출
      var concat = require('gulp-concat'),
          uqlify = require('gulp-uglify'),
          rename = require('gulp-rename');
          
      gulp.task('combine-js', function(){
        return gulp
        
            .src(['project/src/js/**/*.js'])
            .pipe(concat('combine.js'))
            .pipe(gulp.dest('project/dist/js'))
            .pipe(uglify())
            .pipe(rename('combine.min.js'))
            .pipe(gulp.dest('project/dist/js'));
      
      });
      
      /**
      * =======================================
      * 지속적인 업무 관찰을 위해 watch 등록
      * 즉, 파일 변경을 감지한다.
      * =======================================
      */
      
      gulp.task('watch', function(){
      
        /**
        * =====================================
        * 1. 감지할 디렉터리를 정의
        * 2. 변경이 감지되면 실행할 task를 지정
        * =====================================
        */
        
      gulp.watch('project/src/js/**/*.js', ['combine-js']);
        
      });
      
      // gulp 를 실행하면 default 로 combine-js task 와 watch task 를 실행하도록 한다. 
      
      gulp.task('default', ['combine-js','watch']);
      
- 이 task의 gulp.watch 메서드에는 두 개 의 전달인자 값을 전달받고 있다.

- gulp.watch('project/src/js/**/*.js', ['combine-js']);

    - gulp.watch의 첫번째 파라미터에서는 변경 감지를 해야하는 대상을 지정한다.
    
    - 두번째 파라미터는 변경이 감지되었을 때, 실행할 task를 지정하도록 한다. 
    
        - 배열 형태로, 여러개의 task 명을 넣어주면, 변경이 일어날 때마다 해당 task들을 자동으로 실행해주게 된다.
        
    - 위 코드의 watch를 분석해보면 'project/src/js/'디렉터리 내에 js 확장자를 가진 파일이 변경되면, combine-js task를 실행한다는 의미이다!
    
- gulp.task('default' , ['combine-js' , 'watch']);

    - 위와 같이 default task 로 combine-js 와 watch task 를 지정했기 때문에 아래와 같이 gulp 라고만 입력하면 combine-js 와 watch task 가 실행되게 된다.
    
    - watch task 를 샐행했기 때문에, gulp가 바로 종료되지 않고 변경 감지를 위해 대기하고 있는 것을 확인할 수 있다.
    
    - 이 때 project/src/js 디렉터리 아래의 js 파일 하나를 수정하면 바로 변경을 감지해서 combine-js 를 수행하는 것을 확인할 수 있다.
    
### D. gulp-sass / gulp-sourcemaps
          
#### 1. gulp-sass

- npm install gulp-sass gulp-sourcemaps --save -dev 
    
      //gulp load
      var gulp = require('gulp');
      
      //gulp 플러그인 호출
      var concat = require('gulp-concat'),
          uqlify = require('gulp-uglify'),
          rename = require('gulp-rename');
          sourcemaps = require('gulp-sourcemaps'), //sourcemaps 호출
          scss = require('gulp-sass'); //sass 호출
          
            
      /**
      * ==================================
      //경로들을 담을 객체 생성
      * ==================================
      */
          
      var src = 'project/src';
      var dist = 'project/dist';
      var paths = {
            js : src + 'js/**/*.js',
            scss : src + 'sass/**/*.scss'      
      };
      
      /**
      * ==================================
      //@task : script 병합, 압축 min 파일 생성
      * ==================================
      */
      
      gulp.task('js:combine', function(){
      
        return gulp
        
            .src(paths.js)
            .pipe(concat('combine.js'))
            .pipe(gulp.dest(dist+'/js'))
            .pipe(uglify())
            .pipe(rename('combined.min.js'))
            .pipe(gulp.dest(dist+'/js'))
      });
      
      
      /**
      * ==================================
      //SCSS : SCSS Config(환경설정)
      * ==================================
      */
      
      var scssOptions = {
      
        /**
        * outputStyle = (Type : string, Default : nested)
        * CSS의 컴파일의 결과 코드 스타일 지정
        * values : nested, expanded, compact, compressed
        * nested : 뎁스별로 구분해서 컴파일 
        * expanded : 요소의 모든 스타일을 한줄에 컴파일
        * compact : 요소에 스타일이 속성을 한줄씰 정렬해서 컴파일
        * compressed : 공백없이 컴파
        */
        outputStyle : "expanded",
        
        /**
        * indentType (>= v3.0.0 , type : string, default : space)
        * 컴파일 된 CSS "들여쓰기" 의 타입
            * values : space, tab
        */
        indentType : "tab",
        
        /**
        * indentWidth (>= v3.0.0, type : integer, default : 2)
        * 컴파일 된 CSS의 "들여쓰기" 의 갯수
        */
        indentWidth : 1,
        //outputStyle이 nested, expanded 인 경우에 사용
        
        /**
        * precision (typr : integer , defaulp : 5)
        * 컴파일 된 CSS의 소수점 자릿 수
        */
        precision : 6,
        
        /**
        * sourceComments (type : boolean, default : false)
        * 컴파일 된 CSS에 원본 소스의 위치와 줄 수 주석 표시
        */
        
        sourceComments : true
        
      };
      
            
      /**
      * ==================================
      //@task : SCSS Compile $ sourcemaps
      * ==================================
      */
      
      gulp.task('scss:compile', function(){
      
        return gulp 
            
            //SCSS 파일을 읽어온다.
            .src(paths.scss)
            
            //소스맵 초기화 (소스맵을 생성)
            //소스맵 ? 코드상의 위치를 알려주즌 것 
            .pipe(sourcemaps.init())
            
            //SCSS 함수에 옵션 값을 설정, SCSS 작성 시 watch가 멈추지 않도록 logError를 설정
            //on 메서드에서 CLI에서 SCSS문법을 작성시 발생할 수 있는 문법 에러를 잡아주도록 작성
            .pipe(scss(scssOptions).on('error',scss.logEorror))
            
            //위에서 생성한 소스맵을 사용한다.
            .pipe(sourcemaps.write())
            
            //목적지를 설정
            .pipe(gulp.dest(dist+'/css')      
      
      });
      
      gulp.task('watch', function(){
        
        gulp.watch(paths.js, ['js:combine']);
        gulp.watch(paths.scss, ['scss:compile']);
      });
      
      //gulp를 실행하면 default로 'js:combine', 'scss:compile', 'watch'를 실행한다.
      gulp.task('default', ['js:combine', 'scss:compile', 'watch'])
      
        - 소스맵(sourcemaps)은 쉽게 말해 코드상의 위치를 알려주는 것을 말합니다.
          
          예를 들어 SCSS를 사용한다고 가정한다면 컴파일된 CSS 로 HTML과 link 를 시키게 됩니다. 
          
          이 경우에 크롬 개발자도구와 같은 것을 이용하여 CSS 의 값을 확인하거나 디버깅할 시 이슈가 있는 CSS 의 위치를 알 수 있겠지만 원본은 SCSS 이기 때문에 CSS의 위치를 알더라도 SCSS 를 수정해야 하는 입장에서 CSS 위치는 불필요합니다.
          
          이러한 경우 sourcemaps 를 설정하게 되면 SCSS 파일의 위치를 알려주기 때문에 유용하게 사용할 수 있습니다.
  

  
### E. gulp-liveReload

- 일반적으로 로컬에서 프론트엔드 작업을 할 때 어떤 형태로든 웹서버를 띄어서 결과물을 확인한다.

- 파일을 수정할 때마다 정적 리소스들을 빌드해둔 후에 띄어놓은 웹서버에 접속해서 리프레시를 해서 결과물을 확인하는 것이 일반적인 작업 패턴일 것이다.

- liveReload는 파일 변경(Sass, css, js, html 등) 시에 이를 자동으로 감지해서 브라우저 refresh를 자동으로 수행할 수 있다록 도와주는 도구이다.

- gulp-liceReload 플러그인 설치하기
  
      npm install gulp-liveReload --save-dev
    
- 위 소스들과 이어 작업하기.

        var gulp = require('gulp'),
            concat = require('gulp-concat'),
            uglify = require('gulp-uglify'),
            rename = require('gulp-rename'),
            sourcemaps = require('gulp-sourcemaps'),
            scss = require('gulp-scss'),
            livereload = require('gulp-livereload');
            
        
        var src = 'project/src',
            dist = 'project/dist',
            paths = {
                js : src + '/js/**/*.js',
                scss : src + '/sass/**/*.scss'            
            };
            
            
            
        /** 
        * =====================================+ 
        * @task : HTML livereload 반영 
        * =====================================+ 
        */
        
            
        gulp.task('html',function(){
            return gulp
                /**
                * 
                * html 파일을 읽어오기 위해 경로를 지정
                */
                .src('./**/*.html')
                
                /**
                *
                * html 파일을 읽어온 후 livereload 호출하여 브라우저에 반영
                */
                
                .pipe(livereload());
        
         });
         
         
         /** 
         * =====================================+ 
         * @task : script 병합, 압축, min 파일 생성 
         * =====================================+ 
         */
         
         gulp.task('js:combine', function(){
            return gulp
            
                .src(paths.js)
                .pipe(concat('combined.js'))
                .pipe(gulp.dest(dist + '/js'))
                .pipe(ugify())
                .pipe(rename('combined.min.js'))
                .pipe(gulp.dest(dist+ '/js'))
                
                /**
                * 스크립트 task를 모두 수행한 후 livereload 호출하여 브라우저에 반영
                */
                
                .pipe(liverload());
                
         })
         
         
         /** 
         * =====================================+ 
         * @SCSS : SCSS Config(환경설정)  
         * =====================================+ 
         */
         
         
         var scssOptions = {
            outputStyle : "expanded",
            indentType : 'tab',
            indentWidth : 1,
            procision : 6,
            sourceComments : false
         }
         
         
         /** 
         * =====================================+ 
         * @task : SCSS Compile & sourcemaps 
         * =====================================+ 
         */
         
         gulp.task('scss:compile', function(){
            return gulp
            
                .src(paths.scss)
                .pipe(sourcemaps.init())
                .pipe(scss(scssOptions).on('error'), scss.logError))
                .pipe(surcemaps.write())
                .pipe(gulp.dest(dist+'/css))
                
                /**
                * SCSS 컴파일을 모두 수행한 후 livereload 호출하여 브라우저에 반영
                */
                
                .pipe(liverload());
                
         })
         
         
         
         /** 
         * =====================================+ 
         * @task : livereload 실행 
         * =====================================+ 
         */
         
         
         gulp.task('live', ['html', 'js:combine' , 'scss:compile'], function(){
         
                /**
                * livereload.listen() 옵션값으로 기본 경로를 지정
                */
                
                livereload.listen(
                    {basePath : dist}
                );
         });
         
      gulp.task('watch', function(){
        
        gulp.watch('./**/*.html`, ['html']) // html task를 watch에 등록
        gulp.watch(paths.js, ['js:combine']);
        gulp.watch(paths.scss, ['scss:compile']);
      });
      
      gulp.task('default', ['live' , 'watch'])
      
         
         
         
         
         
        
         
         
         
                 
                 
         
         
            


     
  
  
#### 사용한 블로그

- https://webclub.tistory.com/470?category=574769 [Web Club]
      
     
      
    
          
          
          
              