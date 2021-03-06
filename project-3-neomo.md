---
layout: page
title: NEOMO
---

[<img src="/assets/images/NEOMO/mainlogo.png">](https://github.com/neomorphism/neomo)

<font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B"> πGo to GitHub by clicking the image above!π</font>

<br>
<div style="text-align: left">
    <font size="7"> What is this? </font> <br>
    <font size="4"> Neomorphism(neumorphism) Design Framework Open Source </font>
</div>

<br>
<div style="text-align: left">
    <font size="7"> Tech Stack </font> <br>
    <img src="/assets/images/NEOMO/κΈ°μ μμ.png">
</div>

<br>
<div style="text-align: left">
    <font size="7"> Organization </font> <br>
    neomo/<br>
βββ css/<br>
β   βββ components/<br>
β   β   βββ alert.css<br>
β   β   βββ badge.css<br>
β   β   βββ breadcrumb.css<br>
β   β   βββ button.css<br>
β   β   βββ card.css<br>
β   β   βββ dropdown.css<br>
β   β   βββ icon.css<br>
β   β   βββ modal.css<br>
β   β   βββ navbar.css<br>
β   β   βββ navigation.css<br>
β   β   βββ pagination.css<br>
β   β   βββ progressbar.css<br>
β   β   βββ select.css<br>
β   β   βββ spinners.css<br>
β   β   βββ tab.css<br>
β   β   βββ toast.css<br>
β   β   βββ tooltips.css<br>
β   βββ content/<br>
β   β   βββ table.css<br>
β   βββ forms/<br>
β   β   βββ checkbox.css<br>
β   β   βββ file.css<br>
β   β   βββ floatinglabel.css<br>
β   β   βββ input.css<br>
β   β   βββ radio.css<br>
β   β   βββ range.css<br>
β   β   βββ switches.css<br>
β   βββ helpers/<br>
β   β   βββ coloredLinks.css<br>
β   β   βββ typography.css<br>
β   βββ layout/<br>
β   β   βββ columns.css<br>
β   β   βββ container.css<br>
β   βββ color.css<br>
β   βββ neomo.css<br>
βββ dist/<br>
β   βββ neomo.min.css<br>
β   βββ neomo.min.js<br>
βββ js/<br>
    βββ neomo.js<br>
</div>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 1. button.css </font>
</div>

1. **κ°μ΄λ° μ λ ¬**

   ```css
   justify-content: center; //κ°λ‘μΆμ κΈ°μ€μΌλ‘ μ’μ°μ λν μ λ ¬
   align-items: center; //μΈλ‘μΆμ κΈ°μ€μΌλ‘ μ’μ°μ λν μ λ ¬
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

   - inset λ€μ μ€λ μ²« λ²μ§Έ μμ: offset-x, μν κ±°λ¦¬λ₯Ό μλ―Ένλ©° μμ κ°μ κ·Έλ¦Όμλ₯Ό μμμ μΌμͺ½μ νμν¨
   - inset λ€μ μ€λ λ λ²μ§Έ μμ: offset-y, μμ§ κ±°λ¦¬λ₯Ό μλ―Ένλ©° μμ κ°μ κ·Έλ¦Όμλ₯Ό μμμ μμͺ½μ νμν¨
   - inset λ€μ μ€λ μΈ λ²μ§Έ μμ: blur-radius, κ°μ΄ ν΄μλ‘ κ·Έλ¦Όμ νλλ¦¬κ° νλ €μ§κ³  ν¬κΈ°κ° λ μ»€μ§κ³  μμ΄ λ λ°μμ§<br>
     <br>

3. **λ²νΌ ν¬κΈ° μ€μ **

   ```css
   button.normal {
     width: 5rem;
     height: 2.7rem;
   }
   ```

   - μ λμ μΈ κ°: px
   - μλμ μΈ κ°: rem, em
   - rem: κΈ°μ€μ΄ λλ κ°μ μ΅μμ μμμ font-size (e.g. html νκ·Έ)
   - em: κΈ°μ€μ΄ λλ κ°μ νμ¬ μ€νμΌ μ§μ  μμμ font-size (e.g. div νκ·Έ)
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

   - 0% λμ  From μ¬μ© κ°λ₯
   - 100% λμ  To μ¬μ© κ°λ₯
   - animation-timing-function: linear -> μ λλ©μ΄μ ν¨κ³Όκ° μ²μλΆν° λκΉμ§ μΌμ ν μλλ‘ μ§ν
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

   - inline: μ ν μ€λ°κΏ μμ΄ ν μ€μ λ€λ₯Έ μλ¦¬λ¨ΌνΈλ€κ³Ό λλν λ°°μΉ
   - block: μ ν μ€λ°κΏμ΄ λ€μ΄κ° νΌμ ν μ€ μ°¨μ§
   - inline-block: inline μλ¦¬λ¨ΌνΈμ²λΌ λλν λ°°μΉλμ§λ§, width & height & margin & padding μμ± μ§μ  κ°λ₯<br>
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

   - static: position μμ±μ λΆμ¬νμ§ μμμ λ κ°μ§λ λν΄νΈ κ°
   - relative: νμ¬ μμΉμμ μλμ μΈ offset μμ±μ μ€ μ μμ
   - absolute: λΆλͺ¨ μ€μ staticμ΄ μλ μμμ μμΉλ₯Ό κΈ°μ€μΌλ‘ μλμ μΈ offset μμ±μ μ€ μ μμ(νμ¬ μμΉκ° λ³νλ κ²μ μλ!)<br>
     <br>

3. **translate**

   ```css
   .tooltip .tooltip-content.bottom {
     transform: translateX(-50%);
     top: 115%;
     left: 50%;
   }
   ```

   - νμ¬ μμΉλ₯Ό κΈ°μ€μΌλ‘ μ΄λ
   - translateX(): κ°λ‘λ‘ μ΄λ(μμ κ°μ μ€λ₯Έμͺ½/μμ κ°μ μΌμͺ½)
   - translateY(): μΈλ‘λ‘ μ΄λ(μμ κ°μ μλμͺ½/μμ κ°μ μμͺ½)
   - translate(X, Y): κ°λ‘μΈλ‘ κ°μΌλ‘ μ΄λ<br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 4. input.css </font>
</div>

1. **> κ²°ν©μ**

   ```css
   .input-group > input {
     border: none;
   }
   ```

   - μ²« λ²μ§Έ μμμ λ°λ‘ μλ μμμΈ λΈλλ₯Ό μ ν<br>
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
   - container μμ μλ μμ΄νλ€μ κ°λ‘ λ°©ν₯μΌλ‘ λ°°μΉλκ³ , μμ μ΄ κ°μ§ λ΄μ©λ¬Όμ widthλ§νΌλ§ μ°¨μ§
   - flex-directionμ row, column, row-reverse, column-reverseκ° μμ<br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 5. switches.css </font>
</div>

1. **+ κ²°ν©μ**

   ```css
   input:checked + .switch {
     background: white;
     box-shadow: inset 3px 3px 5px #b8b9be, inset -3px -3px 5px #fff;
   }
   ```

   - μ²« λ²μ§Έ μμμ λ°λ‘ λ€μ μμΉνλ©΄μ κ°μ λΆλͺ¨λ₯Ό κ³΅μ νλ λ λ²μ§Έ μ ν<br>
     <br>

---

<div style="background-color: rgba(55, 114, 216, 0.8); text-algin: left; color: #F6F8F8">
    <font size="5" style="color: #F6F8F8"> 6. CSS Selectors </font>
</div>

1. **μ ν μ νμ**

   ```css
   input {
   }
   ```

   - μ£Όμ΄μ§ λΈλ μ΄λ¦(input)μ κ°μ§ λͺ¨λ  μμλ₯Ό μ ν<br>
     <br>

2. **ν΄λμ€ μ νμ**

   ```css
   .index {
   }
   ```

   - μ£Όμ΄μ§ ν΄λμ€ νΉμ±(index)μ κ°μ§ λͺ¨λ  μμλ₯Ό μ ν<br>
     <br>

3. **ID μ νμ**

   ```css
   #toc {
   }
   ```

   - id νΉμ±(toc)μ λ°λΌ μμλ₯Ό μ ν
   - λ¬Έμ λ΄μλ μ£Όμ΄μ§ idλ₯Ό κ°μ§ μμκ° νλλ§ μ‘΄μ¬<br>
     <br>
