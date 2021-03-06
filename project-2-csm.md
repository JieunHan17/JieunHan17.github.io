---
layout: page
title: CSM
---

[<img src="/assets/images/CSM/csm_logo.png">{: width="30%" height="30%"}](https://github.com/mancityg/CSMproject_Android)

<font style="background-color: #51AD91; color: white"> ðGo to GitHub by clicking the image above!ð</font>

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
        âââ com.suwonccc.csmproject/<br>
        â   âââ alarmpage_fragment/<br>
        â   â   âââ AlarmInfo<br>
        â   â   âââ AlarmInfoDAO<br>
        â   â   âââ AlarmpageFragment<br>
        â   â   âââ AlarmPageRecyclerView.kt<br>
        â   âââ etcpage/<br>
        â   â   âââ Etcpage_disconnect<br>
        â   â   âââ Etcpage_modify_mentee<br>
        â   â   âââ Etcpage_modify_mentor<br>
        â   â   âââ Etcpage_mymentee<br>
        â   â   âââ Etcpage_mymentee_list<br>
        â   â   âââ Ectpage_mymentor<br>
        â   â   âââ Ectpage_nomentee<br>
        â   â   âââ Ectpage_nomentor<br>
        â   â   âââ EtcpageFragment.kt<br>
        â   âââ firstpage_fragment/<br>
        â   â   âââ LoginComplete<br>
        â   â   âââ LoginExtraInfo<br>
        â   â   âââ LoginMain<br>
        â   â   âââ LoginMentee<br>
        â   â   âââ LoginMentor<br>
        â   â   âââ LoginProfile<br>
        â   âââ mainpage_fragment/<br>
        â   â   âââ MainpageFragment<br>
        â   â   âââ MainpageWaitMentorFragment.kt<br>
        â   â   âââ MainpageWelcomeMenteeFragment.kt<br>
        â   â   âââ MainpageWelcomeMentorFragment<br>
        â   â   âââ MainSearchMentorActivity<br>
        â   âââ recyclerview/<br>
        â   â   âââ mentee.kt<br>
        â   â   âââ MenteelistAdapter<br>
        â   â   âââ SearchMentorlistAdapter<br>
        â   âââ ChattingpageFragment.kt<br>
        â   âââ Firstpage<br>
        â   âââ MainActivity<br>
        â   âââ MessagingService<br>
        â   âââ UserstorypageFragment.kt<br>
</div>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 1. Login Main </font>
</div>

# **ë ì´ìì**

#### 1) ConstraintLayout

- Chainì ì¬ì©íì¬ íë©´ í´ìëì ë°ë¼ ê° ììì ìì¹ê° ë§ì´ ë¬ë¼ì§ì§ ìê² íê¸° ìí¨

<br>

#### 2) ImageButton

- backgroundë¥¼ í¬ëªíê² íê³ , srcì ì´ë¯¸ì§ íì¼ì ë£ì ê²

<br>

# **íëê·¸ë¨¼í¸**

#### 1) onCreateView vs onViewCreated

<img src="/assets/images/CSM/fragment_lifecycle.png">

- `onCreate()`: í´ë¹ ì½ë°±ì Fragmentê° ìì±ë  ë ë¨ í ë²ë§ í¸ì¶ëë¤. ë°ì´í°ì ê°ì ë¦¬ìì¤ ì´ê¸°í ììì ìííë ì í©íë¤.
- `onCreateView()`: í´ë¹ ì½ë°±ì Viewê° ìì±ëì´ ë§¤ê°ë³ìë¡ ì¬ì© ê°ë¥í ìì ì´ë¤. ëí, Fragmentê° back stackìì ëëìì¤ë ì§ì ì´ë¤.
- `onViewCreated()`: í´ë¹ ì½ë°±ì `onCreateView()`ê° í¸ì¶ë ì§í í¸ì¶ëë¤. ë·°ê° ìì í ìì±ëì´ ìë ì§ì ì´ë¤.

<br>

#### 2) Jetpack Navigation

- NavHost: íì ê·¸ëíìì ëìì íìíë ë¹ ì»¨íì´ë
- NavController: NavHostìì ì± íìì ê´ë¦¬íë ê°ì²´
- login_nav_graph.xmlì ë³ëë¡ ë§ë¤ì´ì¤

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 2. Login Profile </font>
</div>

# **ë ì´ìì**

#### 1) NestedScrollView

- ScrollViewë¥¼ ì¬ì©í  ëì ë¬ë¦¬, ëª¨ë  Viewê° í¨ê» ì¤í¬ë¡¤ì´ ë  ì ìì

<br>

#### 2) CircleImageView

- `implementation 'de.hdodenhof:circleimageview:3.0.0'`

<br>

# **íëê·¸ë¨¼í¸**

#### 1) PopupWindow

- fragment_login_profile_change_dialog.xmlì ë³ëë¡ ë§ë¤ì´ì¤

<br>

#### 2) PopupMenu

```kotlin
var popUpMenu = PopupMenu(wrapper, popup_req_btn)

popUpMenu.menu.add(Menu.NONE, 0, 0, "naver.com")
popUpMenu.menu.add(Menu.NONE, 1, 1, "gmail.com")
popUpMenu.menu.add(Menu.NONE, 2, 2, "hanmail.net")
```

<br>

#### 3) ê°¤ë¬ë¦¬ ì ê·¼

- ê°¤ë¬ë¦¬ ê¶í ë¶ì¬ -> `onRequestPermissionsResult()`ìì í´ë¹íë requestCodeì ë°ë¼ `dispatchPickGalleryIntent()` ì¤í -> `onActivityResult()`ìì í´ë¹íë resultCodeì ë°ë¼ `launchImageCrop()` ì¤í

<br>

#### 4) ì¹´ë©ë¼ ì ê·¼

- ì¹´ë©ë¼ ê¶í ë¶ì¬ -> `onRequestPermissionsResult()`ìì í´ë¹íë requestCodeì ë°ë¼ `dispatchTakePictureIntent()` ì¤í -> `onActivityResult()`ìì í´ë¹íë resultCodeì ë°ë¼ `galleryAddPic()` ì¤í

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 3. Login Mentor/Mentee </font>
</div>

# **ë ì´ìì**

#### 1) AutoCompleteTextView

- ìëìì± ê¸°ë¥ì ìí´ ì¬ì©
- `android:completionThreshold="2"`: ë¬¸ìì ê°ìê° 2ê°ì¼ ëë¶í° ìëìì± ê²ì ì¤í

<br>

#### 2) Button Selector

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- í´ë¦­íì ê²½ì° -->
    <item android:state_pressed="true" android:drawable="@drawable/firstpage_btn_next_pressed" />
    <item android:state_selected="true" android:drawable="@drawable/firstpage_btn_next_pressed" />
    <!-- í´ë¦­íì§ ìì ê²½ì° -->
    <item android:state_pressed="false" android:drawable="@drawable/firstpage_btn_next" />
    <item android:state_selected="false" android:drawable="@drawable/firstpage_btn_next" />
</selector>
```

- selector_next_btn.xmlì ë³ëë¡ ë§ë¤ì´ì¤(drawable í´ëì)
- `state_pressed`: ë·°ê° ëë ¸ì ë(í°ì¹ë í´ë¦­ì´ ë°ìíì ë)
- `state_selected`: ë·°ë¥¼ ì ííì ë(ë°©í¥í¤ë¡ ì´ëíë¤ê° ì ííì ë)
- `state_enabled`: ì¬ì©í  ì ìë ìíì¼ ë(í°ì¹ë í´ë¦­ ì´ë²¤í¸ ë±ì ë°ì ì ìë ìíì¼ ë)

<br>

# **íëê·¸ë¨¼í¸**

#### íêµ ê²ì ìëìì±

<img src="/assets/images/CSM/ArrayAdapter.png">

- dataë¥¼ ArrayListì ë£ì´ì£¼ê³ , ArrayAdapterë¥¼ ì´ì©íì¬ ì´ê²ì ì´ë»ê² ë³´ì¬ì¤ì§ ì§ì íë¤.

```kotlin
val textView = view.findViewById(R.id.mentor_school_edittext) as AutoCompleteTextView
val universities: Array<out String> = resources.getStringArray(R.array.universities_array)
ArrayAdapter<String>(requireContext(), android.R.layout.simple_list_item_1, universities).also { adapter ->
  textView.setAdapter(adapter)
}
</selector>
```

- `also`: ìì  ê°ì²´ ëë¤ê° ì ë¬ë ìì  ê°ì²´ë¥¼ ì í ì¬ì© íì§ ìê±°ë ìì  ê°ì²´ì ìì±ì ë³ê²½íì§ ìê³  ì¬ì©íë ê²½ì° also ë¥¼ ì¬ì©
- íì¥í¨ì: ê°ì²´ë¥¼ ì¬ì©í  ë ëªë ¹ë¬¸ë¤ì ë¸ë­ì¼ë¡ ë¬¶ì´ì ê°ê²°íê² ì¬ì©í  ì ìê² í´ì£¼ë í¨ì

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 4. Login Extra Info </font>
</div>

# **ë ì´ìì**

#### TableLayout

- `<TableRow>`ë¡ êµ¬ì±
- `android:completionThreshold="2"`: ë¬¸ìì ê°ìê° 2ê°ì¼ ëë¶í° ìëìì± ê²ì ì¤í

<br>

# **íëê·¸ë¨¼í¸**

#### ê° ë²í¼ ì í¨ì± ì²´í¬

- ë¹ì´ ìëì§ íì¸
- ì íí ë²í¼ì ê°ìê° 2ê°ë¥¼ ëëì§ íì¸

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 5. Login Complete </font>
</div>

# **íëê·¸ë¨¼í¸**

#### Mainpage Activityë¡ ì´ë

```kotlin
activity?.let{
  val intent = Intent (it, MainActivity::class.java)

  intent.flags = Intent.FLAG_ACTIVITY_CLEAR_TASK or Intent.FLAG_ACTIVITY_NEW_TASK
  it.startActivity(intent)
}
```

- `let`: ìì  ê°ì²´ì ìì± ë³ê²½ ê°ë¥
- T?.let { } ííììë non-null ì²´í¬ ê°ë¥
- cf> `with`ë ìì  ê°ì²´ì ìì±ì ë³ê²½í  ì ìì§ë§ `this`ë¥¼ ì¬ì©íì§ ììë ëë¤ë ì°¨ì´ì  ì¡´ì¬

<br>

---

<div style="background-color: #3DBAC2; text-algin: left; color: white">
    <font size="5"> 6. í¨ìí íë¡ê·¸ëë° </font>
</div>

# apply, with, let, also, run í¨ìì ì°¨ì´ì 

1. ë²ì ì§ì  í¨ì ì í¸ì¶ìì ìì  ê°ì²´ê° ë§¤ê° ë³ìë¡ ëªìì ì¼ë¡ ì ë¬ëê±°ë ìì  ê°ì²´ì íì¥ í¨ìë¡ ììì  ìì  ê°ì²´ ë¡ ì ë¬ëë¤.
2. ë²ì ì§ì  í¨ì ì ìì  ê°ì²´ ì§ì  ëë¤ ì ì ë¬ëë ìì  ê°ì²´ê° ëªìì  ë§¤ê° ë³ì ë¡ ì ë¬ ëê±°ë ìì  ê°ì²´ì íì¥ í¨ìë¡ ììì  ìì  ê°ì²´ë¡ ì½ë ë¸ë¡ ë´ë¶ë¡ ì ë¬ ëë¤.
3. ë²ì ì§ì  í¨ìì ê²°ê³¼ë¡ ìì  ê°ì²´ë¥¼ ê·¸ëë¡ ë°ííê±°ë ìì  ê°ì²´ ì§ì  ëë¤ ì ì¤í ê²°ê³¼ë¥¼ ë°ííë¤.

<br>

```kotlin
inline fun <T, R> with(receiver: T, block: T.() -> R): R {
    return receiver.block()
}
```

- ì¸ìë¡ ë°ë ê°ì²´ë¥¼ ì´ì´ì§ë ë¸ë¡ì ë¦¬ìë²ë¡ ì ë¬
- ë¸ë¡ì ê²°ê³¼ê° ë°í
- `run()`ê³¼ ë§¤ì° ë¹ì·(ë¦¬ìë²ë¡ ì ë¬í  ê°ì²´ê° ì´ëì ìì¹íëì§ë§ ë¤ë¦)

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

- í¨ìë¥¼ í¸ì¶íë ê°ì²´ë¥¼ ì´ì´ì§ë ë¸ë¡ì ë¦¬ìë²ë¡ ì ë¬
- ë¦¬ìë²: ë°ë¡ ì´ì´ì§ë ë¸ë¡ ë´ìì ë©ìë ë° ìì±ì ë°ë¡ ì ê·¼í  ì ìëë¡ í  ê°ì²´
- ê°ì²´ ìì²´ë¥¼ ë°í
- _íì©: í¹ì  ê°ì²´ë¥¼ ìì±íë©´ì í¨ê» ì´ê¸°íë¥¼ í´ì¼í  ë_

<br>

```kotlin
inline fun <T, R> T.let(block: (T) -> R): R {
    return block(this)
}
```

- í¨ìë¥¼ í¸ì¶íë ê°ì²´ë¥¼ ì´ì´ì§ë ë¸ë¡ì ì¸ìë¡ ëê¹
- ë¸ë¡ì ê²°ê³¼ê° ë°í
- _íì©: í¨ìë¥¼ í¸ì¶í ê°ì²´ë¥¼ ì¸ìë¡ ë°ì¼ë¯ë¡, ì´ë¥¼ ì¬ì©íì¬ ë¤ë¥¸ ë©ìëë¥¼ ì¤ííê±°ë ì°ì°ì ìíí´ì¼ íë ê²½ì°_

<br>

```kotlin
inline fun <T, R> T.run(block: T.() -> R): R {
    return block()
}
```

- í¨ìë¥¼ í¸ì¶íë ê°ì²´ë¥¼ ì´ì´ì§ë ë¸ë¡ì ë¦¬ìë²ë¡ ì ë¬
- ë¸ë¡ì ê²°ê³¼ê° ë°í
- _íì©: í¹ì  ê°ì²´ì ë©ìëë íëë¥¼ ì°ìì ì¼ë¡ í¸ì¶íê±°ë ê°ì í ë¹í  ë ì¬ì©_
- `apply()`ì íì©ì´ ì ì¬íì§ë§, `apply()`ë ìë¡ì´ ê°ì²´ë¥¼ ìì±í¨ê³¼ ëìì ì°ìë ììì´ íìí  ë ì¬ì©íê³  `run()`ì ì´ë¯¸ ìì±ë ê°ì²´ì ì°ìë ììì´ íìí  ë ì¬ì©íë¤ë ì ì´ ì¡°ê¸ ë¤ë¦ëë¤.

<br>

---
