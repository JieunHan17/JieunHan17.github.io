---
layout: page
title: Connect Ajou
---

[<img src="/assets/images/connect-ajou/1.png">](https://github.com/amelia9981/Connect_Ajou)

<font style="background-color: #D7DDE2; color: #1E3D6B"> ðGo to GitHub by clicking the image above!ð</font>

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
    âââ App.js<br>
    âââ MainScreenF.js<br>
    âââ Utilities/<br>
    â âââ Firebase.js<br>
    â âââ UserPermissions.js<br>
    âââ Pages/<br>
    â   âââ AlarmPage/<br>
    â   â âââ Chat.js<br>
    â   â âââ ChatList.js<br>
    â   â âââ Message.js<br>
    â   â âââ Notification.js<br>
    â   âââ CommunityPage/<br>
    â   â âââ subCommunityPage/<br>
    â   â â âââ addWriting.js<br>
    â   â â âââ searchWriting.js<br>
    â   â â âââ seeWriting.js<br>
    â   â â âââ showList.js<br>
    â   â âââ FindFriend.js<br>
    â   â âââ GetInfo.js<br>
    â   â âââ schoolLife.js<br>
    â   â âââ showAll.js<br>
    â   âââ HomeTab/<br>
    â   â âââ AddFavorites.js<br>
    â   â âââ HomeTabMain.js<br>
    â   âââ TimetablePage/<br>
    â       âââ CourseItem.js<br>
    â       âââ PickCourses.js<br>
    â       âââ Timetable.js<br>
    âââ Alarm.js<br>
    âââ CommunityMain.js<br>
    âââ handleCommunity.js<br>
    âââ handleHome.js<br>
    âââ HomeTabF.js<br>
    âââ Login.js<br>
    âââ Registration.js<br>
    âââ TimetableTab.js<br>
    âââ User.js<br>
</div>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 1. App.js </font>
</div>

1. **ëë°ì´ì¤ì ë°ë¼ í°í¸ ì¬ì´ì¦ê° ë³ëëì§ ìëë¡ ì¤ì **

   ```javascript
   Text.defaultProps = Text.defaultProps || {};
   Text.defaultProps.allowFontScaling = false;
   ```

   <br>

2. **í°í¸ ë¡ë & í¸ì ìëì ë¤ ë¹ëê¸°ë¡ ëì**

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

   ì¤ì  ëë°ì´ì¤ì¸ì§ íì¸ -> íì¬ ê¶íì´ ìëì§ íì¸ -> ìì¼ë©´ ê¶í ìì²­ -> ìµì¢ ê¶í íì¸

    <br>

3. **ì¤í ë¡ì§**

   í°í¸ê° ë¤ ë¡ëëìê³ , ì ì  ì ë³´ ë¡ë©ì´ ëëë©´ ì ì  ì ë³´ ì²´í¬

   -> ì ì ê° ìì¼ë©´ MainScreenF.jsë¡ ë°ë¡ ëì´ê° / ì ì ê° ìì¼ë©´ Registration.jsë¡ ëì´ê°

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 2. Registration.js </font>
</div>

1. **ì´ë©ì¼ê³¼ ë¹ë°ë²í¸ë¡ ê°ì**

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

2. **ì ì  ë°ì´í° ìì±**

   > ì´ë©ì¼, ì±ëª, íë¡í ì´ë¯¸ì§ ì¬ë¶, íë¡í ì´ë¯¸ì§ ì£¼ì, ëì ìê°ëª©ë¡

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
   > ì»¤ë®¤ëí° ì¦ê²¨ì°¾ê¸°

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

2. **ì ì  ë°ì´í° ë¶ë¬ì¤ê¸°**

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

3. **ìê°ëª©ë¡ ë°ì´í° ë¶ë¬ì¤ê¸°**

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

   ëì ìê°ëª©ë¡ì í´ë¹íë ê³¼ëª© ì ë³´ ê°ì ¸ì¤ê¸° -> ê³¼ëª© ì¤ì¼ì¥´ íì¸ -> í´ë¹íë ìê°í ë°°ì´ì ë°°ê²½ì & ê³¼ëª©ëª ì§ì 

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

2. **ì¦ê²¨ì°¾ê¸°ì ì¶ê°ë ì»¤ë®¤ëí° ë°ì´í° ë¶ë¬ì¤ê¸°**

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

1. **ì¦ê²¨ì°¾ê¸°ì ê´ë ¨ë ë°ì´í° ë¶ë¬ì¤ê¸°**

   - ì¦ê²¨ì°¾ê¸°ì ì¶ê°ë ì»¤ë®¤ëí° ë°ì´í°: selectedItems
   - ì¦ê²¨ì°¾ê¸°ì ì¶ê°ë ì»¤ë®¤ëí° ë°°ì´: selectedItemsArray
   - ëª¨ë  ì»¤ë®¤ëí°: allItems

   <br>

2. **ì¦ê²¨ì°¾ê¸°ì ì¶ê°í  ì»¤ë®¤ëí° ì í**

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

   ì´ë¯¸ ì²´í¬ëì´ ìë¤ë©´ í´ì  / ì²´í¬íì§ ììë¤ë©´ ì²´í¬

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

3. **ì¦ê²¨ì°¾ê¸°ì ì¶ê°**

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

   ì¶ê°í ìê°ê³¼ í¨ê» DBì ìë¡ë

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

2. **ì»¤ë®¤ëí° ë¤ë¹ê²ì´ì í¤ë ì´ë¦ ì¤ì **

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
   `getFocusedRouteNameFromRoute(route)`ë íì¬ íì±íëì´ ìë routeì ì´ë¦ì ë°í

   -> ë§ì½ ì´ ê°ì´ nullì´ê±°ë undefinedì´ë©´ ì¤ë¥¸ìª½ ê° ë°í

   <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 8. showList.js </font>
</div>

1. **ê¸ ëª©ë¡ ê°ì ¸ì¤ê¸°**

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
   ì¤ìê°ì¼ë¡ ê°ì ¸ì¤ê¸° ìí´ `onSnapshot` ì¬ì©<br>

2. **ê¸ ëª©ë¡ ë³´ì¬ì£¼ê¸°**

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
   ë°ì´í°ë¥¼ mapping í´ì ì¤í¬ë¡¤ë·°ìì ë³´ì¬ì¤<br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 9. addWriting.js </font>
</div>

1. **í¤ë ì¤ì **

   `useLayoutEffect`: ë ëë§ í íë©´ì´ ìë°ì´í¸ ëê¸° ì ì ëê¸°ì ì¼ë¡ ì¤í(cf. `useEffect`ë ë¹ëê¸°ì ì¼ë¡ ì¤í)
   <br>

2. **ê¸ ìì±**

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

1. **ê²ì ë°ì´í° ê°ì ¸ì¤ê¸°**

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

2. **ê²ì ë²í¼ ì´ë²¤í¸**

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
   `isSearch` ê°ì´ true ì´ë©´ ê²ì ê²°ê³¼ê° ë³´ì¬ì§ë¤.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 11. seeWriting.js </font>
</div>

1. **ì¢ìì í´ë¦­**

2. **ëê¸ ìì±**

3. **ê¸ ëª©ë¡ ê°ì ¸ì¤ê¸°**

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
   ê¸ì ì­ì íê³  ë íìë `doc.data()`ê° undefinedê° ëë¯ë¡ ifë¬¸ì ì¶ê°íìë¤.

   <br>

4. **ê¸ ìì **

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

   ê¸ ì ëª©ì´ ë°ëë¯ë¡ ìë ì¡´ì¬íë docì ì§ìì£¼ê³  ìë¡ì´ docì ìì±íì¬ì¼ íë¤.<br>
   `<Modal>`ìì `<Modal>`ì ë ë£ì´ì¤ì ê¸ì ìì í  ëë§ íìì°½ì´ ë³´ì´ëë¡ íìë¤.

   <br>

5. **ê¸/ëê¸ ì­ì **

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

   ëê¸ ì­ì  ì, [Firebase ë°°ì´ ìì ìë°ì´í¸ ì°¸ê³ ](https://firebase.google.com/docs/firestore/manage-data/add-data#update_elements_in_an_array)

   <br>

6. **ê¸ ìì±ìì ì±í ìì**

   - ê¸ ìì±ìê° ë³¸ì¸ì´ ìë ê²½ì°, ê¸°ì¡´ ì±íë°©ì¼ë¡ ì´ë(cf. ë³¸ì¸ì¼ ê²½ì°ìë ë§ì´ íì´ì§ë¡ ì´ë)
   - ë§ì½ ê¸°ì¡´ ì±íë°©ì´ ì¡´ì¬íì§ ìëë¤ë©´ ìë¡ì´ ì±íë°© ìì±

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

1.  **ì ì²´ ê°ì ëª©ë¡ ê°ì ¸ì¤ê¸°**

    `setCourses(array)`

    <br>

2.  **ë´ê° ìê°íë ê°ì ëª©ë¡ ê°ì ¸ì¤ê¸°**

    `setMyCourses(getUser.myCourses)`

    <br>

3.  **ê°ì ì­ì **

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
     `filter()` ë©ìëë ì£¼ì´ì§ í¨ìì íì¤í¸ë¥¼ íµê³¼íë ëª¨ë  ììë¥¼ ëª¨ì ìë¡ì´ ë°°ì´ë¡ ë°ííë¤.

     <br>

4.  **ìê°í í ìì±**

    `<View>` íê·¸ë¡ íì´ë¸ì ë§ë¤ìë¤.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 14. PickCourses.js </font>
</div>

1.  **ì ì²´ ê°ì ëª©ë¡ ê°ì ¸ì¤ê¸°**

    `setCourses(array)`

    <br>

2.  **ë´ê° ìê°íë ê°ì ëª©ë¡ ê°ì ¸ì¤ê¸°**

    `setMyCourses(getUser.myCourses)`

    <br>

3.  **ê°ì ì¶ê°**

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

    - myCoursesìë ê³¼ëª© ì½ëë¡ ì ì¥ëë¤.
    - ìê°ì´ ì¤ë³µëë©´ ì¶ê°ê° ëì§ ìëë¤.

    <br>

4.  **ê°ì ëª©ë¡ ë³´ì¬ì£¼ê¸°**

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
    `courses.map()`ì ì¬ì©í´ì CourseItem.jsì functionì ë³´ì¬ì¤ë¤.

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

1. **ê³µì§ì¬í­ ë°ì´í° ë¶ë¬ì¤ê¸°**

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

   - ìµê·¼ìì¼ë¡ ì ë ¬

   <br>

2. **ê³µì§ì¬í­ ë§í¬ ì°ê²°**

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

3. **ê³µì§ì¬í­ ëª©ë¡ ë³´ì¬ì£¼ê¸°**

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

   - `<FlatList>` íê·¸ì `renderItem()` functionì ì´ì©íë¤.
   - key ê°ì ë°ëì _ë¬¸ìì´_ ì´ì´ì¼ íë¤.

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

1. **ì±í ëª©ë¡ ê°ì ¸ì¤ê¸°**

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

   - ìµê·¼ìì¼ë¡ ì ë ¬
   - ë´ê° ëíë¥¼ ììí ì±íë°© / ë¤ë¥¸ ì¬ëì´ ëìì ëíë¥¼ ììí ì±íë°©ì ë³´ì¬ì¤ë¤.
   - DOM ìë°ì´í¸ë¥¼ ìí´ `setReRendering(isReRendering + 1)`ì ì¤ííë¤.
   - threadì \_idë target.email

   <br>

2. **ì±íë°©ì¼ë¡ ì´ë**

   ```javascript
   const moveToChat = (item) => {
     navigation.navigate("Chat", { thread: item, user: user });
   };
   ```

   - `<FlatList>`ë¥¼ ì¬ì©í´ì ì±í ëª©ë¡ì ë³´ì¬ì£¼ê¸° ëë¬¸ì `renderItem()`ì itemì threadì ë´ì íë©´ì ì´ëíë¤.

    <br>

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 19. Chat.js </font>
</div>

1. **ì±í ë°ì´í° ê°ì ¸ì¤ê¸°**

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

2. **GiftedChat ì´ì©**

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

3. **ë©ìì§ ë³´ë´ê¸°**

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

   ë§¤ê°ë³ìë¡ ë°ë messages[0]ì textê° ë³´ë´ë ë©ìì§ì´ë¤.

---

<div style="background-color: #5995DD; text-algin: left; color: #F6F8F8">
    <font size="5" style="background-color: #5995DD; color: #F6F8F8"> 20. User.js </font>
</div>

1. **Storageìì íë¡í ì´ë¯¸ì§ ê°ì ¸ì¤ê¸°**

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

2. **Storageì íë¡í ì´ë¯¸ì§ ì¬ë¦¬ê¸°**

   ```javascript
   const uploadImageToStorage = async (path, imageName) => {
     const response = await fetch(path);
     const blob = await response.blob();
     const ref = firebase.storage().ref().child(imageName);
     return ref.put(blob);
   };
   ```

3. **ì´ë¦ì ìµëªì¼ë¡ ë°ê¾¸ê¸°**

4. **ì´ë¦ ë°ê¾¸ê¸°**

5. **íë¡í ì´ë¯¸ì§ ì´ê¸°í**

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

   - ë¡ì»¬ ë³ì `profile`, `url` ì´ê¸°í
   - Storage ë°ì´í° ì´ê¸°í
   - Firestore DB ì´ê¸°í

6. **ë¡ê·¸ìì**

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

   ì± ì¬ì¤í
