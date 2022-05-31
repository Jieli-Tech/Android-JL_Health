# Android-JL_Health
[中文](https://github.com/Jieli-Tech/Android-JL_Health/blob/main/README.md)|EN

This repository is the open source repository of JieLi health SDK for Android, officially launched by JieLi, online and offline support synchronous release.

The current version: `V1.6.7`



##  Getting Started

Welcome to JieLi health SDK(Android) open source project. Before starting the development project, <strong style="color:#de2233">please read [the SDK development documentation](https://doc.zh-jieli.com/Apps/Android/health/zh-cn/master/index.html) in detail to get a general idea of the structure and function of the SDK</strong>, and you can use the documentation for development access.





## Introduction to development materials

```tex
├ apk   --- test APK
   ├- app  --- WearLink test APK, Download it from the app store
   └- tool --- Watch test tool, Used to test the watch function
├ code  --- Demo source code
   ├- app  --- the source code of WearLink
   └- tool --- the source code of Watch test tool
├ doc   --- Development of the document
   └- ReadMe --- Online document link
├ libs  --- Core library
   ├- jldecryption_v0.1-release           --- Encryption
   ├- jl_bluetooth_connect_V0.2.0-release --- Bluetooth connection
   ├- jl_health_http_V1.0.0-release       --- Health server
   ├- jl_rcsp_V0.2.3-release              --- Basic protocol
   ├- JL_Watch_V1.6.7-release             --- Health feature
   ├- jl_bt_ota_V1.6.0_release            --- OTA feature
   └- BmpConvert_V0.0.4-release           --- Image conversion
```





## Function Implementation

### 1. WearLink

* Implementation of Bluetooth connection, see `com.jieli.healthaide.tool.bluetooth.BluetoothHelper`
* Implementation of Health SDK, see `com.jieli.healthaide.tool.watch.WatchManager`
* Implementation of OTA feature, see `com.jieli.healthaide.tool.upgrade.OTAManager`



**You can refer to the unit test sample of `the Test package` for testing capabilities**



### 2. Watch test tool

* Implementation of Bluetooth connection, see `com.jieli.watchtesttool.tool.bluetooth.BluetoothHelper`
* Implementation of Health SDK, see `com.jieli.watchtesttool.tool.watch.WatchManager`
* Implementation of OTA feature, see `com.jieli.watchtesttool.tool.upgrade.OTAManager`
* Image conversion function, see  `com.jieli.watchtesttool.BmpConvertDemo` of the Test package
* Custom command function, see `com.jieli.watchtesttool.CustomCommandDemo` of the Test package





## Debugging and testing

1. Open the file output function of JL_Log
	```java
	JL_Log.setTagPrefix("health"); //set log flag
	//log config
	//context    --- context, Advice is getApplicationContext()
	//islog      --- Whether to print the output? It is recommended to enable the output during development and disable the output during publication
	//isSaveFile --- Whether to save the log file? You are advised to open it during development and close it during publishing
	JL_Log.configureLog(context, true, true);
	```
	
	
	
2. Logcat file

      1. file format
          format：[tag_prefix]_log_[timestamp].txt
          Example：health_log_20220113093020.432.txt ==> logcat file of the health SDK, create time：2022/01/13 09:30:20 

      2. store path
         location: /Android/data/[package name]/files/logcat/

         * WearLink
           eg：Android/data/com.jieli.healthaide/files/logcat/

         * Watch test tool
           eg：Android/data/com.jieli.watchtesttool/files/logcat/

3. Correct handling procedures when exceptions occur
   1.  description of problem symptoms (necessary)
   2. Provide the log file closest to the timestamp (necessary)
   3. Provide screenshots or videos



## open source community

1.  Users can ask questions in issues, our developers will provide timely reply

