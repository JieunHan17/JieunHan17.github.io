---
title: Android Application Components
layout: post
post-image: "https://miro.medium.com/max/2000/1*33hzCoxAoUehHrHeBJi-VA.png"
description: Basic Components & Additional Components
tags:
  - Android Studio
  - Components
---

# Basic Components

1. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Activities</font>
   <br>

   - 스마트폰과의 사용자 상호작용을 처리
   - Android GUI 요소 중에 화면을 의미

      <br>

2. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Services</font>
   <br>

   - Application과 연관된 Background 프로세싱 처리
   - 화면에 존재하지 않음
   - manifest에 선언해야 함
   - e.g. 배경음악

      <br>

3. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Broadcast Receivers</font>
   <br>

   - Android OS와 Application 사이의 소통 처리(Application이 알아야 하는 상황이 발생하면 알려줌)
   - BroadcastReceiver 클래스의 서브클래스로 구현
   - `sendBroadcast()`를 사용하여 Intent를 주고 받기
   - e.g. 배터리 부족, 문자 수신, 언어 변경

      <br>

4. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Content Providers</font>
   <br>

   - 데이터와 데이터베이스 관리 문제 처리
   - Content Provider 클래스의 서브클래스로 구현
   - 생명주기가 없음
   - 데이터 쓰기 및 읽기에 대한 허가 필요
   - e.g. 주소록, 이미지, 오디오

---

# Additional Components

1. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Fragments</font>
   <br>

   - 전체 UI의 부분
   - 화면의 일부만 차지
   - 다양한 Activity 안에서 재사용 가능
   - View와 View Groups 포함

      <br>

2. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Views</font>
   <br>

   - Android GUI 요소 중에 각각의 GUI 요소 의미(e.g. Text View, Button)
   - View Groups: View를 모아놓은 것

      <br>

3. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Layouts</font>
   <br>

   - Activity나 Fragment가 포함해야 할 GUI 컴포넌트를 명시

      <br>

4. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Resources</font>
   <br>

   - images, strings, and other material
   - 화면 크기에 따라 서로 다른 자원 사용 가능

      <br>

5. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Manifest</font>
   <br>

   - 패키지 정보를 담고 있음
   - manifest가 AndroidManifest.xml 파일의 root element

---
