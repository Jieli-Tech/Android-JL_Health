[tag download]:https://github.com/Jieli-Tech/Android-JL_Health/tags
[tag_badgen]:https://img.shields.io/github/v/tag/Jieli-Tech/Android-JL_Health?style=plastic&logo=android&labelColor=ffffff&color=informational&label=Tag&logoColor=blue

# Android-JL_Health  [![tag][tag_badgen]][tag download]

<div align="center">

**JieLi Health SDK (Android) - A development platform for health data and device management of JieLi Bluetooth wearable products**

[中文](./README.md) · [English](./README_en.md) · [Documentation Center](https://doc.zh-jieli.com/Apps/Android/health/en-us/master/index.html) · [SDK Release History](#eight-release-history) · [Report Issues](https://github.com/Jieli-Tech/Android-JL_Health/issues)

</div>

---

## 📋 Table of Contents

- [One: Overview](#one-overview)
- [Two: Environment Requirements](#two-environment-requirements)
- [Three: Quick Start](#three-quick-start)
- [Four: Project Structure](#four-project-structure)
- [Five: Configuration Guide](#five-configuration-guide)
- [Six: Debugging Tips](#six-debugging-tips)
- [Seven: Community and Support](#seven-community-and-support)
- [Eight: Release History](#eight-release-history)
- [Nine: License](#nine-license)

---

## One: Overview

`Android-JL_Health` is a health data and device management development platform provided by **Zhuhai JieLi Technology Co., Ltd.** ("the Company") for Bluetooth wearable products. This SDK is based on the <strong style="color:red">RCSP protocol (Remote Control System Protocol)</strong> and provides complete wearable device control functionality with rich application examples, supporting the following application scenarios:

| Application Type | Typical Products |
|---------|---------|
| **Smart Watches** | Children's watches, adult smart watches, health monitoring watches |
| **Fitness Bands** | Sports bands, sleep monitoring bands, pedometers |
| **Wearable Devices** | Bluetooth headbands, smart rings, and other wearable devices |

**Jieli Health SDK** provides a rich set of functional interfaces:

| Function           | Description                                                     |
| -------------- | -------------------------------------------------------- |
| **OTA Upgrade**    | Firmware over-the-air upgrade, 4G module OTA, differential upgrade |
| **Watch Face Management** | Watch face file browsing, insertion, deletion, custom backgrounds |
| **Health Data**   | Heart rate, blood oxygen, blood pressure, body temperature, sleep monitoring data sync |
| **Sports Data**   | Sports info sync, step count, calorie consumption |
| **Message Sync**   | SMS, phone calls, social app message push |
| **Weather Info**   | Weather synchronization |
| **Contacts**     | Contact sync, emergency contact settings |
| **Alarm Management**   | Alarm add/delete/modify/query |
| **File Transfer**   | Large file transfer (e.g. music files), file browsing, file management |
| **Fall/Sedentary Reminder** | Health settings and safety alerts |
| **Music Control**   | Music file transfer, playback control, ID3 info display |
| **Image Conversion**   | BMP/GIF/ARGB image encode/decode conversion |
| **Find Device**   | Find device or find phone |
| **Alipay**     | Alipay activation, payment functionality |
| **AI Watch Face**     | AI cloud service, AI watch face functionality |
| **Custom Commands** | Support for customer extended features |

---

## Two: Environment Requirements

| Category | Requirement | Description |
|------|------------|-----------|
| **Operating System** | Android 5.1+ | BLE support required |
| **Hardware** | RCSP-capable SDK | AC701N, AC707N, AC697N, AC696N, AC695N, etc. |
| **Development Platform** | Android Studio | Latest version recommended |
| **Language Support** | Java/Kotlin | Full API support provided |

---

## Three: Quick Start

### 3.1 Clone Repository

```bash
git clone https://github.com/Jieli-Tech/Android-JL_Health.git
cd Android-JL_Health
```

### 3.2 Import Project into Android Studio

1. Open Android Studio
2. Select "Open an existing project"
3. Navigate to the extracted `code/` directory
4. Open the corresponding sample project file

### 3.3 Add Dependencies

- **JL_Watch_Vxxx-release.aar** : Core Jieli Health SDK library providing main wearable device functionality
- **jl_bluetooth_connect_Vxxx-release.aar** : Bluetooth connection related
- **jl_bt_ota_Vxxx-release.aar** : OTA upgrade related
- **jl_rcsp_Vxxx-release.aar** : RCSP base protocol related
- **jl_health_http_Vxxx-release.aar** : Jieli Health server related
- **BmpConvert_Vxxx-release.aar** : Image conversion (BMP/JPEG/PNG, etc.)
- **GifConvert_Vxxx-release.aar** : GIF dynamic image conversion
- **jl_audio_decode_Vxxx-release.aar** : Opus and Speex audio decoding

**Note: xxx represents the version number.**

Add the AAR files from the `libs/` directory to your project's `libs` folder, and add dependencies in `build.gradle`:

```gradle
dependencies {
    // 1. Place the above .aar files in the libs folder of the corresponding module
    // 2. Add in the module's build.gradle
    implementation fileTree(include: ['*.aar'], dir: 'libs')

    implementation 'com.google.code.gson:gson:2.13.1'
}
```

### 3.4 Permission Configuration

When integrating the SDK, request the following permissions in `AndroidManifest.xml`:

```xml
<!-- Bluetooth permissions -->
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>

<!-- Required for newer Android versions -->
<uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />

<!-- Location permission, required by Android for Bluetooth/network development -->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

<!-- Storage permissions, required for file transfer and watch face management -->
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

### 3.5 Run Sample Applications

Refer to the test APKs in the `apk/` directory:

- **YiDong Health** — Full health SDK feature demo, recommended for download from app stores
- **Watch Test Tool** — For testing various watch functions

---

## Four: Project Structure

```
Android-JL_Health/
├── apk/                                     # Test APK folder
│   ├── app                                  # YiDong Health test APK, recommended for download from app stores
│   └── tool                                 # Watch test tool for testing watch functions
├── code/                                    # Reference source code folder
│   ├── app                                  # YiDong Health open source code
│   └── tool                                 # Watch test tool open source code
├── doc/                                     # Development documentation folder
│   ├── Jieli Health SDK (Android) Developer Guide  # Health SDK developer documentation
│   ├── Jieli OTA External Library (Android) Docs   # OTA library developer documentation
│   └── Jieli Connect Library (Android) Docs          # Bluetooth connection library documentation
├── libs/                                    # Core library folder
│   ├── ALi/                                 # Alipay related libraries
│   │   └── AliAgent-release-xxx.aar         # Alipay activation library
│   ├── JL/ui/                               # UI component libraries
│   │   ├── jl_dialog_Vxxx-debug.aar         # Jieli dialog styles
│   │   ├── jl_health_http_Vxxx-release.aar  # Jieli Health server related
│   │   └── jl-component-lib_Vxxx-release.aar# Jieli utility classes
│   ├── jldecryption_v0.4-release.aar        # Encryption/decryption related
│   ├── jl_bluetooth_connect_Vxxx-release.aar# Bluetooth connection related
│   ├── jl_bt_ota_Vxxx-release.aar           # Jieli OTA related
│   ├── jl_rcsp_Vxxx-release.aar             # Base protocol related
│   ├── JL_Watch_Vxxx-release.aar            # Jieli Health SDK core library
│   ├── BmpConvert_Vxxx-release.aar          # Image conversion (BMP/JPEG/PNG, etc.)
│   ├── GifConvert_Vxxx-release.aar          # GIF dynamic image conversion
│   └── jl_audio_decode_Vxxx-release.aar     # Opus and Speex audio decoding
├── Jieli_Health_SDK_Android_Releases.pdf    # SDK release notes
└── ReadMe.txt                               # Instructions file
```

---

## Five: Configuration Guide

### 5.1 SDK Initialization

#### 5.1.1 Extend Parent Class

```java
// Implement the health management class
public class WatchManager extends WatchOpImpl{

   private BluetoothDevice mTargetDevice;

   public static WatchManager getInstance() {
       if (null == instance) {
           synchronized (WatchManager.class) {
              if (null == instance) {
                  instance = new WatchManager(FUNC_WATCH);
               }
            }
        }
        return instance;
   }

   // FUNC_WATCH: watch functionality
   // FUNC_RCSP: use RCSP protocol only
   // FUNC_FILE_BROWSE: use RCSP protocol and file browsing
    public WatchManager(int func) {
        super(func);
    }
     /**
      * Get the currently connected device; all SDK operations are based on this device.
      * @return Target device
      */
    @Override
    public BluetoothDevice getConnectedDevice() {
        // TODO: Customer overrides this method
         return mTargetDevice;
    }

    /**
     * SDK notifies external layer that data needs to be sent.
     * @param device Bluetooth device object
     * @param data   Data packet (byte array)
     * @return false: send failed  true: send succeeded
     */
    @Override
    public boolean sendDataToDevice(BluetoothDevice device, byte[] data) {
        // TODO: Customer overrides this method
         return false;
    }
}
```



#### 5.1.2 External State and Data Sync

```java
WatchManager mWatchManager = WatchManager.getInstance();
// 1. Notify SDK of Bluetooth device connection status
// targetDevice: target device
// connection status: must be converted to StateCode constants
// Note: connection status must be converted to internal StateCode values
mWatchManager.notifyBtDeviceConnection(targetDevice, StateCode.CONNECTION_OK);
// 2. Notify SDK of received data
// targetDevice: target device
// data: byte array, data received from the target device
mWatchManager.notifyReceiveDeviceData(targetDevice, data);
// 3. SDK notifies external layer to send data (implemented via overridden subclass method)
// device: target device
// data: data to send
sendDataToDevice(BluetoothDevice device, byte[] data);
```



**Notes:**

1. The passthrough connection status must be converted to the internal defined connection states.

2. If the device requires **authentication flow**, complete the device authentication flow after connection before callback the success status.

3. For the send data interface, if implemented via **BLE**, pay attention to `MTU packet splitting` and `queue-based sending`.

   - BLE MTU packet splitting: BLE connection negotiates an MTU value; data exceeding the MTU will be discarded by the system.

     To avoid data loss, send data according to the MTU size. If the data length exceeds the MTU, perform MTU-based packet splitting.

   - BLE send queue: concurrent sends can easily cause the phone's BLE protocol stack to hang.

     It is recommended to use **queue-based sending** based on the status returned by `BluetoothGattCallback#onCharacteristicWrite` after sending data.



### 5.2 SDK Initialization Flow

Please refer to [SDK Initialization Flow](https://doc.zh-jieli.com/Apps/Android/health/en-us/master/Development/import.html#sdk-init-flow) for details.

### 5.3 HealthAide Core Classes

| Module | Reference Class |
|--------|----------------|
| **Bluetooth Connection** | `com.jieli.healthaide.tool.bluetooth.BluetoothHelper` |
| **Health SDK** | `com.jieli.healthaide.tool.watch.WatchManager` |
| **OTA Upgrade** | `com.jieli.healthaide.tool.upgrade.OTAManager` |
| **4G Module OTA** | `com.jieli.healthaide.ui.device.upgrade.UpgradeViewModel` |

### 5.4 Watch Test Tool Core Classes

| Module | Reference Class |
|--------|----------------|
| **Bluetooth Connection** | `com.jieli.watchtesttool.tool.bluetooth.BluetoothHelper` |
| **Health SDK** | `com.jieli.watchtesttool.tool.watch.WatchManager` |
| **OTA Upgrade** | `com.jieli.watchtesttool.tool.upgrade.OTAManager` |
| **Image Conversion** | Refer to <strong style="color:red">test package</strong> `com.jieli.watchtesttool.BmpConvertDemo` |
| **Custom Commands** | Refer to <strong style="color:red">test package</strong> `com.jieli.watchtesttool.CustomCommandDemo` |

---

## Six: Debugging Tips

- **Log Output**: The SDK provides detailed log output for monitoring Bluetooth connection status and health data interactions
- **Device Debugging**: Use **Android Studio**'s `Logcat` to view real-time logs
- **Troubleshooting**:
  - **SDK**: Refer to [SDK Debugging Guide](https://doc.zh-jieli.com/Apps/Android/health/en-us/master/Other/debug.html)
  - **HealthAide APP**: Refer to the test APK in [APK Directory](./apk/)
  - **Watch Test Tool**: Refer to the test tool in [APK Directory](./apk/)

---

## Seven: Community and Support

### 7.1 Technical Exchange

| Platform | Contact | Status |
|----------|---------|--------|
| **Official Website** | [Jieli Technology](https://www.zh-jieli.com/) | ✅ Active |
| **GitHub Issues** | [Report Issues](https://github.com/Jieli-Tech/Android-JL_Health/issues) | ✅ Active |

### 7.2 Resource Links

| Resource | Link |
|----------|------|
| 📖 **Online Documentation** | [Jieli Health SDK Developer Docs](https://doc.zh-jieli.com/Apps/Android/health/en-us/master/index.html) |
| 📄 **Datasheets** | [Developer Documentation](./doc/) |
| 📚 **Release History** | [Release History](#eight-release-history) |
| 🐛 **Bug Reports** | [GitHub Issues](https://github.com/Jieli-Tech/Android-JL_Health/issues) |

---

## Eight: Release History

| Version | Date | Changelog |
|---------|------|-----------|
| 1.14.0 | 2026/01/30 | 1. New Features<br />1.1 Added support for ``FIND MY`` device reconnection<br />1.2 Added AC707N image compression algorithm support<br />1.3 Added AC707N GIF format support<br />1.4 Added special upgrade path support for multiplexed space<br />2. Optimizations<br />2.1 Added Android 15 compatibility<br />3. Bug Fixes<br />3.1 Fixed intermittent large file transfer failures<br />3.2 Fixed known issues |
| 1.13.1 | 2024/11/29 | 1. New Features<br/>1.1 Added AC707N image transcoding algorithm support<br/>1.2 Added image captcha mechanism<br />2. Bug Fixes<br />2.1 Fixed crash caused by wrist-up screen-on<br />2.2 Fixed crash caused by incorrect offset reply from device during large file transfer |
| 1.13.0 | 2024/03/15 | 1. New Features<br />1.1 Added 4G module OTA functionality<br />1.2 Added watch face extended parameters<br />1.3 Improved AI watch face functionality |
| 1.12.0 | 2024/01/05 | 1. New Features<br />1.1 Added AI watch face functionality<br />1.2 Added Nand Flash storage information extension support<br />1.3 Added large file transfer error codes<br />2. Bug Fixes<br />2.1 Fixed intermittent file read failures |
| 1.11.0 | 2023/09/15 | 1. New Features<br />1.1 Added AI cloud service functionality |
| 1.10.0 | 2023/06/26 | 1. New Features<br />1.1 Added alarm overflow data processing<br />1.2 Added filename encoding option for large file transfer<br />1.3 Added x86 and x86_64 platform support<br />2. Bug Fixes<br />2.1 Fixed crash when continuously measuring heart rate<br />2.2 Fixed security vulnerability in unZipFolder<br />2.3 Removed mandatory location permission requirement for Android 12+ |
| 1.9.1  | 2023/03/28 | 1. Bug Fixes<br />1.1 Fixed data loss caused by packet assembly errors |
| 1.9.0  | 2023/03/17 | 1. New Features<br />1.1 Added cancel large file transfer API<br />2. Optimizations<br />2.1 Unified error codes<br />3. Bug Fixes<br />3.1 Fixed crash caused by Arabic locale<br />3.2 Compatible with Android 13 BLE broadcast format |
| 1.8.0  | 2022/11/17 | 1. New Features<br />1.1 Added device settings adaptation functionality<br />1.2 Added ARGB image support for image conversion<br />2. Bug Fixes<br />2.1 Fixed abnormal data for fall alert emergency contacts<br />2.2 Fixed health setting command failure status handling<br />2.3 Fixed abnormal behavior of other commands during OTA |
| 1.7.5  | 2022/09/26 | 1. Optimizations<br />1.1 Added Android 12 compatibility<br />2. Bug Fixes<br />2.1 Fixed missing files after music transfer<br />2.2 Fixed crash caused by health setting command reply failure<br />2.3 Fixed SPP dual-mode single backup OTA upgrade anomalies |
| 1.7.1  | 2022/07/27 | 1. Bug Fixes<br />1.1 Fixed Jieli Bluetooth connect library infinite loop when no filter is applied during device search<br />1.2 Fixed known issues |
| 1.7.0  | 2022/07/12 | 1. New Features<br />1.1 Added APIs for getting remaining watch space and watch face file size<br />2. Optimizations<br />2.1 Compatible with single backup OTA flow<br />3. Bug Fixes<br />3.1 Fixed wrist-up screen-on type error<br />3.2 Fixed invalid lower limit for continuous heart rate measurement<br />3.3 Fixed small file transfer anomalies |
| 1.6.7  | 2022/05/13 | 1. New Features<br />1.1 Added BLE to SPP connection strategy<br />2. Bug Fixes<br />2.1 Fixed duplicate file list issue in device file browsing |
| 1.6.5  | 2022/02/18 | 1. New Features<br />1.1 Watch face operations: browse, insert, delete watch face files, custom backgrounds<br />1.2 Large file transfer: music file transfer, etc.<br />1.3 Contacts: contact synchronization<br />1.4 Health data sync: heart rate, step count, etc.<br />1.5 Sports data sync: sports information<br />1.6 Weather sync: weather data synchronization<br />1.7 Message sync<br />1.8 Health settings: fall alert, sedentary reminder, heart rate test, etc.<br />1.9 Device file browsing<br />1.10 Alarm management: add, delete, modify alarms<br />1.11 Find device functionality |

---

## Nine: License

This project is licensed under the [Apache License 2.0](./LICENSE).

```
Copyright 2024 Zhuhai Jieli Technology Co., Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

<div align="center">

**© 2024 Zhuhai Jieli Technology Co., Ltd. | Licensed under Apache License 2.0**

</div>
