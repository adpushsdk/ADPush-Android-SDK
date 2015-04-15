# AfterPush Android SDK v1.0


##Instructions : 

**1) Implementation via JAR file**
  - Download AfterPushSDK_v1.0
  - Include in your project libs folder
  - Add AfterPushSDK_v1.0 as external JAR file
  - Include **Google Play Services library in build path as well**
  - In your project MainActivity class, override onStart() method
  - Instantiate AfterPush with your activity context as a parameter : 
  
    ```java
    AfterPush afterPush = new AfterPush(MainActivity.this);
    ```
  - In your AndroidManifest.xml, copy the following codes [There are 2 parts]:  
  
  **Part 1**
  
    ```xml
    <!-- BEGIN AFTERPUSH PERMISSION -->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

    <permission
        android:name="your.app.packagename.permission.C2D_MESSAGE"
        android:protectionLevel="signature" />

    <uses-permission android:name="your.app.packagename.permission.C2D_MESSAGE" />
    <!-- END AFTERPUSH PERMISSION -->
    ```
    
    **Part 2**
    ```xml
    <!-- BEGIN AFTERPUSH ACTIVITY & SERVICES DECLARATION -->
      <meta-data
          android:name="com.google.android.gms.version"
          android:value="@integer/google_play_services_version" />

        <receiver
            android:name="mvillage.afterpush.process.MyGCMBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND" >
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />

                <category android:name="com.example.testnoti" />
            </intent-filter>
        </receiver>

        <service android:name="mvillage.afterpush.process.MyGCMIntentService" />
        <service android:name="mvillage.afterpush.process.GCMRegister" />
    <!-- END AFTERPUSH ACTIVITY & SERVICES DECLARATION -->
    ```
    
  - That's it, you are ready to push notifications to your app users now! 
