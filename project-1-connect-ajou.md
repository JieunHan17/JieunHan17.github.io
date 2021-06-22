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
    └── Pages/<br>
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
    │     ├── CourseItem.js<br>
    │     ├── PickCourses.js<br>
    │     └── Timetable.js<br>
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

    <br>

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
