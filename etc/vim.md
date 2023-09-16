## vim 배우기

### 입력모드

- i - insert
- a - append(커서 뒤로)
- I는 문장 맨앞으로
- A는 문장 맨뒤로

### 명령모드

0-문장 앞으로 이동
$-문장 뒤로 이동
w 문장 단위 앞으로 이동  
b 문장 단위 뒤로 이동
(숫자 + w)로 몇개의 단어단위 이동가능

H 화면 위 중간
M 화면 중간
L 화면 끝
gg 파일 앞
G 파일 끝
(숫자 + G)로 몇번 줄 단위로 이동 가능

ctrl u 위로 스크롤
ctrl d 아래로 스크롤

{ 문단 시작
} 문단 끝

x커서 아래글자
dd 문장 삭제
yy 문장 복사
p 붙여넣기
\*p 클립보드 붙여넣기
<br/>

### 응용편

d + 3w 3단어 삭제
d + $ 문장 끝까지 삭제
d + d 문장 삭제

d + it 태그안에 있는 문장 삭제

aw a word
at a tag
ap aparagraph
as a sentence

it in tag
i" in ""
ip in paragraph

**명령어를 동일하게사용할때는 . 을 사용하면 된다.**
**u는 undo, ctrl + r은 redo**

di{를 하면 {}안에 있는 문장을 삭제한다.

핵심은 di+ object는 object안에 있는 문장을 삭제한다는 것이다.
그리고 da+ object는 object안에 있는 문장을 삭제하고 object까지 삭제한다는 것이다..

d + /는 검색한 단어까지 삭제한다.
d/ 검색한 단어까지

nomarl 모드에서 /를 누르고 검색을 할 수 있다.
n은 다음 검색, N은 이전 검색

v는 visual 모드로 들어간다.

v와 기존 명령어를 사용하면 된다.

- v + aw 단어단위로 선택
- ctrl
- v + $ 문장 끝까지 선택
