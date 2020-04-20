## SASS(SCSS)

- 기본 요약

    - 탭 대신 스페이스 두(2) 칸을 들여쓴다;
    - 행의 너비는 80 글자;
    - CSS를 여러 행으로 적절히 작성한다;
    - 공백을 의미 있게 사용한다;
    - 문자열과 URL에는 인용 부호(작은 따옴표)를 붙인다;
    - 뒤따르는 0은 표기하지 않는다. 앞장서는 0은 반드시 표기한다;
    - 연산은 괄호로 감싼다;
    - 매직 넘버를 피한다;
    - 색은 키워드 > HSL > RGB > 16진법 순으로 표기한다;
    - 리스트는 쉼표로 구분한다;
    - 리스트에는 뒤따르는 쉼표를 붙이지 않는다(한 줄로 표기하므로);
    - 맵에는 뒤따르는 쉼표를 붙인다;
    - 가상 클래스와 가상 요소 외에는 선택자를 내포하지 않는다;
    - 작명 시 하이픈으로 구분한다;
    - 많은 주석을 붙인다;
    - SassDoc을 이용하여 API 주석을 표기한다;
    - @extend는 제한적으로 사용한다;
    - 간단한 믹스인을 사용한다;
    - 반복문은 최소한으로 사용하고, @while은 사용하지 않는다;
    - 의존성의 수를 줄인다;
    - 경고와 오류를 의미 있게 사용한다.

### 설치

* MAC

1. terminal 에서 "sudo gem install sass"로 전역에 sass를 설치한다.

2. sass -v 으로 사스 설치 유무와 버전 확인

3. SCSS를 사용할 폴더를 만들고 terminal에서 command + 해당 파일을 드래그 시켜, 위치를 그 곳으로 이동시킨다.

4. 해당 위치에 sass --watch .:. 입력 

5. 들어가면 sass-cache폴더가 생성되고, 자동으로 컴파일이 되기 시작한다.

6. 하나의 scss 파일로 만들어 주고 싶으면, 

        ex)
        - _main.scss
        - _common.scss
        - _header.scss
        
        로 나누어진 scss 파일로 작업을 하고,
        
        - style.scss 을 만들면 자동으로 style.css 와 style.map 이 생성된다.
        - @import "common"
        - @import "header"
        - @import "main"
        - 을 해서 모든 scss 파일을 style에 넣어주면 된다.
        
7. style 출력 하는 방식

        - sass --watch style.scss:style.css --style compressed
        - sass --watch .:. --style compressed



* WINDOW

1.	File – settings – tools – file watchers 추가
 
2.	안잡히면 직접 경로 잡아서 설치하기!! 

### 패턴

