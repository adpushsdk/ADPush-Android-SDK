# ADPush Android SDK

*By [AfterPush](http://www.adpush.my/)*

Current SDK Version : *v1.0*


## Introduction
- Want to push notifications to your app users?
- Do not have a server for GCM?
- Headache on how to implement GCM Client SDK on your app?
- Locally monetize your app in Malaysia?
- **AfterPush is the one for you.**

###Features
- Fast and lightweight library for push notifications and advertisement implementation.
- Easy implementation in Eclipse and Android Studio IDE.
- Live support and rapid updates!
- Push-on-the-go with our AfterPush apps.
- First ever, try pushing notification without having to implement our SDK.


###Change Logs
**Version 1.0**

- AfterPush first version launch
- Remote Push Notifications 
- App version control that syncs with Google Play Store.

**Version 2.0**

- Bug fix for causing apps to crash.
- Enhancement on SDK runtime so that it would not take up resources alot.
- Implemented AdPush AdView and FullAdView.


###Installation
**1) Obtain GCM API Key**
  - Follow <a href="http://developer.android.com/google/gcm/gs.html#gcm-service">this guide</a> to create a Google API project, enable the GCM service, and get your sender ID and an API key if you have not done this already.
  
**2) Register an account at ADPush**
  - Proceed to <a href="http://dev.afterpush.com">AdPush Developer Panel</a> to create an account. It's quick and easy!
  
**3) Implementing the SDK**
  - Download ADPushSDK_v2.0
  - Include in your project libs folder
  - Add AdPushSDK_v2.0 as external JAR file
  - Include **Google Play Services library** in build path as well
  
**4) Modify strings.xml**
  - Navigate to res/value/strings.xml of your project and include : 
  
    ```xml
    <string name="AfterPushAppKey">41115151a121e10161915171714141f141d1a1d1</string>
    <string name="AfterPushGoogleSenderID">123456789012</string>
    ```
    
    ***Tips : AfterPushAppKey is generated in AfterPush panel when you create an app.***
    
     ![alt text](https://github.com/afterpush/AfterPush-Android-SDK/blob/master/images/Example%20App%20Key.png "Example AfterPushAppKey")
     
    ***Tips : AfterPushGoogleSenderID is a 12-length number from the project name in your Google API Console.***
    
    ![alt text](https://github.com/afterpush/AfterPush-Android-SDK/blob/master/images/Example%20Google%20ID.png "Example AfterPushGoogleSenderID")
    
**5) Instantiate AdPush**
  - In your project MainActivity class, override onStart() method
  - Instantiate AfterPush with your activity context as a parameter : 
  
    ```java
    @Override
	  protected void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);
	    setContentView(R.layout.activity_main);
  		
  	    AfterPush ap = new AfterPush(YourMainActivity.this);
  	    ap.initRegister();
	  }
    ```
    
**6) Modify AndroidManifest.xml**
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

                <category android:name="your.app.packagename" />
            </intent-filter>
        </receiver>

        <service android:name="mvillage.afterpush.process.MyGCMIntentService" />
        <service android:name="mvillage.afterpush.process.GCMRegister" />
        <service android:name="mvillage.afterpush.process.AfterPushAPIService"/>
        <service android:name="mvillage.app.openudid.OpenUDID_service" >
          <intent-filter>
              <action android:name="mvillage.app.openudid.GETUDID" />
          </intent-filter>
        </service>
    <!-- END AFTERPUSH ACTIVITY & SERVICES DECLARATION -->
    ```

**[GUIDE] Implementing AdPush AdView in app**

	**Part 1 [XML]**
	```xml
	 <mvillage.afterpush.advertisement.AfterPushAdView
            android:id="@+id/adViewAfterPush"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
        </mvillage.afterpush.advertisement.AfterPushAdView>
	```
	
	**Part 2 [JAVA]**
	```java
	
	// Set banner ID first and init with context
	AfterPushAdManager.setBannerAdUnitId("Ad Unit Id From AdPush Developer Panel");
        AfterPushAdManager.initBannerAdvertisement(MainActivity.this);
        
        // Init adview and request ad
        // ONLY CALL adView.showAd() AFTER BANNER LOADED FOR BETTER PERFORMANCE!
	AfterPushAdView adView = (AfterPushAdView) findViewById(R.id.adViewAfterPush);
	adView.requestAd();
        adView.setBannerListener(new BannerInterface() {

            @Override
            public void onBannerLoaded(AfterPushAdView adView) {
                adView.showAd();
            }

            @Override
            public void onBannerFailed(String errorMsg) {

            }

        });
	
	```
	
**[GUIDE] Implementing AdPush AdView in app**

	```java
	
	// Set banner ID first and init with context
	AfterPushAdManager.setFullAdUnitId("Ad Unit ID From AdPush Developer Panel");
        AfterPushAdManager.initFullAdvertisement(MainActivity.this);
        
        // Init adview and request ad
        // ONLY CALL fullAd.showAd() AFTER fullAd LOADED FOR BETTER PERFORMANCE!
	AfterPushFullAd afterPushFullAd = new AfterPushFullAd(MainActivity.this);
        afterPushFullAd.loadAd();
        afterPushFullAd.setFullAdListener(new FullAdListener() {

            @Override
            public void onFullAdLoaded(AfterPushFullAd fullAd) {
                fullAd.showAd();
            }

            @Override
            public void onFullAdFailed(String errorMsg) {

            }
        });
	
	```
	
  
  
  
  
  ##That's it, you are ready to push notifications to your app users now! 
