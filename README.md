# What is this

This is a documents and tools for improving cordova `config-file` and `edit-config` functions.
The current cordova (9.0) has an issue, like https://github.com/apache/cordova/issues/95 .
This is very difficult problem. 
Because each `config-file` or `edit-config` in `config.xml` or`plugin.xml` modifies an application setting file, e.g. `AndroidManifest.xml` or `-Info.plist`.
Inevitably they conflicts each other.

It makes this issue more difficult that the user can add/remove plugin and edit `config.xml` anytime.
The cordova should detect which `config-file` or `edit-config` is changed and apply the modification to an appropriate application setting file.


The cordova (more details, `cordova-common`) manages each plugin's settings (i.e. `config-file` or `edit-config`) and project's `config.xml` settings
by using `munge` json data structure. But it is not enough to resolve confliction even if it looks simple for human.


# The typical situation for this issue

See https://github.com/apache/cordova/issues/95#issuecomment-508971041

For example

```
$ cordova create sampleProject
$ cd sampleProject
$ cordova platform add android
$ cordova plugin add cordova-plugin-camera
```

Then we found the platforms/android/app/src/main/AndroidManifest.xml as


```
<!-- list1 -->
    <application android:hardwareAccelerated="true" android:icon="@mipmap/ic_launcher" android:label="@string/app_name" android:supportsRtl="true">
        <activity android:configChanges="orientation|keyboardHidden|keyboard|screenSize|locale" android:label="@string/activity_name" android:launchMode="singleTop" android:name="MainActivity" android:theme="@android:style/Theme.DeviceDefault.NoActionBar" android:windowSoftInputMode="adjustResize">
            <intent-filter android:label="@string/launcher_name">
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <provider android:authorities="${applicationId}.provider" android:exported="false" android:grantUriPermissions="true" android:name="org.apache.cordova.camera.FileProvider">
            <meta-data android:name="android.support.FILE_PROVIDER_PATHS" android:resource="@xml/camera_provider_paths" />
        </provider>
    </application>
```

where the `provider` directive is added by camera plugin.

Then I edit config.xml to add

```
<!-- list2 -->
        <edit-config file="AndroidManifest.xml" target="/manifest/application" mode="merge">
            <application android:usesCleartextTraffic="true" />
        </edit-config>
```

in `<platform name="android">` directive. Then do cordova prepare again.

We expect this to add `android:usesCleartextTraffic="true"` attribute in application directive.

However, the resulting AndroidManifest.xml is

```
<!-- list3 -->
    <application android:hardwareAccelerated="true" android:icon="@mipmap/ic_launcher" android:label="@string/app_name" android:supportsRtl="true" android:usesCleartextTraffic="true">
        <activity android:configChanges="orientation|keyboardHidden|keyboard|screenSize|locale" android:label="@string/activity_name" android:launchMode="singleTop" android:name="MainActivity" android:theme="@android:style/Theme.DeviceDefault.NoActionBar" android:windowSoftInputMode="adjustResize">
            <intent-filter android:label="@string/launcher_name">
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
```

We found

- The android:usesCleartextTraffic="true" attribute in application directive is added as we expect.
- The provider directive in application disappears. This is contrary to our expectation.


# The basic plugins

[plugins data](plugins.md)
