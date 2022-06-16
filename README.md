# Android Starter

```bash 
# 数字签名
keytool  -genkeypair -alias key0 -keyalg RSA -validity 400 -keystore demo.jks
```

## release 配置

```
android {
    compileSdk 32

    defaultConfig {
        applicationId "com.payne.androidstarter"
        minSdk 21
        targetSdk 32
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    signingConfigs {
        release {
            storeFile file('../demo.jks')
            storePassword '123456'
            keyAlias 'key0'
            keyPassword '123456'
        }
    }


    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'

            signingConfig signingConfigs.release
        }
    }

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
```

## 安装app

```bash 
adb install app/build/outputs/apk/release/app-release.apk
```

## 感染app

- RatelManager_x.0-SNAPSHOT-release.apk 中感染
- ratel-engine中感染app（推荐）

```bash 
 ratel.sh --help
-,--abi <arg>             设置ABI，可以可以指定app运行在32位机器上，或者运行在64位机器上。可选值: armeabi-v7a/arm64-v8a
-c,--certificate <arg>    authorizer certificate file
-d,--debug                add debuggable flag on androidManifest.xml
-D,--decompile            create a RDP(ratel decompile project) like "apktool output project",this project
                       only contains smali files and with capability to bypass signature check with ratel
                       framework
-e,--engine <arg>         the ratel engine,now support appendDex|rebuildDex|shell
-h,--help                 print help message
-l,--log                  add log component,we can call it from apktool baksmali
-o,--output <arg>         the output apk path or output project path
-p,--hookProvider <arg>   no use , a deprecate flag,which ratel framework integrate sandhook
-s,--signature            signature apk with ratel default KeyStore
-t,--tell                 tell me the output apk file path
-w,--workdir <arg>        set a ratel working dir
-x,--extract              extract origin apk from a ratel output apks

example:  ratel.sh app-release.apk -o app-sucess.apk
```
