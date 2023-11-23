# Responsive_Website
- 여행 사이트 메인페이지 반응형 웹사이트 
- HTML, CSS, JavaScript, jQuery 를 사용하여 스크롤시 애니메이션,
  디자인이 변경되는 헤더와 이미지 애니메이션, 글자별 텍스트 애니메이션,
  GNB 오픈메뉴 구현 반응형 웹사이트 입니다. 
***
## 구현 화면
![반응형_커버](https://github.com/lcl3392/Responsive_Website/assets/133613544/91b9ee69-9e66-4d48-baee-dbd989e19498)
***
## code 설명 

- 문서가 로드될 때부터 href 속성이 "#"인 모든 앵커의 클릭 동작을 막아서 해당 앵커들이 페이지 내에서의 이동을 방지합니다.
 + $(document).on('click', 'a[href="#"]', function(e) {...}): 문서 객체 모델(DOM)이 로드되면서, 모든 <a> 요소 중에서 href 속성 값이 "#"인 것들에 대한 클릭 이벤트 핸들러를 등록합니다.
 + function(e) {...}: 클릭 이벤트가 발생했을 때 실행되는 함수를 정의합니다. e는 이벤트 객체를 나타냅니다.
 + e.preventDefault();: 클릭 이벤트에서 e.preventDefault()를 호출하여 브라우저가 해당 앵커의 기본 동작을 수행하지 않도록 막습니다. 여기서는 앵커가 클릭되었을 때 브라우저가 해당 앵커의 "#"로 이동하는 동작을 막습니다.
 ```
$(document).on('click','a[href="#"]',function(e){
    e.preventDefault();
})
```
***

-  페이지를 스크롤하거나 창의 크기를 조절할 때 발생하는 이벤트에 따라 여러 가지 효과를 적용하는 역할을 합니다.
  + $(window).on('scroll resize', function() {...}): 윈도우 객체에 스크롤 또는 리사이즈 이벤트가 발생하면 실행될 함수를 등록합니다.
  + var scrollPos = 0;: 스크롤 위치를 저장할 변수 scrollPos를 초기화합니다.
  + scrollPos = $(document).scrollTop();: 현재 스크롤 위치를 scrollTop() 메서드를 사용하여 가져와서 scrollPos에 저장합니다.
  + fix();, fixHeader();, fixList();: 각각 fix(), fixHeader(), fixList() 함수를 호출합니다.
  + function fix() {...}: 스크롤 위치에 따라 .fix .text 요소에 on 클래스를 추가 또는 제거하여 효과를 줍니다.
  + function fixHeader() {...}: 스크롤 위치에 따라 header 요소에 on 클래스를 추가 또는 제거하여 효과를 줍니다.
  + function fixList() {...}: 스크롤 위치에 따라 section.approach .inner .list li a 요소 중에서 특정 위치에 해당하는 것에 on 클래스를 추가하고, 다른 위치에 해당하는 것에는 on 클래스를 제거하여 리스트에 효과를 줍니다.
  ```
  $(window).on('scroll resize', function(){
    var scrollPos = 0;
    scrollPos = $(document).scrollTop();
    fix();
    fixHeader();
    fixList();

    function fix(){
        if(scrollPos > 1250) {$('.fix .text').addClass('on');}
        else {$('.fix .text').removeClass('on');}
        if(scrollPos > 2700) {$('.fix .text').removeClass('on');}
    }

    function fixHeader(){
        if(scrollPos > 80){$('header').addClass('on');}
        else {$('header').removeClass('on');}
    }

    function fixList() {
        $('section.approach .inner .list li a').removeClass('on');
        if(scrollPos > 1250){
            $('section.approach .inner .list li a').removeClass('on');
            $('section.approach .inner .list li:eq(0) a').addClass('on');
            // eq() : 인덱스 값을 사용해 원하는 위치의 요소를 선택해 가져올 수 있는 선택자 메소드
        }
        if(scrollPos > 1650){
            $('section.approach .inner .list li a').removeClass('on');
            $('section.approach .inner .list li:eq(1) a').addClass('on');
        }
        if(scrollPos > 2050){
            $('section.approach .inner .list li a').removeClass('on');
            $('section.approach .inner .list li:eq(2) a').addClass('on');
        }
        if(scrollPos > 2550){
            $('section.approach .inner .list li a').removeClass('on');
            $('section.approach .inner .list li:eq(3) a').addClass('on');
        }
        if(scrollPos > 2900){
            $('section.approach .inner .list li a').removeClass('on');
        }
    }
});
  ```

***  
-  jQuery를 사용하여 화면에 나타나는 요소에 스크롤 애니메이션 효과를 부여하는 역할을 합니다.
  + $(function() {...}): HTML 문서가 완전히 로드되면 실행될 함수를 정의합니다. 이는 jQuery에서 문서가 준비되었을 때 코드를 실행하는 관례적인 방법입니다.
  + $('.animate').scrolla({...}): 클래스가 "animate"로 지정된 요소들을 대상으로 scrolla 플러그인을 적용합니다. Scrolla는 스크롤 애니메이션을 제공하는 jQuery 플러그인 중 하나입니다.
  + mobile: true, once: false: scrolla 플러그인에 옵션을 설정합니다. 여기서는 mobile을 true로 설정하여 모바일에서도 애니메이션이 동작하도록 하고, once를 false로 설정하여 애니메이션이 한 번만 실행되지 않도록 합니다.
  ```
 $(function(){
    $('.animate').scrolla({
        mobile: true,
        once:false
    })
})

  ```

***  
- 이 코드는 페이지가 로드될 때 Splitting.js를 초기화하여 텍스트를 분할하고, 분할된 각 부분에 대한 스타일을 적용할 수 있도록 하는 것입니다. 
  + $(function(){...});: HTML 문서가 완전히 로드되면 실행될 함수를 정의합니다. 이는 jQuery에서 문서가 준비되었을 때 코드를 실행하는 관례적인 방법입니다.
  + Splitting();: Splitting.js 라이브러리의 초기화 함수를 호출합니다. Splitting.js는 텍스트를 문자 또는 단어로 분할(splitting)하여 각 문자 또는 단어에 대한 스타일링이 가능하도록 해주는 라이브러리입니다.
  ```
  $(function(){Splitting();});
  ```

***
- 네비게이션 메뉴를 열고 닫는 동작에 대한 jQuery 이벤트 핸들러를 정의합니다.
  + $(function(){...});: HTML 문서가 로드되면 실행될 함수를 정의합니다. 이것은 jQuery에서 문서가 준비되었을 때 코드를 실행하는 관례적인 방법입니다.
  + $('header .gnbBtn').on('click', function(){...});: 페이지 상단의 헤더(header)에서 클래스가 'gnbBtn'인 요소가 클릭되었을 때 실행될 함수를 정의합니다. 해당 함수는 헤더 내비게이션(nav.gnb)에 'on' 클래스를 토글(toggle)합니다.
  + $('.contents').on('click', function(){...});: 클래스가 'contents'인 요소가 클릭되었을 때 실행될 함수를 정의합니다. 해당 함수는 헤더 내비게이션(nav.gnb)에서 'on' 클래스를 제거합니다.
  + $('nav.gnb .gnbBtn_shut span').on('click', function(){...});: 내비게이션(nav.gnb) 내부에서 클래스가 'gnbBtn_shut'인 하위 요소인 span이 클릭되었을 때 실행될 함수를 정의합니다. 해당 함수는 헤더 내비게이션(nav.gnb)에 'on' 클래스를 토글합니다.
  ```
  $(function(){
    $('header .gnbBtn').on('click', function(){
        $('header nav.gnb').toggleClass('on');
    });
    $('.contents').on('click', function(){
        $('header nav.gnb').removeClass('on');
    });
    $('nav.gnb .gnbBtn_shut span').on('click', function(){
        $('header nav.gnb').toggleClass('on');
      });
  });
  ``` 

