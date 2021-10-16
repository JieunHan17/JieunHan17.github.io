---
layout: page
title: CSM
---

[<img src="/assets/images/CSM/csm_logo.png">{: width="30%" height="30%"}](https://github.com/mancityg/CSMproject_Android)

<font style="background-color: #51AD91; color: white"> 👆Go to GitHub by clicking the image above!👆</font>

<br>
<div style="text-align: left">
    <font size="7"> What is this? </font> <br>
    <font size="4"> Mentoring Application for Christian Students Who Will Enter the University </font>
</div>

<br>
<div style="text-align: left">
    <font size="7"> Tech Stack </font> <br>
    <font size="4"> Kotlin </font>
</div>

<br>
<div style="text-align: left">
    <font size="7"> Organization </font> <br>
      java/<br>
        ├── com.suwonccc.csmproject/<br>
        │   ├── alarmpage_fragment/<br>
        │   │   ├── AlarmInfo<br>
        │   │   ├── AlarmInfoDAO<br>
        │   │   ├── AlarmpageFragment<br>
        │   │   └── AlarmPageRecyclerView.kt<br>
        │   ├── etcpage/<br>
        │   │   ├── Etcpage_disconnect<br>
        │   │   ├── Etcpage_modify_mentee<br>
        │   │   ├── Etcpage_modify_mentor<br>
        │   │   ├── Etcpage_mymentee<br>
        │   │   ├── Etcpage_mymentee_list<br>
        │   │   ├── Ectpage_mymentor<br>
        │   │   ├── Ectpage_nomentee<br>
        │   │   ├── Ectpage_nomentor<br>
        │   │   └── EtcpageFragment.kt<br>
        │   ├── firstpage_fragment/<br>
        │   │   ├── LoginComplete<br>
        │   │   ├── LoginExtraInfo<br>
        │   │   ├── LoginMain<br>
        │   │   ├── LoginMentee<br>
        │   │   ├── LoginMentor<br>
        │   │   └── LoginProfile<br>
        │   ├── mainpage_fragment/<br>
        │   │   ├── MainpageFragment<br>
        │   │   ├── MainpageWaitMentorFragment.kt<br>
        │   │   ├── MainpageWelcomeMenteeFragment.kt<br>
        │   │   ├── MainpageWelcomeMentorFragment<br>
        │   │   └── MainSearchMentorActivity<br>
        │   ├── recyclerview/<br>
        │   │   ├── mentee.kt<br>
        │   │   ├── MenteelistAdapter<br>
        │   │   └── SearchMentorlistAdapter<br>
        │   ├── ChattingpageFragment.kt<br>
        │   ├── Firstpage<br>
        │   ├── MainActivity<br>
        │   ├── MessagingService<br>
        │   └── UserstorypageFragment.kt<br>
</div>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 1. Login Main </font>
</div>

# **레이아웃**

#### 1) ConstraintLayout

- Chain을 사용하여 화면 해상도에 따라 각 요소의 위치가 많이 달라지지 않게 하기 위함

<br>

#### 2) ImageButton

- background를 투명하게 하고, src에 이미지 파일을 넣을 것

<br>

# **프래그먼트**

#### 1) onCreateView vs onViewCreated

<img src="/assets/images/CSM/fragment_lifecycle.png">

- `onCreate()`: 해당 콜백은 Fragment가 생성될 때 단 한 번만 호출된다. 데이터와 같은 리소스 초기화 작업을 수행하는 적합하다.
- `onCreateView()`: 해당 콜백은 View가 생성되어 매개변수로 사용 가능한 시점이다. 또한, Fragment가 back stack에서 되돌아오는 지점이다.
- `onViewCreated()`: 해당 콜백은 `onCreateView()`가 호출된 직후 호출된다. 뷰가 완전히 생성되어 있는 지점이다.

<br>

#### 2) Jetpack Navigation

- NavHost: 탐색 그래프에서 대상을 표시하는 빈 컨테이너
- NavController: NavHost에서 앱 탐색을 관리하는 객체
- login_nav_graph.xml을 별도로 만들어줌

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 2. Login Profile </font>
</div>

# **레이아웃**

#### 1) NestedScrollView

- ScrollView를 사용할 때와 달리, 모든 View가 함께 스크롤이 될 수 있음

<br>

#### 2) CircleImageView

- `implementation 'de.hdodenhof:circleimageview:3.0.0'`

<br>

# **프래그먼트**

#### 1) PopupWindow

- fragment_login_profile_change_dialog.xml을 별도로 만들어줌

<br>

#### 2) PopupMenu

```kotlin
var popUpMenu = PopupMenu(wrapper, popup_req_btn)

popUpMenu.menu.add(Menu.NONE, 0, 0, "naver.com")
popUpMenu.menu.add(Menu.NONE, 1, 1, "gmail.com")
popUpMenu.menu.add(Menu.NONE, 2, 2, "hanmail.net")
```

<br>

#### 3) 갤러리 접근

- 갤러리 권한 부여 -> `onRequestPermissionsResult()`에서 해당하는 requestCode에 따라 `dispatchPickGalleryIntent()` 실행 -> `onActivityResult()`에서 해당하는 resultCode에 따라 `launchImageCrop()` 실행

<br>

#### 4) 카메라 접근

- 카메라 권한 부여 -> `onRequestPermissionsResult()`에서 해당하는 requestCode에 따라 `dispatchTakePictureIntent()` 실행 -> `onActivityResult()`에서 해당하는 resultCode에 따라 `galleryAddPic()` 실행

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 3. Login Mentor/Mentee </font>
</div>

# **레이아웃**

#### 1) AutoCompleteTextView

- 자동완성 기능을 위해 사용
- `android:completionThreshold="2"`: 문자의 개수가 2개일 때부터 자동완성 검색 실행

<br>

#### 2) Button Selector

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- 클릭했을 경우 -->
    <item android:state_pressed="true" android:drawable="@drawable/firstpage_btn_next_pressed" />
    <item android:state_selected="true" android:drawable="@drawable/firstpage_btn_next_pressed" />
    <!-- 클릭하지 않은 경우 -->
    <item android:state_pressed="false" android:drawable="@drawable/firstpage_btn_next" />
    <item android:state_selected="false" android:drawable="@drawable/firstpage_btn_next" />
</selector>
```

- selector_next_btn.xml을 별도로 만들어줌(drawable 폴더에)
- `state_pressed`: 뷰가 눌렸을 때(터치나 클릭이 발생했을 때)
- `state_selected`: 뷰를 선택했을 때(방향키로 이동하다가 선택했을 때)
- `state_enabled`: 사용할 수 있는 상태일 때(터치나 클릭 이벤트 등을 받을 수 있는 상태일 때)

<br>

# **프래그먼트**

#### 학교 검색 자동완성

<img src="/assets/images/CSM/ArrayAdapter.png">

- data를 ArrayList에 넣어주고, ArrayAdapter를 이용하여 이것을 어떻게 보여줄지 지정한다.

```kotlin
val textView = view.findViewById(R.id.mentor_school_edittext) as AutoCompleteTextView
val universities: Array<out String> = resources.getStringArray(R.array.universities_array)
ArrayAdapter<String>(requireContext(), android.R.layout.simple_list_item_1, universities).also { adapter ->
  textView.setAdapter(adapter)
}
</selector>
```

- `also`: 수신 객체 람다가 전달된 수신 객체를 전혀 사용 하지 않거나 수신 객체의 속성을 변경하지 않고 사용하는 경우 also 를 사용
- 확장함수: 객체를 사용할 때 명령문들을 블럭으로 묶어서 간결하게 사용할 수 있게 해주는 함수

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 4. Login Extra Info </font>
</div>

# **레이아웃**

#### TableLayout

- `<TableRow>`로 구성
- `android:completionThreshold="2"`: 문자의 개수가 2개일 때부터 자동완성 검색 실행

<br>

# **프래그먼트**

#### 각 버튼 유효성 체크

- 비어 있는지 확인
- 선택한 버튼의 개수가 2개를 넘는지 확인

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 5. Login Complete </font>
</div>

# **프래그먼트**

#### Mainpage Activity로 이동

```kotlin
activity?.let{
  val intent = Intent (it, MainActivity::class.java)

  intent.flags = Intent.FLAG_ACTIVITY_CLEAR_TASK or Intent.FLAG_ACTIVITY_NEW_TASK
  it.startActivity(intent)
}
```

- `let`: 수신 객체의 속성 변경 가능
- T?.let { } 형태에서는 non-null 체크 가능
- cf> `with`도 수신 객체의 속성을 변경할 수 있지만 `this`를 사용하지 않아도 된다는 차이점 존재

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 6. 함수형 프로그래밍 </font>
</div>

# apply, with, let, also, run 함수의 차이점

1. 범위 지정 함수 의 호출시에 수신 객체가 매개 변수로 명시적으로 전달되거나 수신 객체의 확장 함수로 암시적 수신 객체 로 전달된다.
2. 범위 지정 함수 의 수신 객체 지정 람다 에 전달되는 수신 객체가 명시적 매개 변수 로 전달 되거나 수신 객체의 확장 함수로 암시적 수신 객체로 코드 블록 내부로 전달 된다.
3. 범위 지정 함수의 결과로 수신 객체를 그대로 반환하거나 수신 객체 지정 람다 의 실행 결과를 반환한다.

<br>

```kotlin
inline fun <T, R> with(receiver: T, block: T.() -> R): R {
    return receiver.block()
}
```

- 인자로 받는 객체를 이어지는 블록의 리시버로 전달
- 블록의 결과값 반환
- `run()`과 매우 비슷(리시버로 전달할 객체가 어디에 위치하는지만 다름)

<br>

```kotlin
inline fun <T> T.also(block: (T) -> Unit): T {
    block(this)
    return this
}
```

<br>

```kotlin
inline fun <T> T.apply(block: T.() -> Unit): T {
    block()
    return this
}
```

- 함수를 호출하는 객체를 이어지는 블록의 리시버로 전달
- 리시버: 바로 이어지는 블록 내에서 메서드 및 속성에 바로 접근할 수 있도록 할 객체
- 객체 자체를 반환
- _활용: 특정 객체를 생성하면서 함께 초기화를 해야할 때_

<br>

```kotlin
inline fun <T, R> T.let(block: (T) -> R): R {
    return block(this)
}
```

- 함수를 호출하는 객체를 이어지는 블록의 인자로 넘김
- 블록의 결과값 반환
- _활용: 함수를 호출한 객체를 인자로 받으므로, 이를 사용하여 다른 메서드를 실행하거나 연산을 수행해야 하는 경우_

<br>

```kotlin
inline fun <T, R> T.run(block: T.() -> R): R {
    return block()
}
```

- 함수를 호출하는 객체를 이어지는 블록의 리시버로 전달
- 블록의 결과값 반환
- _활용: 특정 객체의 메서드나 필드를 연속적으로 호출하거나 값을 할당할 때 사용_
- `apply()`와 활용이 유사하지만, `apply()`는 새로운 객체를 생성함과 동시에 연속된 작업이 필요할 때 사용하고 `run()`은 이미 생성된 객체에 연속된 작업이 필요할 때 사용한다는 점이 조금 다릅니다.

<br>

---
