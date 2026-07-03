[tag download]:https://github.com/Jieli-Tech/Android-JL_Health/tags
[tag_badgen]:https://img.shields.io/github/v/tag/Jieli-Tech/Android-JL_Health?style=plastic&logo=android&labelColor=ffffff&color=informational&label=Tag&logoColor=blue

# Android-JL_Health  [![tag][tag_badgen]][tag download]

<div align="center">

**杰理健康SDK(Android) - 专为杰理蓝牙穿戴类产品提供健康数据与设备管理开发平台**

[中文](./README.md) · [English](./README_en.md) · [文档中心](https://doc.zh-jieli.com/Apps/Android/health/zh-cn/master/index.html) · [SDK 版本历史](#八版本历史) · [报告问题](https://github.com/Jieli-Tech/Android-JL_Health/issues)

</div>

---

## 📋 目录

- [一、概述](#一概述)
- [二、运行环境](#二运行环境)
- [三、快速开始](#三快速开始)
- [四、工程结构](#四工程结构)
- [五、配置说明](#五配置说明)
- [六、调试技巧](#六调试技巧)
- [七、社区与支持](#七社区与支持)
- [八、版本历史](#八版本历史)
- [九、许可证](#九许可证)

---



## 一、概述

`Android-JL_Health` 是**珠海市杰理科技股份有限公司**为蓝牙穿戴类产品提供的健康数据与设备管理开发平台。本 SDK 基于<strong style="color:red">RCSP协议(远程控制系统协议)</strong>，提供完整的穿戴设备控制功能和丰富的应用示例，支持以下应用场景：

| 应用类型 | 典型产品 |
|---------|---------|
| **智能手表** | 儿童手表、成人智能手表、健康监测手表 |
| **健康手环** | 运动手环、睡眠监测手环 |
| **穿戴设备** | 智能徽章、智能戒指等可穿戴设备 |

**杰理健康SDK**提供了丰富的功能接口：

| 功能           | 说明                                                     |
| -------------- | -------------------------------------------------------- |
| **OTA升级**    | 固件空中升级、4G模块OTA、差分升级等                        |
| **表盘管理**   | 表盘文件浏览、插入、删除、自定义背景等                     |
| **健康数据**   | 心率、血氧、血压、体温、睡眠等健康监测数据同步             |
| **运动数据**   | 运动信息同步、步数统计、卡路里消耗等                       |
| **消息同步**   | 短信、电话、社交软件消息推送                               |
| **天气信息**   | 同步天气情况                                               |
| **联系人**     | 常用联系人同步、紧急联系人设置                             |
| **闹钟管理**   | 闹钟的增删改查                                             |
| **文件传输**   | 大文件传输(如音乐文件)、文件浏览、文件管理                 |
| **跌倒/久坐提醒** | 健康设置与安全提醒功能                                   |
| **音乐控制**   | 音乐文件传输、播放控制、ID3信息显示                        |
| **图像转换**   | BMP/JPEG/PNG图像编解码转换                     |
| **设备查找**   | 查找设备或查找手机                                         |
| **支付宝**     | 支付宝激活、支付功能                                       |
| **AI表盘**     | AI云服务、AI表盘功能                                     |
| **自定义命令** | 支持客户拓展功能                                         |

---



## 二、运行环境

| 类别 | 要求 | 说明 |
|------|------------|-----------|
| **操作系统** | Android 5.1+ | 支持BLE功能 |
| **硬件要求** | 支持**RCSP功能**的SDK | AC701N、AC707N、AC695N等 |
| **开发平台** | Android Studio | 建议使用最新版 |
| **语言支持** | Java/Kotlin | 提供完整的API支持 |

---



## 三、快速开始

### 3.1 克隆仓库

```bash
git clone https://github.com/Jieli-Tech/Android-JL_Health.git
cd Android-JL_Health
```



### 3.2 导入项目到Android Studio

1. 打开 Android Studio
2. 选择 "Open an existing project"
3. 导航到解压后的 `code/` 目录
4. 打开对应的示例项目文件



### 3.3 添加依赖库

- **JL_Watch_Vxxx-release.aar** : 杰理健康SDK核心库，提供穿戴设备主要功能
- **jl_bluetooth_connect_Vxxx-release.aar** : 蓝牙连接相关
- **jl_bt_ota_Vxxx-release.aar** : OTA升级相关
- **jl_rcsp_Vxxx-release.aar** : RCSP基础协议相关
- **jl_health_http_Vxxx-release.aar** : 杰理健康服务器相关
- **BmpConvert_Vxxx-release.aar** : 图像转换(BMP/JPEG/PNG等)
- **GifConvert_Vxxx-release.aar** : GIF动态图片转换
- **jl_audio_decode_Vxxx-release.aar** : Opus和Speex音频解码

**PS: xxx为版本号**

将 `libs/` 目录下的 AAR 文件添加到项目的 `libs` 目录中，并在 `build.gradle` 中添加依赖：

```gradle
dependencies {
    //1.将上面的aar文件放入工程目录中的对应moudle的lib文件夹下
    //2.在moudlu的build.gradle中添加
    implementation fileTree(include: ['*.aar'], dir: 'libs')

    implementation 'com.google.code.gson:gson:2.13.1'
}
```



### 3.4 权限配置

接入SDK时应在 `AndroidManifest.xml` 申请以下权限:

```xml
<-- 使用蓝牙权限 --!>
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>

<-- 定位权限，官方要求使用蓝牙或网络开发，需要位置信息 --!>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
        
<-- Android 12+ 需要增加蓝牙连接权限 --!>
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```



### 3.5 运行示例应用

参考 `apk/` 目录中的测试APK：

- **宜动健康** — 完整健康SDK功能演示，建议在应用商店下载
- **手表测试工具** — 用于测试手表各项功能

---



## 四、工程结构

```
Android-JL_Health/
├── apk/                                     # 测试APK文件夹
│   ├── app                                  # 宜动健康测试APK，建议在应用商店下载
│   └── tool                                 # 手表测试工具，用于测试手表功能
├── code/                                    # 参考源码工程文件夹
│   ├── app                                  # 宜动健康开放源码
│   └── tool                                 # 手表测试工具开放源码
├── doc/                                     # 开发文档文件夹
│   ├── 杰理健康SDK(Android)开发说明         # 杰理健康SDK开发说明文档
│   ├── 杰理OTA外接库(Android)开发文档       # OTA库的开发说明文档
│   └── 杰理连接库(Android)开发文档          # 蓝牙连接库开发说明文档
├── libs/                                    # 核心库文件夹
│   ├── ALi/                                 # 支付宝相关库
│   │   └── AliAgent-release-xxx.aar         # 支付宝激活库
│   ├── JL/ui/                               # UI组件库
│   │   ├── jl_dialog_Vxxx-debug.aar         # 杰理对话框样式
│   │   ├── jl_health_http_Vxxx-release.aar  # 杰理健康服务器相关
│   │   └── jl-component-lib_Vxxx-release.aar# 杰理工具类
│   ├── jldecryption_v0.4-release.aar        # 加密解密相关
│   ├── jl_bluetooth_connect_Vxxx-release.aar# 蓝牙连接相关
│   ├── jl_bt_ota_Vxxx-release.aar           # 杰理OTA相关
│   ├── jl_rcsp_Vxxx-release.aar             # 基础协议相关
│   ├── JL_Watch_Vxxx-release.aar            # 杰理健康SDK核心库
│   ├── BmpConvert_Vxxx-release.aar          # 图像转换(BMP/JPEG/PNG等)
│   ├── GifConvert_Vxxx-release.aar          # GIF动态图片转换
│   └── jl_audio_decode_Vxxx-release.aar     # Opus和Speex音频解码
├── Jieli_Health_SDK_Android_Releases.pdf    # SDK发布记录
└── ReadMe.txt                               # 说明文件
```

---



## 五、配置说明

### 5.1 SDK初始化

#### 5.1.1 继承父类

```java
//实现健康管理类
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

   //func FUNC_WATCH:手表功能
   //FUNC_RCSP：仅仅使用rcsp协议
   //FUNC_FILE_BROWSE：使用rcsp协议和目录浏览功能
    public WatchManager(int func) {
        super(func);
    }
     /**
      * 获取当前连接的设备，sdk的操作都是基于该设备
      * @return 目标设备
      */
    @Override
    public BluetoothDevice getConnectedDevice() {
        //TODO: 客户重写实现功能
         return mTargetDevice;
    }

    /**
     * SDK通知外部需要发送数据
     * @param device 蓝牙设备对象
     * @param data   数据包 byte数组
     * @return false：发送失败  true:发送成功
     */
    @Override
    public boolean sendDataToDevice(BluetoothDevice device, byte[] data) {
        //TODO: 客户重写实现功能
         return false;
    }
}
```



#### 5.1.2 外部状态和数据同步

```java
WatchManager mWatchManager = WatchManager.getInstance();
//1. 通知SDK蓝牙设备状态
//targetDevice : 目标设备
//connection status : 连接状态
//注意：连接状态需要转换成StateCode的连接状态
mWatchManager.notifyBtDeviceConnection(targetDevice, StateCode.CONNECTION_OK);
//2. 通知SDK接收数据
//targetDevice： 目标设备
//data:byte数组， 接收到目标数据发送的数据
mWatchManager.notifyReceiveDeviceData(targetDevice,data);
//3. SDK通知外部需要发送数据（在子类重写方法实现）
//device: 目标设备
//data: 发送数据
sendDataToDevice(BluetoothDevice device, byte[] data);
```



**注意事项:**

1. 透传连接状态需要转换库内定义的连接状态

2. 如设备需要 **认证流程** ，请连接成功后并完成设备认证流程再回调成功状态

3. 发送数据接口，如果是 **BLE实现** ，需要注意 `MTU分包` 和 `队列式发数`

   - BLE的MTU分包处理: BLE 连接会协商MTU值, 超出MTU的值, 会被系统抛弃。

     为了避免数据丢失, 请按照MTU大小发送, 若发送数据长度超过MTU, 则需要进行MTU分包发送处理

   - BLE发送-队列式发数: BLE并发式发送容易导致手机系统BLE底层协议栈卡住。

     建议发送数据后根据 `BluetoothGattCallback#onCharacteristicWrite` 回调的状态，进行 **队列式发数** 处理



### 5.2 SDK初始化流程

具体参考[SDK初始化流程](https://doc.zh-jieli.com/Apps/Android/health/zh-cn/master/Development/import.html#sdk-init-flow)



### 5.3 宜动健康核心类

| 模块 | 参考类 |
|------|--------|
| **蓝牙连接** | `com.jieli.healthaide.tool.bluetooth.BluetoothHelper` |
| **健康SDK** | `com.jieli.healthaide.tool.watch.WatchManager` |
| **OTA升级** | `com.jieli.healthaide.tool.upgrade.OTAManager` |
| **4G模块OTA** | `com.jieli.healthaide.ui.device.upgrade.UpgradeViewModel` |



### 5.4 手表测试工具核心类

| 模块 | 参考类 |
|------|--------|
| **蓝牙连接** | `com.jieli.watchtesttool.tool.bluetooth.BluetoothHelper` |
| **健康SDK** | `com.jieli.watchtesttool.tool.watch.WatchManager` |
| **OTA升级** | `com.jieli.watchtesttool.tool.upgrade.OTAManager` |
| **图像转换** | 参考 <strong style="color:red">test包</strong> 的 `com.jieli.watchtesttool.BmpConvertDemo` |
| **自定义命令** | 参考 <strong style="color:red">test包</strong> 的 `com.jieli.watchtesttool.CustomCommandDemo` |

---



## 六、调试技巧

- **日志输出**：SDK提供详细的日志输出，可通过日志查看蓝牙连接状态和健康数据交互
- **设备调试**：使用**Android Studio**的``Logcat``查看实时日志
- **问题排查**：
  - **SDK：** 参考 [SDK调试说明](https://doc.zh-jieli.com/Apps/Android/health/zh-cn/master/Other/debug.html)
  - **宜动健康APP:** 参考 [APK目录](./apk/) 中的测试APK
  - **手表测试工具:** 参考 [APK目录](./apk/) 中的测试工具

---



## 七、社区与支持

### 7.1 技术交流

| 平台 | 联系方式 | 状态 |
|------|----------|------|
| **官方网站** | [杰理科技](https://www.zh-jieli.com/) | ✅ 活跃 |
| **GitHub Issues** | [问题反馈](https://github.com/Jieli-Tech/Android-JL_Health/issues) | ✅ 活跃 |



### 7.2 资源链接

| 资源 | 链接 |
|------|------|
| 📖 **在线文档中心** | [杰理健康SDK开发文档](https://doc.zh-jieli.com/Apps/Android/health/zh-cn/master/index.html) |
| 📄 **数据手册** | [开发说明文档](./doc/) |
| 📚 **版本历史** | [版本历史](#八版本历史) |
| 🐛 **问题反馈** | [GitHub Issues](https://github.com/Jieli-Tech/Android-JL_Health/issues) |

---



## 八、版本历史

| 版本 | 日期 | 修改记录 |
|------|------|----------|
| 1.14.0 | 2026/01/30 | 1. 新增功能<br />1.1 增加 ``FIND MY`` 设备回连的支持<br />1.2 增加AC707N图像压缩算法支持<br />1.3 增加AC707N GIF格式支持<br />1.4 增加复用空间特殊升级路程支持<br />2. 优化功能<br />2.1 增加Android 15的兼容处理<br />3. 修复问题<br />3.1 修改大文件传输偶现失败的问题<br />3.2 修复已知的问题 |
| 1.13.1 | 2024/11/29 | 1. 新增功能<br/>1.1 增加AC707N图像转码算法支持<br/>1.2 增加图片验证码机制<br />2. 修复问题<br />2.1 修复抬腕亮屏导致闪退的问题<br />2.2 修复大文件传输中设备回复错误偏移导致闪退的问题 |
| 1.13.0 | 2024/03/15 | 1. 新增功能<br />1.1 增加4G 模块OTA功能<br />1.2 增加表盘拓展参数<br />1.3 完善AI表盘功能 |
| 1.12.0 | 2024/01/05 | 1. 新增功能<br />1.1 增加AI表盘功能<br />1.2 Nand Flash存储器信息拓展支持<br />1.3 增加大文件传输错误码<br />2. 修复问题<br />2.1 修复偶现读取文件失败的问题 |
| 1.11.0 | 2023/09/15 | 1. 新增功能<br />1.1 增加AI云服务功能 |
| 1.10.0 | 2023/06/26 | 1. 新增功能<br />1.1 增加闹钟溢出数据处理<br />1.2 增加大文件传输设置文件名编码方式<br />1.3 增加x86，x86_64平台的支持<br />2. 修复问题<br />2.1 修复设备开关连续心率测试闪退的问题<br />2.2 修复unZipFolder的安全漏洞问题<br />2.3 修复Android 12+ 不强制要求位置权限 |
| 1.9.1  | 2023/03/28 | 1. 修复问题<br />1.1 修复拼包出错导致数据丢失问题 |
| 1.9.0  | 2023/03/17 | 1. 新增功能<br />1.1 增加取消大文件传输接口<br />2. 优化功能<br />2.1 统一错误吗<br />3. 修复问题<br />3.1 修复多国语言(阿拉伯语)导致闪退的问题<br />3.2 兼容 Android 13 BLE 广播格式 |
| 1.8.0  | 2022/11/17 | 1. 新增功能<br />1.1 增加设备设置适配功能<br />1.2 增加图像转换支持ARGB图像的处理<br />2. 修复问题<br />2.1 修复跌倒提醒-设置紧急联系人的数据异常问题<br />2.2 修复健康设置命令失败状态的处理<br />2.3 修复OTA过程中偶现其他命令的异常 |
| 1.7.5  | 2022/09/26 | 1. 优化功能<br />1.1 增加Android 12的兼容处理<br />2. 修复问题<br />2.1 修复音乐传输后刷新列表没找到文件<br />2.2 修复健康设置命令回复失败状态导致闪退的问题<br />2.3 修复双模同地址单备份OTA SPP方式升级异常的问题 |
| 1.7.1  | 2022/07/27 | 1. 修复问题<br />1.1 修复杰理蓝牙连接库在无过滤搜索设备的情况下会死循环<br />1.2 修复已知问题 |
| 1.7.0  | 2022/07/12 | 1. 新增功能<br />1.1 获取手表剩余空间大小和获取表盘文件大小的接口<br />2. 优化功能<br />2.1 兼容单备份OTA流程<br />3. 修复问题<br />3.1 抬腕亮屏类型错误<br />3.2 连续测量心率的下限值无效<br />3.3 小文件传输异常 |
| 1.6.7  | 2022/05/13 | 1. 新增功能<br />1.1 增加BLE切换SPP的连接策略<br />2. 修复问题<br />2.1 设备文件浏览可能出现重复列表的问题 |
| 1.6.5  | 2022/02/18 | 1. 增加功能<br />1.1 表盘操作：表盘文件浏览，插入表盘文件，删除表盘文件，插入表盘自定义背景等等<br />1.2 大文件传输：音乐文件传输等等<br />1.3 常用联系人：同步联系人<br />1.4 健康数据同步：心率，运动步数等<br />1.5 运动数据同步：运动信息同步<br />1.6 天气信息同步：同步天气情况<br />1.7 消息同步<br />1.8 健康设置：跌倒提醒、久坐提醒、心率测试等<br />1.9 设备文件浏览<br />1.10 闹钟功能：增加、删除、修改闹钟<br />1.11 设备查找功能 |

---



## 九、许可证

本项目采用 [Apache License 2.0](./LICENSE) 开源协议。

```
Copyright 2024 珠海市杰理科技股份有限公司

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

**© 2024 珠海市杰理科技股份有限公司 | Licensed under Apache License 2.0**

</div>
