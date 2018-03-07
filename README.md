# SplashActivity
Splash Activity screen - right way in Kotlin.
Previously, Google advised against using Splash screen in Android apps by saying that it was useless. But later when the Material design concepts were published, they changed their stand and promoted the use of Splash Screen in a proper way.

    Because launching your app while displaying a blank canvas increases its perceived loading time, consider using a placeholder UI or a branded launch screen

    – MaterialDoc

Google even has a guideline on implementing Splash screen based on the Material Design principles. Check it out here. They have some neat information and examples on different types of Splash screens and their implementations.

Btw, Google calls Splash Screen as Launch screen.
Implementation

As I said in the introduction, whenever a user starts an app, there will be a delay based on the app’s functionality called as cold launch. The Android framework will show a blank white screen during this cold start period.

Previously, developers used to display their logo for a set period of time, say maybe 2 seconds, wasting the users precious time. Don’t ever do that.

Google now recommends you to display the Splash screen only during the cold launch period of the app which is less than 2 seconds(mostly) and no more. In other words, the amount of time the user spends looking at the Splash screen is exactly the amount of time the app takes to load its home screen.
New Project

Create a new project, as usual, nothing different here. Once the project is created and synched, create a new activity with the name SplashActivity and uncheck “Generate Layout File” option. Click Finish.

 

splash_activity

You may be wondering why we are not generating a layout xml file. That is because we will be working with themes. Save this logo in the drawable folder.

logo

Open colors.xml under res/values/colors.xml and paste these colors.

<?xml version="1.0" encoding="utf-8"?>
<resources>
<!--<color name="colorPrimary">#3F51B5</color>-->
<color name="colorPrimary">#212121</color>
<color name="colorPrimaryDark">#212121</color>
<color name="colorAccent">#FF4081</color>
</resources>

Create a new drawable file under res/drawable with the name splash_bg.xml.

<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
<item android:drawable="@color/colorPrimary" />
<item
android:drawable="@drawable/logo"
android:gravity="center" />
</layer-list>

In SplashActivity, add these code,

package com.androidhoney.splashscreen;
import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
public class SplashActivity extends AppCompatActivity {
@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
startActivity(new Intent(this, MainActivity.class));
finish();
}
}

package com.androidhoney.splashscreen
import android.content.Intent
import android.os.Bundle
import android.support.v7.app.AppCompatActivity
class SplashActivity : AppCompatActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
startActivity(Intent(this, MainActivity::class.java))
finish()
}
}

Now Declare the SplashActivity as the Launcher Activity for the app and apply the SplashScreen theme to it.

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="com.androidhoney.splashscreen">
<application
android:allowBackup="true"
android:icon="@mipmap/ic_launcher"
android:label="@string/app_name"
android:roundIcon="@mipmap/ic_launcher_round"
android:supportsRtl="true"
android:theme="@style/AppTheme">
<activity android:name=".MainActivity"/>
<!--Declare SplashActivity as the Launcher activity-->
<!--and apply the SplashScreen theme to it.-->
<activity android:name=".SplashActivity"
android:theme="@style/SplashScreen">
<intent-filter>
<action android:name="android.intent.action.MAIN" />
<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>
</application>
</manifest>

Edit and apply the SplashScreen theme to /res/values/styles.xml

<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>
    <!-- Splash Screen theme. -->
    <style name="SplashScreen" parent="Theme.AppCompat.NoActionBar">
        <item name="android:windowBackground">@drawable/splash_bg</item>
    </style>
</resources>


Run the app and you will see the Splash screen the correct way.
