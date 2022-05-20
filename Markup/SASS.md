### SASS

<img src='https://velog.velcdn.com/images/topgeun7913/post/9f631311-f104-42b1-a5ba-dacd6b7a90c2/sass.png' alt='' />

    최근 리액트에서 많은양은 아니지만 컴포넌트들을 마크업할때 반복작업과 마크업을 하면서 소요되는 시간이 너무 크다는 생각이 들었다.
    React를 하면서 CSS module도 정말 놀라운 기술이지만 CSS 전처리기를 경험하고 싶었다. 요즘은 CSS-in-js를 통해 컵포넌트를 재사용하거나 CSS파일을 따로 관리하지 않는등의 장점으로 인해 사용하는 듯 하다.
    하지만 가독성과 마크업 파일의 역할에 대해서 생각한 결과 주관적으로는 css 전처리기를 제일 먼저 적용해보고 싶었다.

    css 전처리기의 정의를 살펴보면 **CSS 전처리기는 전처리기의 자신만의 특별한 syntax를 가지고 CSS를 생성하도록 하는 프로그램입니다.** 라고 되어있는데 sass의 경우는 어떤지 살펴보자!

<hr/>

    * 리액트에서 설치하기

<code>
    npm i --save sass 
</code>

    프로젝트에 sass를 설치하는 명령어이다.
    package.json에 들어가서 dependencies에 sass가 있는지 확인해보기!!📌
