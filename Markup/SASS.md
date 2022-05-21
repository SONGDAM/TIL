## SASS

<img src='https://velog.velcdn.com/images/topgeun7913/post/9f631311-f104-42b1-a5ba-dacd6b7a90c2/sass.png' width='60%' height='40%' />
<hr/>

<br/>
<br/>
    최근 리액트에서 많은양은 아니지만 컴포넌트들을 마크업할때 반복작업과 마크업을 하면서 소요되는 시간이 너무 크다는 생각이 들었다.
    React를 하면서 CSS module도 정말 놀라운 기술이지만 CSS 전처리기를 경험하고 싶었다. 요즘은 CSS-in-js를 통해 컵포넌트를 재사용하거나 CSS파일을 따로 관리하지 않는등의 장점으로 인해 사용하는 듯 하다.<br/>
    <br/>
    하지만 가독성과 마크업 파일의 역할에 대해서 생각한 결과 주관적으로는 css 전처리기를 제일 먼저 적용해보고 싶었다.
    css 전처리기의 정의를 살펴보면 <i>CSS 전처리기는 전처리기의 자신만의 특별한 syntax를 가지고 CSS를 생성하도록 하는 프로그램입니다.</i> 라고 되어있는데 sass의 경우는 어떤지 살펴보자!<br/><br/><br/>
    
### 리액트(CRA 환경)에서 설치하기

<br/>
<code>
    npm i --save sass 
</code>
<br/>
<br/>
<br/>
    프로젝트에 sass를 설치하는 명령어이다.<br/>
    package.json에 들어가서 dependencies에 sass가 있는지 체크📌<br/>
    그리고 파일 확장자를 .scss로 작성하여 시작!
<br/>
<br/>

### SASS를 알아보자

<br/>
아래 CSS는 특정요소를 가운데 배치하는 코드이다.
레이아웃을 잡을때 flex를 많이 사용하는 편인데 
<br/>
<br/>

```css
.section {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```

매번 이런 코드를 작성하기엔 너무 생산성이 떨어진다고 생각했다.
그리고 SASS는 이런 문제를 대처하는 **@mixin** 이라는 키워드가 있다.
프로그래밍 언어처럼 조건문을 대체하는 **@if** , 하나의 함수로서 작동할 수 있는 **@function** 도 있다!
하지만 내가 어떤 필요에 의해 CSS 전처리기를 사용하고 생각하게 되었는지를 생각하면 **@mixin** 이나 중첩 선택자정도이지 않을까?

<br/>

그래서 두가지를 알아보았다.

1.**@mixin**을 통한 CSS재활용
2.&:를 통한 중첩 선택자

```scss
@mixin button {
  padding: 1rem;
  border: none;
  border-radius: 10px;
  width: 2rem;
}

.button-submit {
  @include button;
  background-color: green;
}
```

<br/>

이런식으로 버튼이라는 **@mixin** 을 작성하면 button을 재활용할 수 있고 우리는 지속적인 재활용을 할 수 있는 것이다.
SASS는 위에서 언급했듯이 중첩 선택자를 지원하는데 기존CSS와 달리 프로그래밍 언어들처럼 부모요소 안에서 **&:** 을 통해서
바로 사용할 수 있다. 위의 button을 hover했을 때 색깔이 바뀐다고 생각해보자. 기존의 CSS를 작성한다면
<br/>
<br/>

```css
.button-submit:hover {
  background-color: black;
}
```

위와 같이 작성해야겠지만 SASS에서는 &:를 사용해

```scss
.button-submit {
  @include button;
  background-color: green;

  &:hover {
    background-color: black;
  }
}
```

<br/>
위와 같이 사용할 수 있는 것이다. 가독성적인 측면과 편의성이 나름 해결되었다고 생각한다.
<br/>
그외에도 파일명앞에 _를 붙여서 상위파일에 import시 CSS로 컴파일할떄 제외되는 기능,
$키워드로 변수를 만들어 CSS value를 할당하는 등의 기능도 있다!

<br/>
다음 프로젝트 때 점진적으로 적용해보고 내 필요에 맞는 다른 CSS전처리기나 css-in-js를 찾아보고싶다.
