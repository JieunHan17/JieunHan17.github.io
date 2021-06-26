---
layout: page
title: Connect Ajou
---

[<img src="/assets/images/connect-ajou/1.png">](https://github.com/amelia9981/Connect_Ajou)

<font style="background-color: #D7DDE2; color: #1E3D6B"> 👆Go to GitHub by clicking the image above!👆</font>

<br>
<div style="text-align: left">
    <font size="7"> What is this? </font> <br>
    <font size="4"> It is a mobile application project for international students at Ajou University and Korean students who want to join various exchange programs from Ajou University. </font>
</div>

<br>
<div style="text-align: left">
    <font size="7"> Tech Stack </font> <br>
    <font size="4"> React Native, Firebase </font>
</div>

<br>
<div style="text-align: left">
    <font size="7"> Organization </font> <br>
    CONNECT_AJOU/<br>
    ├── App.js<br>
    ├── MainScreenF.js<br>
    ├── Utilities/<br>
    │ ├── Firebase.js<br>
    │ └── UserPermissions.js<br>
    ├── Pages/<br>
    │   ├── AlarmPage/<br>
    │   │ ├── Chat.js<br>
    │   │ ├── ChatList.js<br>
    │   │ ├── Message.js<br>
    │   │ └── Notification.js<br>
    │   ├── CommunityPage/<br>
    │   │ ├── subCommunityPage/<br>
    │   │ │ ├── addWriting.js<br>
    │   │ │ ├── searchWriting.js<br>
    │   │ │ ├── seeWriting.js<br>
    │   │ │ └── showList.js<br>
    │   │ ├── FindFriend.js<br>
    │   │ ├── GetInfo.js<br>
    │   │ ├── schoolLife.js<br>
    │   │ └── showAll.js<br>
    │   ├── HomeTab/<br>
    │   │ ├── AddFavorites.js<br>
    │   │ └── HomeTabMain.js<br>
    │   └── TimetablePage/<br>
    │       ├── CourseItem.js<br>
    │       ├── PickCourses.js<br>
    │       └── Timetable.js<br>
    ├── Alarm.js<br>
    ├── CommunityMain.js<br>
    ├── handleCommunity.js<br>
    ├── handleHome.js<br>
    ├── HomeTabF.js<br>
    ├── Login.js<br>
    ├── Registration.js<br>
    ├── TimetableTab.js<br>
    └── User.js<br>
</div>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 1. App.js </font>
</div>

1. **디바이스에 따라 폰트 사이즈가 변동되지 않도록 설정**

   ```javascript
   Text.defaultProps = Text.defaultProps || {};
   Text.defaultProps.allowFontScaling = false;
   ```

   <br>

2. **폰트 로드 & 푸시 알람은 다 비동기로 동작**

   ```javascript
   async function registerForPushNotification() {
   let token;
   if (Constants.isDevice) {
       const { status: existingStatus } =
       await Notifications.getPermissionsAsync();
       let finalStatus = existingStatus;
       if (existingStatus !== "granted") {
       const { status } = await Notifications.requestPermissionsAsync();
       finalStatus = status;
       }
       if (finalStatus !== "granted") {
       alert("Failed to get push token for push notification!");
       return;
       }
       token = (await Notifications.getExpoPushTokenAsync()).data;
       console.log(token);
   } else {
       alert("Must use physical device for Push Notifications");
   }
   ```

   실제 디바이스인지 확인 -> 현재 권한이 있는지 확인 -> 없으면 권한 요청 -> 최종 권한 확인

    <br>

3. **실행 로직**

   폰트가 다 로드되었고, 유저 정보 로딩이 끝나면 유저 정보 체크

   -> 유저가 있으면 MainScreenF.js로 바로 넘어감 / 유저가 없으면 Registration.js로 넘어감

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 2. Registration.js </font>
</div>

1. **이메일과 비밀번호로 가입**

   ```javascript
   firebase
      .auth()
      .createUserWithEmailAndPassword(email, password)
      .then((response) => {
        const uid = response.user.uid;
        const data = {
          email,
          fullName,
          picture,
          url,
          myCourses,
        };
   ```

   <br>

2. **유저 데이터 생성**

   > 이메일, 성명, 프로필 이미지 여부, 프로필 이미지 주소, 나의 수강목록

   ```javascript
   const usersRef = firebase.firestore().collection("users");
   usersRef
     .doc(email)
     .set(data)
     .then(() => {
       setReRendering(isReRendering + 1);
     })
     .catch((error) => {
       console.error("Error: ", error);
     });
   ```

    <br>
   > 커뮤니티 즐겨찾기

   ```javascript
   const favoritesRef = firebase.firestore().collection("favorites");
   favoritesRef.doc(email).set(
     {
       selectedItemsArray: [],
     },
     { merge: true }
   );

   allCommunities.forEach((element) => {
     favoritesRef
       .doc(email)
       .collection("all")
       .doc(element)
       .set({}, { merge: true });
   });

   favoritesRef.doc(email).collection("selectedItems").add({});
   ```

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 3. MainScreenF.js </font>
</div>

1. **Bottom Tab Navigator**

   - Pages/handleHome.js
   - Pages/CommunityMain.js
   - Pages/TimetableTab.js
   - Pages/Alarm.js
   - Pages/User.js

   <br>

2. **유저 데이터 불러오기**

   ```javascript
   const curUserEmail = firebase.auth().currentUser.providerData[0].email;
   const unsubscribe = firebase
     .firestore()
     .collection("users")
     .doc(curUserEmail)
     .onSnapshot((snapshot) => {
       const getUser = snapshot.data();
       setUser(getUser);
       if (!getUser.myCourses.length) {
         return () => {
           unsubscribe();
         };
       }
   ```

   <br>

3. **수강목록 데이터 불러오기**

   ```javascript
   getUser.myCourses.forEach((course) => {
     let background = randomHex();
     const courseRef = firebase.firestore().collection("courses").doc(course);
     courseRef.get().then((doc) => {
       const getMyCourse = doc.data();
       let array_of_schedules = splitSchedule(getMyCourse.schedule);
       for (var i = 0; i < array_of_schedules.length; i++) {
         let day = array_of_schedules[i].substr(0, 3);
         let time = array_of_schedules[i].substr(4, 1);
         let row = matchTime(time);
         let column = matchDays(day);
         if (isSelected[row][column] == "#FFFFFF") {
           isSelected[row][column] = background;
           courseName[row][column] = getMyCourse.name;
         }
       }
     });
   });
   ```

   나의 수강목록에 해당하는 과목 정보 가져오기 -> 과목 스케쥴 확인 -> 해당하는 시간표 배열에 배경색 & 과목명 지정

   <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 4. handleHome.js </font>
</div>

1. **Stack Navigator**

   - Pages/HomeTabF.js
   - Pages/CommunityPage/subCommunityPage/showList.js
   - Pages/CommunityPage/subCommunityPage/addWriting.js
   - Pages/CommunityPage/subCommunityPage/searchWriting.js
   - Pages/CommunityPage/subCommunityPage/seeWriting.js

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 5. HomeTabF.js </font>
</div>

1. **Stack Navigator**

   - Pages/HomeTab/HomeTabMain.js
   - Pages/HomeTab/AddFavorites.js

   <br>

2. **즐겨찾기에 추가된 커뮤니티 데이터 불러오기**

   ```javascript
   const getSelectedItems = firebase
     .firestore()
     .collection("favorites")
     .doc(curUserEmail)
     .collection("selectedItems")
     .orderBy("createdAt", "desc")
     .onSnapshot((querySnapshot) => {
       const selectedItems = querySnapshot.docs.map((docSnapshot) => {
         const selectedItem = {
           _id: docSnapshot.id,
           ...docSnapshot.data(),
         };
         return selectedItem;
       });
       setSelectedItems(selectedItems);
     });
   ```

    <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 6. AddFavorites.js </font>
</div>

1. **즐겨찾기와 관련된 데이터 불러오기**

   - 즐겨찾기에 추가된 커뮤니티 데이터: selectedItems
   - 즐겨찾기에 추가된 커뮤니티 배열: selectedItemsArray
   - 모든 커뮤니티: allItems

   <br>

2. **즐겨찾기에 추가할 커뮤니티 선택**

   ```javascript
   const pick = (community) => {
     let tempSelectedItems = selectedItemsArray;
     const index = tempSelectedItems.indexOf(community._id);
     if (index > -1) {
       tempSelectedItems.splice(index, 1);
     } else {
       tempSelectedItems.push(community._id);
     }
     setSelectedItemsArray(tempSelectedItems);
     setReRendering(isReRendering + 1);
   };
   ```

   이미 체크되어 있다면 해제 / 체크하지 않았다면 체크

   ```javascript
   {
     selectedItemsArray.includes(item._id) ? (
       <MaterialIcons
         name="check-box"
         size={24}
         color="black"
         style={style.communityIcon}
       />
     ) : (
       <MaterialIcons
         name="check-box-outline-blank"
         size={24}
         color="black"
         style={style.communityIcon}
       />
     );
   }
   ```

    <br>

3. **즐겨찾기에 추가**

   ```javascript
   selectedItemsArray.forEach((item) => {
     selectedItemsRef
       .doc(item)
       .set(
         {
           createdAt: new Date().getTime(),
         },
         { merge: true }
       )
       .catch(function (error) {
         console.error("Error: ", error);
       });
   });
   ```

   추가한 시각과 함께 DB에 업로드

   ```javascript
   firebase
     .firestore()
     .collection("favorites")
     .doc(user.email)
     .set(
       {
         selectedItemsArray: selectedItemsArray,
       },
       { merge: true }
     )
     .catch(function (error) {
       console.error("Error: ", error);
     });
   ```

    <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 7. CommunityMain.js </font>
</div>

1. **Stack Navigator**

   - Pages/HandleCommunity.js
   - Pages/CommunityPage/subCommunityPage/showList.js
   - Pages/CommunityPage/subCommunityPage/addWriting.js
   - Pages/CommunityPage/subCommunityPage/searchWriting.js
   - Pages/CommunityPage/subCommunityPage/seeWriting.js

   <br>

2. **커뮤니티 네비게이션 헤더 이름 설정**

   ```javascript
   function getHeaderTitle(route) {
     const routeName = getFocusedRouteNameFromRoute(route) ?? "All";

     switch (routeName) {
       case "All":
         return "All";
       case "Info":
         return "Info";
       case "Campus":
         return "Campus";
       case "Friends":
         return "Friends";
     }
   }
   ```

    <br>
   `getFocusedRouteNameFromRoute(route)`는 현재 활성화되어 있는 route의 이름을 반환

   -> 만약 이 값이 null이거나 undefined이면 오른쪽 값 반환

   <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 8. showList.js </font>
</div>

1. **글 목록 가져오기**

   ```javascript
   const getData = db.onSnapshot((querySnapshot) => {
     const writings = querySnapshot.docs.map((docSnapshot) => {
       const data = {
         _id: docSnapshot.id,
         ...docSnapshot.data(),
       };
       return data;
     });
     setWriting(writings);
   });
   ```

   <br>
   실시간으로 가져오기 위해 `onSnapshot` 사용<br>

2. **글 목록 보여주기**

   ```javascript
   <ScrollView style={style.container}>
       {writing.map((writing) => (
         <TouchableOpacity
           onPress={() => {
             navigation.push("See", {
               extraData: user,
               data: writing,
               listName: listName,
             });
           }}
           key={writing._id}
         >
           <Card style={style.box}>
   ```

   <br>
   데이터를 mapping 해서 스크롤뷰에서 보여줌<br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 9. addWriting.js </font>
</div>

1. **헤더 설정**

   `useLayoutEffect`: 렌더링 후 화면이 업데이트 되기 전에 동기적으로 실행(cf. `useEffect`는 비동기적으로 실행)
   <br>

2. **글 작성**

   ```javascript
   const onSubmit = async (event) => {
     firebase
       .firestore()
       .collection(listName)
       .doc(title)
       .set({
         _id: Math.random().toString(36).slice(2),
         title: title,
         content: content,
         creator: user,
         createdAt: Date.now(),
         like: [],
         comments: [],
       })
       .then(() => {
         navigation.goBack();
       });
     setTitle("");
     setContent("");
   };
   ```

  <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 10. searchWriting.js </font>
</div>

1. **검색 데이터 가져오기**

   ```javascript
   const fetchWriting = () => {
     if (writing) {
       setWriting([]);
     }
     listRf
       .where("title", "<=", search)
       .get()
       .then((querySnapshot) => {
         querySnapshot.forEach((doc) => {
           const data = doc.data();
           setWriting((prev) => [data, ...prev]);
         });
       });

     setisSearch(false);
   };
   ```

   <br>

2. **검색 버튼 이벤트**

   ```javascript
   <Right>
           <TouchableOpacity
             onPress={() => {
               fetchWriting();
               setisSearch(true);
             }}
           >
             <Feather name="search" size={30} />
           </TouchableOpacity>
         </Right>
   };
   ```

   <br>
   `isSearch` 값이 true 이면 검색 결과가 보여진다.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 11. seeWriting.js </font>
</div>

1. **좋아요 클릭**

2. **댓글 작성**

3. **글 목록 가져오기**

   ```javascript
   function getData() {
     const dbCom = firebase.firestore().collection(listName).doc(writing.title);
     dbCom.onSnapshot((doc) => {
       if (doc.data() !== undefined) {
         const data = doc.data().comments;
         setAllComment(data);
         const likeList = doc.data().like;
         setCurrentLike(likeList);
       }
     });
   }
   ```

   <br>
   글을 삭제하고 난 후에는 `doc.data()`가 undefined가 되므로 if문을 추가하였다.

   <br>

4. **글 수정**

   ```javascript
   const reWritingUpdate = () => {
     firebase
       .firestore()
       .collection(listName)
       .doc(writing.title)
       .get()
       .then((doc) => {
         firebase.firestore().collection(listName).doc(reTitle).set(
           {
             title: reTitle,
             content: reContent,
             comments: doc.data().comments,
             createdAt: doc.data().createdAt,
             creator: doc.data().creator,
             like: doc.data().like,
           },
           { merge: true }
         );
       });
     firebase.firestore().collection(listName).doc(writing.title).delete();
     setReModal(false);
     setModalVisible(false);
     navigation.goBack();
   };
   ```

   글 제목이 바뀌므로 원래 존재하던 doc을 지워주고 새로운 doc을 생성하여야 한다.<br>
   `<Modal>`안에 `<Modal>`을 또 넣어줘서 글을 수정할 때만 팝업창이 보이도록 하였다.

   <br>

5. **글/댓글 삭제**

   ```javascript
   onPress: () => {
               firebase
                 .firestore()
                 .collection(listName)
                 .doc(writing.title)
                 .update({
                   comments: firebase.firestore.FieldValue.arrayRemove(comment),
                 });
             },
   ```

   댓글 삭제 시, [Firebase 배열 요소 업데이트 참고](https://firebase.google.com/docs/firestore/manage-data/add-data#update_elements_in_an_array)

   <br>

6. **글 작성자와 채팅 시작**

   - 글 작성자가 본인이 아닌 경우, 기존 채팅방으로 이동(cf. 본인일 경우에는 마이 페이지로 이동)
   - 만약 기존 채팅방이 존재하지 않는다면 새로운 채팅방 생성

     ```javascript
     if (
          Object.keys(thread).length === 0 &&
          thread.constructor === Object
        ) {
          thread = {
            latestMessage: {
              text: "",
              createdAt: new Date().getTime(),
            },
            name: commentAuthor.fullName,
            target: {
              email: commentAuthor.email,
            },
            user: user,
          };

          firebase
            .firestore()
            .collection("chat")
            .doc(commentAuthor.email)
            .set(thread, { merge: true });

          firebase
            .firestore()
            .collection("chat")
            .doc(commentAuthor.email)
            .collection("messages")
            .add({
              text: "Your chat room has been created.",
              createdAt: new Date().getTime(),
              system: true,
            });
     ```

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 12. TimetableTab.js </font>
</div>

1. **Stack Navigator**

   - Pages/TimetablePage/Timetable.js
   - Pages/TimetablePage/PickCourses.js

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 13. Timetable.js </font>
</div>

1.  **전체 강의 목록 가져오기**

    `setCourses(array)`

    <br>

2.  **내가 수강하는 강의 목록 가져오기**

    `setMyCourses(getUser.myCourses)`

    <br>

3.  **강의 삭제**

    ```javascript
    const handleClickCourse = (courseName, row, col) => {
      Alert.alert("Do you want to remove this course?", courseName, [
        {
          text: "No",
          onPress: () => console.log("No"),
        },
        {
          text: "Yes",
          onPress: () => {
            console.log("Yes");
            removeBackground(isSelected[row][col]);
            let selected_code = getCourseCode(courseName);
            update_array = myCourses.filter(
              (element) => element !== selected_code
            );
            userRef
              .set(
                {
                  myCourses: update_array,
                },
                { merge: true }
              )
              .catch(function (error) {
                console.error("Error: ", error);
              });
          },
          style: "destructive",
        },
      ]);
    };
    ```

     <br>
     `filter()` 메서드는 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환한다.

     <br>

4.  **시간표 틀 생성**

    `<View>` 태그로 테이블을 만들었다.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 14. PickCourses.js </font>
</div>

1.  **전체 강의 목록 가져오기**

    `setCourses(array)`

    <br>

2.  **내가 수강하는 강의 목록 가져오기**

    `setMyCourses(getUser.myCourses)`

    <br>

3.  **강의 추가**

    ```javascript
    const handlePickCourse = (schedule, code, name) => {
      console.log("handling");
      let array_of_schedules = splitSchedule(schedule);
      setBackground(randomHex());
      for (var i = 0; i < array_of_schedules.length; i++) {
        let day = array_of_schedules[i].substr(0, 3);
        let time = array_of_schedules[i].substr(4, 1);
        if (isSelected[matchTime(time)][matchDays(day)] != "#FFFFFF") {
          Alert.alert("Duplicate Entry");
          return;
        }
        isSelected[matchTime(time)][matchDays(day)] = background;
        courseName[matchTime(time)][matchDays(day)] = name;
      }
      let update_array = myCourses;
      update_array.push(code);
      userRef
        .set(
          {
            myCourses: update_array,
          },
          { merge: true }
        )
        .catch(function (error) {
          console.error("Error: ", error);
        });
    };
    ```

    - myCourses에는 과목 코드로 저장된다.
    - 시간이 중복되면 추가가 되지 않는다.

    <br>

4.  **강의 목록 보여주기**

    ```javascript
    <ScrollView>
      {courses.map((course) => (
        <TouchableOpacity
          onPress={() =>
            handlePickCourse(course.schedule, course.code, course.name)
          }
          key={course.code}
        >
          <CourseItem
            name={course.name}
            prof={course.prof}
            schedule={course.schedule}
            credits={course.credits}
            code={course.code}
          />
        </TouchableOpacity>
      ))}
    </ScrollView>
    ```

    <br>
    `courses.map()`을 사용해서 CourseItem.js의 function을 보여준다.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 15. Alarm.js </font>
</div>

1. **Material Top Tab Navigator**

   - Pages/AlarmPage/Notification.js
   - Pages/AlarmPage/Message.js

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 16. Notification.js </font>
</div>

1. **공지사항 데이터 불러오기**

   ```javascript
   const unsubscribe = firebase
     .firestore()
     .collection("notification")
     .orderBy("createdAt", "desc")
     .onSnapshot((querySnapshot) => {
       if (querySnapshot.size) {
         const notices = querySnapshot.docs.map((docSnapshot) => {
           return {
             ...docSnapshot.data(),
           };
         });
         setData(notices);
       } else {
         console.log("No such document!");
       }
     });
   ```

   - 최근순으로 정렬

   <br>

2. **공지사항 링크 연결**

   ```javascript
   const noticeClick = async (item) => {
     Linking.canOpenURL(item.url).then((supported) => {
       if (supported) {
         Linking.openURL(item.url);
       } else {
         Linking.openURL(
           "https://www.ajou.ac.kr/oia/notice/notice.do?mode=list&srCategoryId=108&srSearchKey=&srSearchVal="
         );
       }
     });
   ```

   <br>

3. **공지사항 목록 보여주기**

   ```javascript
   return (
     <View style={style.container}>
       <FlatList
         data={data}
         renderItem={renderItem}
         keyExtractor={(item) => item.id.toString()}
         contentContainerStyle={style.list}
       />
     </View>
   );
   ```

   <br>

   ```javascript
   const renderItem = ({ item }) => {
     const isRead = item.isRead;

     return (
       <TouchableOpacity
         style={[style.box, isRead ? style.boxRead : style.boxUnRead]}
         onPress={() => noticeClick(item)}
       >
         <View style={{ flex: 1, flexDirection: "row" }}>
           <Text style={style.title}>{item.title}</Text>
           <Text style={style.time}>{calculateTime(item.createdAt)}</Text>
         </View>
         <Text style={style.content}>{item.content}</Text>
       </TouchableOpacity>
     );
   };
   ```

   - `<FlatList>` 태그와 `renderItem()` function을 이용한다.
   - key 값은 반드시 _문자열_ 이어야 한다.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 17. Message.js </font>
</div>

1. **Stack Navigator**

   - Pages/AlarmPage/ChatList.js
   - Pages/AlarmPage/Chat.js

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 18. ChatList.js </font>
</div>

1. **채팅 목록 가져오기**

   ```javascript
   const unsubscribe = firebase
     .firestore()
     .collection("chat")
     .orderBy("latestMessage.createdAt", "desc")
     .onSnapshot((snapshot) => {
       const threads = [];
       snapshot.docs.map((docSnapshot) => {
         if (
           docSnapshot.data().user.email == user.email ||
           docSnapshot.data().target.email == user.email
         ) {
           let thread = {
             _id: docSnapshot.data().target.email,
             ...docSnapshot.data(),
           };
           threads.push(thread);
         }
       });

       setThreads(threads);
       setReRendering(isReRendering + 1);
     });
   ```

   - 최근순으로 정렬
   - 내가 대화를 시작한 채팅방 / 다른 사람이 나와의 대화를 시작한 채팅방을 보여준다.
   - DOM 업데이트를 위해 `setReRendering(isReRendering + 1)`을 실행한다.
   - thread의 \_id는 target.email

   <br>

2. **채팅방으로 이동**

   ```javascript
   const moveToChat = (item) => {
     navigation.navigate("Chat", { thread: item, user: user });
   };
   ```

   - `<FlatList>`를 사용해서 채팅 목록을 보여주기 때문에 `renderItem()`의 item을 thread에 담아 화면을 이동한다.

    <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 19. Chat.js </font>
</div>

1. **채팅 데이터 가져오기**

   ```javascript
   const unsubscribe = firebase
     .firestore()
     .collection("chat")
     .doc(thread._id)
     .collection("messages")
     .orderBy("createdAt", "desc")
     .onSnapshot((snapshot) => {
       const messages = snapshot.docs.map((docSnapshot) => {
         const data = {
           _id: docSnapshot.id,
           text: "",
           createdAt: new Date().getTime(),
           ...docSnapshot.data(),
         };
         if (!docSnapshot.data().system) {
           data.user = {
             ...docSnapshot.data().user,
             name: docSnapshot.data().user.fullName,
           };
         }
         return data;
       });

       setMessages(messages);
     });
   ```

2. **GiftedChat 이용**

   ```javascript
   return (
     <GiftedChat
       messages={messages}
       onSend={onSend}
       user={{
         _id: user.email,
       }}
       renderAvatar={null}
       showAvatarForEveryMessage={true}
       alwaysShowSend={true}
       renderBubble={renderBubble}
     />
   );
   ```

3. **메시지 보내기**

   ```javascript
   async function onSend(messages) {
     const text = messages[0].text;

     firebase
       .firestore()
       .collection("chat")
       .doc(thread._id)
       .collection("messages")
       .add({
         text,
         createdAt: new Date().getTime(),
         user: {
           _id: user.email,
           name: user.fullName,
         },
       });

     await firebase
       .firestore()
       .collection("chat")
       .doc(thread._id)
       .set(
         {
           latestMessage: {
             text,
             createdAt: new Date().getTime(),
           },
         },
         { merge: true }
       );
   }
   ```

   매개변수로 받는 messages[0]의 text가 보내는 메시지이다.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 20. User.js </font>
</div>

1. **Storage에서 프로필 이미지 가져오기**

   ```javascript
   usersRef.get().then((doc) => {
     const getuser = doc.data();
     if (getuser.picture) {
       setPicture(true);
       const storageRef = firebase.storage().ref(`${user.email}`);
       storageRef
         .getDownloadURL()
         .then((url) => {
           setUrl(url);
         })
         .catch((error) => {
           console.error("Error updating document: ", error);
         });
     }
   });
   ```

2. **Storage에 프로필 이미지 올리기**

   ```javascript
   const uploadImageToStorage = async (path, imageName) => {
     const response = await fetch(path);
     const blob = await response.blob();
     const ref = firebase.storage().ref().child(imageName);
     return ref.put(blob);
   };
   ```

3. **이름을 익명으로 바꾸기**

4. **이름 바꾸기**

5. **프로필 이미지 초기화**

   ```javascript
   onPress: () => {
            console.log("Yes");
            setPicture(false);
            setUrl("");
            const storageRef = firebase.storage().ref(`${user.email}`);
            storageRef
              .delete()
              .then(() => {
                console.log("Your profile has been reset");
              })
              .catch((error) => {
                console.error("Error updating document: ", error);
              });

            usersRef
              .set({ picture: false, url: "" }, { merge: true })
              .then(() => {
                console.log("Document successfully updated!");
                setReRendering(isReRendering + 1);
              })
              .catch((error) => {
                console.error("Error updating document: ", error);
              });
          },
   ```

   - 로컬 변수 `profile`, `url` 초기화
   - Storage 데이터 초기화
   - Firestore DB 초기화

6. **로그아웃**

   ```javascript
   firebase
     .auth()
     .signOut()
     .then(() => {
       console.log("Sign-out successful");
       Update.reloadAsync();
     })
     .catch((error) => {
       console.log("Error: ", error);
     });
   ```

   앱 재실행
