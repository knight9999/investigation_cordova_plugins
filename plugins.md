# Plugins

## cordova-plugin-battery-status

 No `config-file` and `edit-config` for each platform settings.


## cordova-plugin-camera

### Android

```
        <config-file target="AndroidManifest.xml" parent="/*">
            <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        </config-file>
        <config-file target="AndroidManifest.xml" parent="application">
          <provider
              android:name="org.apache.cordova.camera.FileProvider"
              android:authorities="${applicationId}.provider"
              android:exported="false"
              android:grantUriPermissions="true" >
              <meta-data
                  android:name="android.support.FILE_PROVIDER_PATHS"
                  android:resource="@xml/camera_provider_paths"/>
          </provider>
        </config-file>
```

## cordova-plugin-media-capture

### Android

```
        <config-file target="AndroidManifest.xml" parent="/*">
            <uses-permission android:name="android.permission.RECORD_AUDIO" />
            <uses-permission android:name="android.permission.RECORD_VIDEO"/>
            <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
            <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        </config-file>
```

