## ✨CSS 방법론

CSS사용시 클래스 이름을 어떻게 작성할지, 어떠한 방식으로 스타일을 작성할지 등 CSS를 보다 효율적으로 작성하기 위해 정의된 일종의 규칙

#### CSS 방법론을 사용하는 이유

- 원활한 유지보수
- 코드의 재사용성을 높이기 위해
- 클래스명만으로도 무슨 내용인지 예측할 수 있음

### 🎨OOCSS (Object Oriented CSS)

CSS를 모듈 방식으로 작성하여 중복을 줄이는 방식의 방법론

- 구조와 스타일을 분리하여 작성
- 중복되는 디자인 요소를 따로 빼내어 작성하기 때문에 반복적으로 사용 가능
- 코드의 재사용성이 높아져 코드량이 적어짐
- 다중 클래스 사용으로 코드의 가독성이 떨어질 수 있음

#### 컨테이너와 컨텐츠 분리

```html
<div class="header common-width">Header</div>
<div class="footer common-width">Footer</div>
```

```css
.header {
  position: fixed;
  top: 0;
}
.footer {
  position: relative;
  bottom: 0;
}
.common-width {
  width: 800px;
  margin: 0;
}
```

#### 구조와 모양을 분리하거나 결합

```html
// 기존 방식
<a class="instagram_btn instagram_skin">Instagram</a>
<a class="facebook_btn facebook_skin">Facebook</a>

// OOCSS 적용
<a class="btn skin instagram">Instagram</a>
<a class="btn skin facebook">Facebook</a>

.btn -> 공통 버튼 스타일 정의 .skin -> 공통 스킨 스타일 정의
```

### 🎨BEM (Block Element Modifier)

블록(Block), 요소(Element), 상태(Modifier)로 구분하여 클래스 이름을 작성하는 방식의 방법론

- 블록, 요소, 상태로 구성하고 각 부분을 `__`와 `--`로 구분하여 작성
- 어떠한 목적인가에 초점을 두어 이름을 지음
- 클래스명이 용도와 형태를 잘 표현하여 직관적으로 알 수 있으나, 클래스명이 길고 복잡해 질 수 있음

#### 블록

- 재사용이 가능하고 기능적으로 독립이 가능한 컴포넌트
- 일반적으로 하나의 단어를 사용하지만 길어질 경우 -를 사용

```css
.header {
  ..;
}
.block {
  ..;
}
```

#### 요소

- 블록을 구성하는 단위
- `__`를 사용

```css
.header {
  ..;
}
.header__tap {
  ..;
}
.header__content {
  ..;
}
.header__logo__button {
  ..;
}
```

#### 상태

- 블록이나 요소의 속성으로 `--`를 사용

```css
.header--hide {
  ..;
}
.header__tap--big {
  ..;
}
.header__content--disabled {
  ..;
}
```

### 🎨SMACSS (Scalable and Modular Architecture for CSS)

CSS를 범주화(Categorization)로 패턴화하고자 하는 방법론

- CSS를 비슷한 종류끼리 모아 5가지 스타일로 나누고 각 유형에 맞는 선택자와 작명법, 코딩 기법을 제시
- 카테고리 : 기본(Base), 레이아웃(Layout), 모듈(Module), 상태(State), 테마(Theme)

#### 기본

- Reset, Variable등을 포함하고 !important를 쓰지 않음

```css
body,
form,
p,
table,
button,
fieldset,
input ... {
  margin: 0;
  padding: 0;
}
```

#### 레이아웃

- 주요 요소(id)와 하위 요소(class)로 구분하고 접두사를 사용

```css
// layout => l-

// 주요 요소 작성
#header {
  width: 400px;
}
#aside {
  width: 40px;
}

// 하위 요소 작성
.l-width #header {
  width: 650px;
  padding: 10px;
}
.l-width #aside {
  width: 100px;
}
```

#### 모듈

- 재사용성이 높은 구성 요소를 정의

```css
.stick {
  ...;
}
.stick-name {
  ...;
}
.stick-number {
  ...;
}
```

#### 상태

- 요소의 상태 변화를 표현하고 접두사 `is-`나 `s-`를 사용

```css
.is-error {
  ...;
}
.is-hidden {
  ...;
}
.is-disabled {
  ...;
}
```

#### 테마

- 사용자가 선택 가능하도록 스타일을 재선언하여 사용

```css
// base.css
.header {
  background-color: red;
}
// theme.css
.header {
  background-color: orange;
}
```

### SMACSS 사용시 유의 사항

- 파생된 CSS 셀렉터 사용금지
- Id 셀렉터 사용금지
- !important 사용금지
- class 이름을 의미있게 지어야함

## ✨CSS 선택자 우선 순위

| 순위 | 선언방식           | 설명                                            | 예시                                                             |
| ---- | ------------------ | ----------------------------------------------- | ---------------------------------------------------------------- |
| 1    | !important         | 우선순위 최상위 명령어. 속성값 바로 뒤에 넣는다 | `p { color: red !important; }`                                   |
| 2    | inline style       | html 문서에서 tag 내에 style을 정의한 것        | `<p style="color: red"> `                                        |
| 3    | id Selector        | tag 내에 id를 정의한 후, #id 으로 선택          | `<p id="title">제목</p>`<br>`#title { color: red; }`             |
| 4    | class Selector     | or tag 내에 class를 정의한 후, .class 으로 선택 | `<p>class="subtitle">부제목</p>`<br>`.subtitle { color: red; } ` |
| 5    | tag Selector       | tag 요소를 선택자로 사용                        | `p { color: red; }`                                              |
| 6    | universal Selector | asterisk(\*)로 요소 전체를 선택                 | `* { color: red; }`                                              |

#### 이외의 경우

<table>
<tr>
<td>class 선택자 vs 특정 요소의 class 선택자 </td> <td>	특정 태그의 class 우선<br>ex) .title vs h1.title : h1.title가 더 구체적임 </td>
</tr>
<tr>
<td> 같은 요소 선택자에 대한 css </td> <td> 순서상 나중이 우선 </td>
</tr>
<tr>
<td> 같은 class 선택자에 대한 css </td> <td> 순서상 나중이 우선 </td>
</tr>
</table>