- 7개의 다른 폴더에 채워넣은 모든 부분 파일과, 이를 불러들여 CSS 스타일로 컴파일 하는 루트 레벨에 있는 하나의 파일(main.scss)을 갖게된다

      sass/
      | // 리셋파일, 타이포그래픽 규칙, 자주 사용되는 HTML 요소에 대한 표준 스타일을 정의하는 스타일 시트 등.
      |– base/
      |   |– _reset.scss       # Reset/normalize
      |   |– _base.scss        # 표준 스타일
      |   |– _typography.scss  # 타이포그래피 규칙
      |   …                    # 기타.
      | // 더 작은 컴퍼넌트들, layout이 전반적인 뼈대를 정의하는 폴더임에 반해, 위젯에 초점을 둔다.
      |– components/
      |   |– _buttons.scss     # 버튼
      |   |– _carousel.scss    # 캐러셀
      |   |– _cover.scss       # 커버
      |   |– _dropdown.scss    # 드롭다운
      |   …                    # 기타.
      | // 사이트나 어플리케이션의 레이아웃에 기여하는 모든 것들 
      |– layout/
      |   |– _navigation.scss  # 네비게이션
      |   |– _grid.scss        # 그리드 시스템
      |   |– _header.scss      # 헤더
      |   |– _footer.scss      # 푸터
      |   |– _sidebar.scss     # 사이드바
      |   |– _forms.scss       # 폼
      |   …                    # 기타.
      | // 페이지에 한정된 스타일이 있다면, 이 폴더 속에, 페이지의 이름을 딴 파일에 넣는 것이 좋다.
      |– pages/
      |   |– _home.scss        # 홈 한정 스타일
      |   |– _contact.scss     # 연락처 한정 스타일
      |   …                    # 기타.
      | // 큰 사이트와 어플리케이션에서 여러 다른 테마들을 갖는 경우 이곳에 넣어 관리한다.
      |– themes/
      |   |– _theme.scss       # 디폴트 테마
      |   |– _admin.scss       # 관리자 테마
      |   …                    # 기타.
      | // 프로젝트에서 사용되는 모든 sass 도구와 헬퍼를 담는 폴더, 한 줄의 CSS도 산출하지 않아야 한다.  
      |– utils/ (or helpers)
      |   |– _variables.scss   # Sass 변수
      |   |– _functions.scss   # Sass 함수
      |   |– _mixins.scss      # Sass 믹스인
      |   |– _helpers.scss     # 클래스 & 플레이스홀더 헬퍼
      | // 외부 라이브러리와 프레임워크에서 나오는 모든 CSS 파일을 담고 있는 폴더
      |– vendors/
      |   |– _bootstrap.scss   # Bootstrap
      |   |– _jquery-ui.scss   # jQuery UI
      |   …                    # 기타.
      |
      | // 전체 코드베이스에서 언더스코어로 시작하지 않는 유일한 Sass 파일이어야 한다. @import와 주석 외에는 아무것도 포함하지 않아야 한다.
      `– main.scss             # 메인 Sass 파일
      
        - @import 'abstracts/variables';
          @import 'abstracts/functions';
          @import 'abstracts/mixins';
          @import 'abstracts/placeholders';
          
          @import 'vendors/bootstrap';
          @import 'vendors/jquery-ui';
          
          @import 'base/reset';
          @import 'base/typography';
          
          @import 'layout/navigation';
          @import 'layout/grid';
          @import 'layout/header';
          @import 'layout/footer';
          @import 'layout/sidebar';
          @import 'layout/forms';
          
          @import 'components/buttons';
          @import 'components/carousel';
          @import 'components/cover';
          @import 'components/dropdown';
          
          @import 'pages/home';
          @import 'pages/contact';
          
          @import 'themes/theme';
          @import 'themes/admin';


## MIXIN

### Break Point (반응형 디자인)

- 다양한 디바이스 기준으로 대응을 해야하기 때문에, 브레이크 포인트의 이름은 보편적으로 지어야 한다.

        // Break Point (Desktop First 기준 내림차순 설정)
        
        $desktop-l-width	: 1440px;
        $tablet-l-width		: 1024px;
        $tablet-s-width		: 768px;
        $mob-l-width		: 640px;
        $mob-m-width		: 425px;
        $mob-s-width		: 375px;
         
        // only PC
        @mixin pc-only {
            @media screen and (min-width: #{$tablet-l-width + 1}) {
                @content;
            }
        }
        // PC large
        @mixin pc-large {
            @media screen and (min-width: #{$desktop-l-width + 1}) {
                @content;
            }
        }
        
        // 태블릿
        @mixin tab {
            @media screen and (max-width: #{$tablet-l-width}) {
                @content;
            }
        }
        // 모바일
        @mixin mob {
            @media screen and (max-width: #{$tablet-s-width}) {
                @content;
            }
        }
        // 모바일 large
        @mixin mob-large {
            @media screen and (max-width: #{$mob-l-width}) {
                @content;
            }
        }
        // 모바일 mid
        @mixin mob-mid {
            @media screen and (max-width: #{$mob-m-width}) {
                @content;
            }
        }
        // 모바일 small
        @mixin mob-small {
            @media screen and (max-width: #{$mob-s-width}) {
                @content;
            }
        }
 
- SCSS에 적용하고, CSS에 compile 된 경우,

        // scss
         
        @include pc-only{
            body{
                padding:0 15px;
            }
        }
         
        //  css compiled 되면 아래와 같다!
         
        @media screen and (min-width: 1025px) { body { padding: 0 15px; } }
      
### MIXIN의 다양한 예

- 말줄임을 표현하는 스타일, 버튼 스타일, clearfix 등 만들어 놓고 필요한 위치에 클래스를 추가로 넣어주는 경우가 있는데, mixin을 이용하면 더 쉽게 반복적인 작업을 할 수 있다.

- @mixin 지시자를 사용하며, 적용할 때는 @include 지시자를 사용한다.

        @mixin mixin명 {
        
            //작업할 것들
            
        }
        
        SCSS 적용
        
        @include mixin명 또는 @include mixin(전달할인자)
        
- 예시
        
        * mixin 설정
        
        @mixin ellpise-one($wid:100%){ 
        //$wid를 인자로 받는데, 넘겨주는 값이 없을 경우, 기본 값을 100%로 전달한다는 것이다. 즉 100% = default값 이다. 기본값은 : 콜론 으로 정의한다.
        
            width : $wid;
            overflow:hidden;
            text-overflow:ellipsis;
            white-space:nowrap;
            
        }
        
        * scss
        
        .text{
            @includ ellipse-one(80%);
            
        }
        
        * css
        
        .text { width: 80%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

- 예시 2

        * mixin 설정
        
        @mixin media( $queryPoint ) {        
            
            //여기서 #{}은 특정 문자열을 따로 처리하지 않고, 그대로 출력할 때 사용한다. 
            @media #{ $queryPoint } {            
                @content                
                //content 지시자를 사용하면 @include 했을 때, 해당 선택자 내부의 내용들이 @content 부분에 나타나게 된다.
            }        
        }
        
        * scss
        
        .new-list{
            width : 100%;
            @includ media("(max-width:480px)"){
                width : 50%;
            }
        }
                
        * css

        .news-list { width: 100%; }
        @media (max-width: 480px) { .news-list { width: 50%; }        
        
- 예시 3

        * mixin
        /// 내부 float을 해제하는 헬퍼
        /// @author Nicolas Gallagher
        /// @link http://nicolasgallagher.com/micro-clearfix-hack/ Micro Clearfix
        
        @mixin clearfix {
          &::after {
            content: '';
            display: table;
            clear: both;
          }
        }          
        
- 예시 4

        * mixin
        @mixin border-radius($radius) {
          -webkit-border-radius: $radius;
             -moz-border-radius: $radius;
              -ms-border-radius: $radius;
                  border-radius: $radius;
        }
        
        * scss
        .box { @include border-radius(10px); }  

- 예시 5

        * mixin
        @mixin input-placeholder {
            &.placeholder { @content; }
            &:-moz-placeholder { @content; }
            &::-moz-placeholder { @content; }
            &:-ms-input-placeholder { @content; }
            &::-webkit-input-placeholder { @content; }
        }
        
        * scss
        input,  
        textarea {  
            @include input-placeholder {
                color: $grey;
            }
        }
        
        
        
### EXTEND

- scss에서 특정 선택자를 상속할 때, @extend 지시자를 사용한다.

        @extend .클래스명;
        
        @extend %클래스명;
        
- 예시
        
        * scss
        .box{
            padding:10px;
            border : 1px solid #fff;
        }
        
        .news-box {
            @extend .box;
            background-color : #08c;
        }
        
        .list-box{
            @extend .box;
            background-color : red;
        }
          
        * css  
        .box, .news-box, .list-box { padding: 20px; border: 1px solid #333; }
        .news-box { background-color: #eee; }
        .list-box { background-color: #000; }
        
- placeholder selector

    - extend를 사용할 때 id나 class 선택자처럼 %로 선택자를 만들 수 있다.
    
    - placeholder 선택자 %를 사용하면 상속은 할 수 있지만, 해당 선택자는 컴파일 되지 않는다.
    
    - 투명 선택자라고 보면 된다.
    
          * scss
          
          %box{
              padding:10px;
              border : 1px solid #fff;
          }
          
          .news-box {
              @extend %box;
              background-color : #08c;
          }
          
          .list-box{
              @extend %box;
              background-color : red;
          }
          
          * css
          
          .news-box, .list-box { padding: 20px; border: 1px solid #333; }
          .news-box { background-color: #eee; }
          .list-box { background-color: #000; }
    
### 중첩

- 상위 선택자 참조 

    & 키워드는 상위(부모) 선택자를 참조하여 치환한다.
    
    - 예시
    
          * scss
          .fs {
            &-small { font-size : 12px ; }
            &-medium { font-size : 14px ; }
            &-large { font-size : 16px ; }
          }
          
          * css
          .fs-small {
            font-size: 12px;
          }
          .fs-medium {
            font-size: 14px;
          }
          .fs-large {
            font-size: 16px;
          }
          
- 중첩 벗어나기

    - @at-root 
    
           * scss
           .list {
             $w: 100px;
             $h: 50px;
             li {
               width: $w;
               height: $h;
             }
             @at-root .box {
               width: $w;
               height: $h;
             }
           }
           
           * css
           .list li {
             width: 100px;
             height: 50px;
           }
           .box {
             width: 100px;
             height: 50px;
           }
           
- 중첩된 속성

    - font-, margin- 등과 같이, 동일한 네임 스페이스를 가지는 속성들을 다음과 같이 사용할 수 있다.
    
          * scss
          .box{
            font : {
            weight : bold;
            size: 10px;
            family : sans-serif;
            }
            margin : {
            top : 10px;
            bottom : 10px;
            }
            padding : {
            bottom : 10px;
            right : 20px;
            };
          }
          
          * css
          .box{
          font-weight:bold;
          font-size:10px;
          font-family:sans-serif;
          margin-top:10px;
          margin-bottom:10px;
          padding-bottom:10px;
          padding-right:20px;
          }
    
### 변수

-반복적으로 사용되는 값을 변수로 지정할 수 있다.

- 변수는 선언된 블록( { } ) 내에서만 유효범위를 가진다.

- $변수이름 : 속성값;

      * scss 
      $color-primary : #08c;
      $url-images : "assets/image/";
      $w : 200px;
      
      .box{
        width : $w;
        margin-left : $w;
        background : $color-primary url($url-images + "bg.jpg");
        }
        
      * css
      .box {
        width: 200px;
        margin-left: 200px;
        background: #e96900 url("/assets/images/bg.jpg");
      }
      

- !gobal 

    - 전역 설정 : 변수의 유효범위를 전역(global)로 설정할 수 있다.
    
          * scss
          $color: #000;
          .box1 {
            $color: #111 !global;
            background: $color;
          }
          .box2 {
            background: $color;
          }
          .box3 {
            $color: #222;
            background: $color;
          }
          
          * css
          .box1 {
            background: #111;
          }
          .box2 {
            background: #111;
          }
          .box3 {
            background: #222;
          }
    
- !default

    - 초깃값 설정 : 할당되지 않은 변수의 초깃값을 설정한다.
    
    - 즉, 할당 되어있는 변수가 있다면 변수가 기존 할당 값을 사용한다.
     
          * scss
          $color-primary: red;
          
          .box {
            $color-primary: blue !default;
            background: $color-primary;
          }
          
          * css
          .box {
            background: red;
          }
           

### 도움받은 블로그

- https://m.blog.naver.com/PostView.nhn?blogId=hwangmari&logNo=220938011725&proxyReferer=https%3A%2F%2Fwww.google.com%2F

- https://publisherkjh.tistory.com/105

- http://frontend.diffthink.kr/2016/09/scss.html?m=1

- https://m.blog.naver.com/PostView.nhn?blogId=hwangmari&logNo=220938011725&proxyReferer=https%3A%2F%2Fwww.google.com%2F

- https://designmeme.github.io/ko/blog/sass-css-output-style/

- https://webclub.tistory.com/57