---
title: Activity Life Cycle
layout: post
post-image: "https://evgenii.com/image/blog/2015-03-27-testing-ui-in-android-studio/0120_new_project_select_empty_activity_in_android_studio.png"
description: Activity에 대해 알아보기
tags:
  - Android Studio
  - Activity
---

# Activity의 3가지 상태

1. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Resumed(Active)</font>: Focus를 가지고 있으며 화면에 보이는 상태

   - Dialog에 가려진 Activity도 Resumed(Dialog 또한 Activity의 일부이므로)

   <br>

2. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Paused</font>: 화면에는 보이지만 Focus를 받지 못하고 있는 상태

   - 투명한 Activity에 가려진 Activity는 Paused
   - 시스템이 이를 메모리에서 삭제하려면 종료 요청(`finish()` 메서드 호출) 또는 액티비티의 프로세스 중단

   <br>

3. <font style="background-color: rgba(55, 114, 216, 0.288); color: #1E3D6B">Stopped</font>: 화면에 보이지 않는 상태

   - 시스템이 이를 메모리에서 삭제하려면 종료 요청(`finish()` 메서드 호출) 또는 액티비티의 프로세스 중단

---

# Activity의 생명 주기

<img src="/assets/images/lifecycle.png">

1. onCreate()

   - 활동의 필수 구성요소 초기화
   - 뷰 생성
   - 데이터를 목록에 결합(데이터 바인딩)
   - `setContentView()`를 호출하여 UI를 위한 레이아웃 정의
   - 완료되면 다음 콜백은 항상 `onStart()`
     <br>
     <br>

2. onStart()

   - Activity가 사용자에게 **<font style="color: red">표시되기</font>** 직전에 호출
   - Activity가 Foreground로 나옴
     <br>
     <br>

3. onResume()

   - Activity가 사용자와 **<font style="color: red">상호작용하기</font>** 직전에 호출
   - 이 시점에서 Activity는 Activity Stack의 맨 위에 있으며, 사용자가 정보 입력중
   - 완료되면 다음 콜백은 항상 `onPause()`
     <br>
     <br>

4. onPause()

   - 시스템이 다른 Activity를 재개하기 직전에 호출
   - 빨리 끝내야 하는 메서드(이것이 반환될 때까지 다음 Activity가 재개되지 않으므로)
     <br>
     <br>

5. onStop()

   - Activity가 사용자에게 표시되지 않게 되면 호출
   - 해당 Activity가 소멸되는 중(-> `onDestroy()`)이거나 다른 Activity가 덮고 있는 중(-> `onRestart()`)
   - 메모리 관리 등을 위해 Activity 상태를 Bundle에 저장하는 작업 진행(`onSavedInstanceState()` _단, 많은 양의 데이터 저장 불가_)
     <br>
     <br>

6. onDestroy()
   - Activity가 소멸되기 전에 호출
   - `finish()`를 호출해서이거나 시스템이 공간을 절약하기 위해 인스턴스를 일시적으로 소멸시키기 때문
     <br>
     <br>

---

# ViewModel

- Activity와 Fragment에서 사용되는 UI 관련 데이터를 보관하고, 관리하기 위해 디자인됨
- Activity를 재생성 하는 상황에서도 ViewModel 인스턴스를 유지함으로써 데이터를 안전하게 다룰 수 있음
- Activity와 Fragment는 UI를 업데이트하는 역할에만 집중
- `onCreate()`가 여러 번 호출되는 상황에서도 ViewModel Scope는 일관되게 유지
- Fragment 간 데이터 공유에서 Activity가 중간자 역할을 안 해도 됨
- Activity가 `onDestroy()`를 호출할 때 종료가 되며, 이때 `onCleared()` 함수가 호출됨
- <font style="color: red">주의: ViewModel에 Activity, Fragment, View에 대한 Context를 저장해서는 안됨</font> -> 메모리 릭 발생
- 기기의 구성이 변경(e.g. 화면 전환)되었을 때만 유지됨

---
