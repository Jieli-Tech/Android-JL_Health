# Android-JL_Health
中文|[EN](https://github.com/Jieli-Tech/Android-JL_Health/blob/main/README-en.md)

本仓库为杰理健康SDK(Android)的开源仓库，由杰理官方推出，线上线下支持同步发布。

当前版本: `V1.6.7`



## 快速开始

欢迎使用杰理健康SDK(Android)开源项目，在开始开发项目之前，<strong style="color:#de2233">请详细阅读[SDK开发文档](https://doc.zh-jieli.com/Apps/Android/health/zh-cn/master/index.html)</strong>, 从而对杰理健康SDK的结构和功能有大概的认识，并且可以通过文档进行开发接入。





## 开发资料介绍

```tex
├ apk   --- 测试APK
   ├- app  --- 宜动健康测试APK， 建议在应用商店下载
   └- tool --- 手表测试工具, 用于测试手表功能
├ code  --- 参考Demo源码存放
   ├- app  --- 宜动健康开放源码
   └- tool --- 手表测试工具开放源码
├ doc   --- 开发文档
   └- ReadMe --- 现在改为在线文档，请详细阅读
├ libs  --- 相关库
   ├- jldecryption_v0.1-release           --- 加密相关
   ├- jl_bluetooth_connect_V0.2.0-release --- 蓝牙连接相关
   ├- jl_health_http_V1.0.0-release       --- 杰理健康服务器相关
   ├- jl_rcsp_V0.2.3-release              --- 基础协议相关
   ├- JL_Watch_V1.6.7-release             --- 杰理健康相关
   ├- jl_bt_ota_V1.6.0_release            --- 杰理OTA相关
   └- BmpConvert_V0.0.4-release           --- 图像转换相关
```





## 功能实现参考

### 1. 宜动健康

* 蓝牙连接实现，可以参考 `com.jieli.healthaide.tool.bluetooth.BluetoothHelper`
* 健康SDK实现，可以参考 `com.jieli.healthaide.tool.watch.WatchManager`
* OTA功能实现，可以参考 `com.jieli.healthaide.tool.upgrade.OTAManager`



**测试功能可以参考`test包`的单元测试示例**



### 2. 手表测试工具

* 蓝牙连接实现，可以参考 `com.jieli.watchtesttool.tool.bluetooth.BluetoothHelper`
* 健康SDK实现，可以参考 `com.jieli.watchtesttool.tool.watch.WatchManager`
* OTA功能实现，可以参考 `com.jieli.watchtesttool.tool.upgrade.OTAManager`
* 图像转换功能，可以参考 `test包的com.jieli.watchtesttool.BmpConvertDemo`
* 自定义命令功能，可以参考test包的 `com.jieli.watchtesttool.CustomCommandDemo`





## 调试与测试

1. 打开JL_Log的文件输出
	```java
	JL_Log.setTagPrefix("health"); //设置log的标识
	//log配置
	//context    --- 上下文，建议是getApplicationContext()
	//islog      --- 是否输出打印，建议是开发时打开，发布时关闭
	//isSaveFile --- 是否保存log文件，建议是开发时打开，发布时关闭
	JL_Log.configureLog(context, true, true);
	```
	
	
	
2. 打印文件

  1.  打印文件格式
       格式：[tag_prefix]_log_[timestamp].txt
       例如：health_log_20220113093020.432.txt ==> 健康SDK打印文件，创建时间：2022/01/13 09:30:20 
  2. 文件存储路径
       位置: 手机根目录/Android/data/[包名]/files/logcat/
       * 宜动健康
         举例：Android/data/com.jieli.healthaide/files/logcat/
       * 手表测试工具
         举例：Android/data/com.jieli.watchtesttool/files/logcat/

3. 出现异常时的正确处理步骤
   1. 简单描述问题现象 (必要)
   2. 提供最接近时间戳的log文件 (必要)
   3. 提供现象的截图或者视频



## 开源社区

1.  用户可以在 issues 提问, 我司开发者会及时提供回复
2.  用户也可以进入我司的开源群(钉钉: 搜索群号“31691148”), 找到对应负责人进行咨询
