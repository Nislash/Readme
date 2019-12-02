# **README**

( last reviewed on 04/09/2019 )

current Camera LiFi SDK version : **v1.0.0**

## **Introduction**

This is the documentation of the Camera LiFi SDK for Android.

### **To import .aar library file**

* Place the .aar file into your project folder at app/libs
* Edit your app level gradle.build file to include those configuration:

```java
repositories {
    flatDir {
        dirs 'libs'
    }
}

dependencies {
    implementation(name: 'camera-lifisdk-android-v1.0.0', ext: 'aar')
}
```

### **To use the SDK module with your own project**

Use the SDK as follows:

1. Add static permission request to access camera in AndroidManifest file.

    ```xml
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-feature android:name="android.hardware.camera" />
    <uses-feature android:name="android.hardware.camera.autofocus" />
    ```

    **ATTENTION : please also include run-time permission request**

    Refer to android developer site or our SdkDemo project code as an example

2. Add id to your layout xml file where you want to put camera view

    ```xml
    android:id="@+id/main_layout"
    ```

3. Declare an instance of LiFiSdkManager in your activity where you'd like to implement the SDK:

    ```java
    private LiFiSdkManager liFiSdkManager;
    ```

4. Initialize LiFiSdkManager with Camera_Lib_Version:

    ```java
    liFiSdkManager = new LiFiSdkManager(this, new LiFiCallback() {
        @Override
        public void onLiFiPositionUpdate(String lamp) {

            /* Add your actions here.
                *  lamp will contain the tag (eg. 10101010) if decoding was successful.
                */

            textView.setText(lamp);
        }

        @Override
        public void onLiFiErrorUpdate(String errorMessage) {
            /* Add your actions here.
                *  If there was an error, lamp could contain error related text like "No lamp detected" or "Weak signal", etc.
                */
            textView.setText(errorMessage);
        }
    });
    ```

5. Choose which side of camera you want to use and provide the layout id that you created to start camera :

    ```java
    liFiSdkManager.start(R.id.main_layout, LiFiSdkManager.FRONT_CAMERA);
    ```

6. Do not forget to stop your liFiSdkManager for a proper full life cycle:

    ```java
    if (liFiSdkManager != null && liFiSdkManager.isStarted()) {
        liFiSdkManager.stop();
        liFiSdkManager = null;
    }
    ```

### **SDK demo project**

Refer to attached SDK demo project as an example. Concrete demonstration of SDK implementation is provided.

Bonus: lors que nous avons reçu le tag, nous déclenchons un web view avec le lien :https://www.edf.fr/edf/accueil-magazine/le-lifi-accedez-a-internet-par-la-lumiere

