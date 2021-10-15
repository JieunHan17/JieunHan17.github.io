---
layout: page
title: NEOMO
---

[<img src="/assets/images/NEOMO/mainlogo.png">](https://github.com/neomorphism/neomo)

<font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B"> 👆Go to GitHub by clicking the image above!👆</font>

<br>
<div style="text-align: left">
    <font size="7"> What is this? </font> <br>
    <font size="4"> Neomorphism(neumorphism) Design Framework Open Source </font>
</div>

<br>
<div style="text-align: left">
    <font size="7"> Tech Stack </font> <br>
    <font size="4"> CSS, JavaScript </font> <br>
    <font size="3"> (For the templates: HTML) </font>
</div>

<br>
<div style="text-align: left">
    <font size="7"> Organization </font> <br>
    neomo/<br>
├── css/<br>
│   ├── components/<br>
│   │   ├── alert.css<br>
│   │   ├── badge.css<br>
│   │   ├── breadcrumb.css<br>
│   │   ├── button.css<br>
│   │   ├── card.css<br>
│   │   ├── dropdown.css<br>
│   │   ├── icon.css<br>
│   │   ├── modal.css<br>
│   │   ├── navbar.css<br>
│   │   ├── navigation.css<br>
│   │   ├── pagination.css<br>
│   │   ├── progressbar.css<br>
│   │   ├── select.css<br>
│   │   ├── spinners.css<br>
│   │   ├── tab.css<br>
│   │   ├── toast.css<br>
│   │   └── tooltips.css<br>
│   ├── content/<br>
│   │   └── table.css<br>
│   ├── forms/<br>
│   │   ├── checkbox.css<br>
│   │   ├── file.css<br>
│   │   ├── floatinglabel.css<br>
│   │   ├── input.css<br>
│   │   ├── radio.css<br>
│   │   ├── range.css<br>
│   │   └── switches.css<br>
│   ├── helpers/<br>
│   │   ├── coloredLinks.css<br>
│   │   └── typography.css<br>
│   ├── layout/<br>
│   │   ├── columns.css<br>
│   │   └── container.css<br>
│   ├── color.css<br>
│   └── neomo.css<br>
├── dist/<br>
│   ├── neomo.min.css<br>
│   └── neomo.min.js<br>
└── js/<br>
    └── neomo.js<br>
</div>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 1. button.css </font>
</div>

1. **가운데 정렬**

   ```css
   justify-content: center; //가로축을 기준으로 좌우에 대한 정렬
   align-items: center; //세로축을 기준으로 좌우에 대한 정렬
   ```

   <br>

2. **box-shadow**

   ```css
   .button:hover {
     outline: 0;
     cursor: pointer;
     box-shadow: inset 3px 3px 5px #b8b9be, inset -3px -3px 5px #fff !important;
   }
   ```

   - inset 뒤에 오는 첫 번째 요소: offset-x, 수평 거리를 의미하며 음수 값은 그림자를 요소의 왼쪽에 표시함
   - inset 뒤에 오는 두 번째 요소: offset-y, 수직 거리를 의미하며 음수 값은 그림자를 요소의 위쪽에 표시함
   - inset 뒤에 오는 세 번째 요소: blur-radius, 값이 클수록 그림자 테두리가 흐려지고 크기가 더 커지고 색이 더 밝아짐<br>
     <br>

3. **버튼 크기 설정**

   ```css
   button.normal {
     width: 5rem;
     height: 2.7rem;
   }
   ```

   - 절대적인 값: px
   - 상대적인 값: rem, em
   - rem: 기준이 되는 값은 최상위 요소의 font-size (e.g. html 태그)
   - em: 기준이 되는 값은 현재 스타일 지정 요소의 font-size (e.g. div 태그)
     <br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 2. spinners.css </font>
</div>

1. **animation**

   ```css
   .loader.point-purple {
     border-bottom: 3px solid var(--purple);
     border-radius: 50%;
     width: 1.5em;
     height: 1.5em;
     animation: spin 2s linear infinite;
   }
   @keyframes spin {
     0% {
       transform: rotate(0deg);
     }
     100% {
       transform: rotate(360deg);
     }
   }
   ```

   - 0% 대신 From 사용 가능
   - 100% 대신 To 사용 가능
   - animation-timing-function: linear -> 애니메이션 효과가 처음부터 끝까지 일정한 속도로 진행
   - animation-iteration-count: infinite<br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 3. tooltips.css </font>
</div>

1. **display**

   ```css
   .tooltip {
     position: relative;
     display: inline-block;
   }
   ```

   - inline: 전후 줄바꿈 없이 한 줄에 다른 엘리먼트들과 나란히 배치
   - block: 전후 줄바꿈이 들어가 혼자 한 줄 차지
   - inline-block: inline 엘리먼트처럼 나란히 배치되지만, width & height & margin & padding 속성 지정 가능<br>
     <br>

2. **position**

   ```css
   .tooltip {
     position: relative;
     display: inline-block;
   }
   .tooltip .tooltip-content {
     visibility: hidden;
     padding: 7px;
     width: fit-content;
     position: absolute;
     z-index: 100;
   }
   ```

   - static: position 속성을 부여하지 않았을 때 가지는 디폴트 값
   - relative: 현재 위치에서 상대적인 offset 속성을 줄 수 있음
   - absolute: 부모 중에 static이 아닌 요소의 위치를 기준으로 상대적인 offset 속성을 줄 수 있음(현재 위치가 변하는 것은 아님!)<br>
     <br>

3. **translate**

   ```css
   .tooltip .tooltip-content.bottom {
     transform: translateX(-50%);
     top: 115%;
     left: 50%;
   }
   ```

   - 현재 위치를 기준으로 이동
   - translateX(): 가로로 이동(양수 값은 오른쪽/음수 값은 왼쪽)
   - translateY(): 세로로 이동(양수 값은 아래쪽/음수 값은 위쪽)
   - translate(X, Y): 가로세로 값으로 이동<br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 4. input.css </font>
</div>

1. **> 결합자**

   ```css
   .input-group > input {
     border: none;
   }
   ```

   - 첫 번째 요소의 바로 아래 자식인 노드를 선택<br>
     <br>

2. **flex**

   ```css
   .input-group {
     display: flex;
     width: fit-content;
     border-radius: 10px;
     box-shadow: 3px 3px 7px #ababab, -3px -3px 7px #ffffff;
   }
   ```

   - flex container
   - container 안에 있는 아이템들은 가로 방향으로 배치되고, 자신이 가진 내용물의 width만큼만 차지
   - flex-direction은 row, column, row-reverse, column-reverse가 있음<br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 5. switches.css </font>
</div>

1. **+ 결합자**

   ```css
   input:checked + .switch {
     background: white;
     box-shadow: inset 3px 3px 5px #b8b9be, inset -3px -3px 5px #fff;
   }
   ```

   - 첫 번째 요소의 바로 뒤에 위치하면서 같은 부모를 공유하는 두 번째 선택<br>
     <br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 6. CSS Selectors </font>
</div>

1. **유형 선택자**

   ```css
   input {
   }
   ```

   - 주어진 노드 이름(input)을 가진 모든 요소를 선택<br>
     <br>

2. **클래스 선택자**

   ```css
   .index {
   }
   ```

   - 주어진 클래스 특성(index)을 가진 모든 요소를 선택<br>
     <br>

3. **ID 선택자**

   ```css
   #toc {
   }
   ```

   - id 특성(toc)에 따라 요소를 선택
   - 문서 내에는 주어진 id를 가진 요소가 하나만 존재<br>
     <br>
