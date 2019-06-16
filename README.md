# FABLAB 2019 메이커아카데미  Project

![FABLAB Screenshot](/assets/images/FABLAB_Logo.png)


## Blog 관련하여...

2019 메이커아카데미의 프로젝트 진행 내용을 정리하는 블로그 입니다.

Github 에서 제공하는 [Jekyll](https://jekyllrb-ko.github.io/) 툴을 사용하여 만들어 졌으며,

호스팅 되는 blog 주소는 [https://hyuni.github.io/FABLAB/](https://hyuni.github.io/FABLAB/) 입니다.



## Jekyll 사용법

### 이미지 사용 관련 Tips

 1. assets/images 폴더를 생성하고 이미지를 업로드


 2. html 문법
 
   - 절대경로(Absoulte URL)
   
 	```html
 	<img data-action="zoom" src='{{ "/assets/images/image.png" | relative_url }}' alt='absolute'>
<!-- result : http://blog.jaeyoon.io/my-baseurl/assets/images/image.png -->
 	```
 	
 	
 	- 상대경로(Releative URL)
 	
 	```html
 	<img data-action="zoom" src='{{ "/assets/images/image.png" | relative_url }}' alt='relative'>
<!-- result : /my-baseurl/assets/images/image.png -->
 	```

 	
 3. 마크다운(Markdown) 문법

    ```kramdown
    ![Image Alt 텍스트]({{site.url}}/assets/images/image.png)
    ![Image Alt 텍스트](http://blog.jaeyoon.io/assets/images/image.png)
    ![Image Alt 텍스트]({{"/assets/images/image.png"| relative_url}})
    ![Image Alt 텍스트](/assets/images/image.png)
    ```
 
  

## Markdown

### Markdown 사용 관련 Tips

 1. 마크다운 문서에 유튜브 링크 추가하기

 	아래와 같이 사용
    ```
    [![이미지 텍스트](스크린샷 이미지)](유투브링크)
    ```
    
    예를 들어 아래와 같은 경우
    ```
    [![Video Label](http://img.youtube.com/vi/uLR1RNqJ1Mw/0.jpg)](https://youtu.be/uLR1RNqJ1Mw?t=0s)
    ```
    
    이렇게 표시됨.
    
    [![Video Label](http://img.youtube.com/vi/uLR1RNqJ1Mw/0.jpg)](https://youtu.be/uLR1RNqJ1Mw?t=0s)