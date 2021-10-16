---
title: Android Studio Thread
layout: post
post-image: "https://developer.android.com/studio/images/studio-homepage-hero.jpg"
description: Android Studio에서 Thread란 무엇인가?
tags:
  - Android Studio
  - Thread
---

# Main Thread(UI Thread)

- 안드로이드 이벤트 생성 및 처리 담당
- 안드로이드에서 발생되는 여러 이벤트를 그와 관련된 위젯으로 연동시키는 역할
- 안드로이드에서 제공하는 다양한 뷰와 위젯을 표현하는 역할
- 안드로이드 시스템은 각각의 컴포넌트를 위해서 별도의 스레드를 생성하지 않음 -> _동일한 프로세스에서 동작하는 모든 컴포넌트는 **여기서** 처리_
- <font style="color: red">단점: 네트워크 접속 및 데이터베이스 쿼리와 같이 오래 걸리는 작업을 하는 동안 UI 관련된 작업은 처리되지 못함</font>

## ANR

- Application Not Responding
- 오랜 시간 UI 관련 작업이 처리되지 못할 경우 발생하는 에러
- Application이 정지됨

---

# Worker Thread(작업 스레드)

- UI 관련 작업은 여기서 처리되면 안됨 -> Worker Thread에서 UI Thread로 메시지를 전달하는 핸들러 사용/AsyncTask 필요

## 예시

<font style="color: #1E3D6B">[핸들러]</font>

```java
public void onClick(View v) {
  new Thread(new Runnable()) {
    public void run() {
      final Bitmap bitmap =
        loadImageFromNetwork("http://example.com/image.png");

        mImageView.post(new Runnable()) { //Handler
          public void run() {
            mImageView.setImageBitmap(b);
          }
        }
    }
  }
}
```

<br>

<font style="color: #1E3D6B">[AsyncTask]</font>

```java
public void onClick(View v) {
  new DownloadImageTask().execute("http://example.com/image.png");
}

private class DownloadImageTask extends AsyncTask<String, Void, Bitmap> {
  protected Bitmap doInBackground(String... urls) {
    return loadImageFromNetwork(urls[0]);
  }

  protected void onPostExecute(Bitmap result) {
    mImageView.setImageBitmap(result);
  }
}
```

- AsyncTask의 서브클래스를 생성해서 doInBackground() 콜백함수를 구현
- UI를 업데이트하기 위해서 onPostexecute()라는 메소드 구현

---
