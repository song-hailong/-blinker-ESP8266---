# Blinker-Switch

通过改造墙壁开关，实现语音控制灯的效果。接入的平台为点灯科技，语音助手为小爱同学，可改造成天猫精灵和百度小度。

视频链接为： [【blinker】1：ESP8266点灯科技开发环境搭建](https://www.bilibili.com/video/BV1sk4y127Ab/?spm_id_from=333.999.0.0&vd_source=5d0dd24722835df97c44f4058436cf53)  [【blinker】2：语音开关灯，墙壁开关改造篇！](https://www.bilibili.com/video/BV1dz4y1f7gt/?spm_id_from=333.999.0.0&vd_source=5d0dd24722835df97c44f4058436cf53)

Blinker开发环境搭建可根据文档 **[点灯科技开发环境搭建](https://www.songhailong.cn/2022/05/%E7%82%B9%E7%81%AF%E7%A7%91%E6%8A%80%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/)** 进行操作。

PlatformIO IDE开发环境搭建可根据 [VSCode 下 PlatformIO 的安装教程](https://songhailong.cn/2023/01/VSCode%E4%B8%8BPlatformIO%E7%9A%84%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B/) 进行安装。

---

# 常见问题：

1. 米家同步后无设备：需设备在线时点同步。
2. 米家APP设备页不显示该设备：点灯科技只能接入小爱同学，不能显示在米家主页，只会在其他平台设备页显示。如需设置与米家设备联动，可选择 **小爱音响 -> 自定义指令 -> 输入对应指令（如：”打开客厅的灯泡“） -> 选择静默执行**。

# 更新说明：

更新 3.0.2 版本代码，加入自动配网程序 [WiFiManager](https://github.com/song-hailong/WiFiManager) ，可以上传 key，不需修改代码，直接烧入后配网即可。

设置上电后连上WiFi `AutoConnectAP` ，在弹出的界面进行配网。

![new ducument-300](https://res.cloudinary.com/dqv7zex1k/image/upload/v1697270720/2023/10/f20379d405ba7f8a2f63fbb42a090cae.jpg)



## 一：项目文件介绍

#### 1. **Hardware**

Hardware文件夹为Blinker-Switch电路的原理图和PCB文件，提供Altium Designer格式的源文件。

#### 2. **Software**

Software文件夹为Blinker-Switch的程序源码。

2.1 **Arduino IDE**文件夹为初代程序代码，编译器为Arduino IDE，程序版本号为v2.0，推荐使用，对应的APP界面配置文件为：[界面配置_v2.0.txt](3.%20AppInterface/界面配置_v2.0.txt)。

2.2 **PlatformIO**为后续修改的代码，编译器使用的PlatformIO，程序版本号为v3.0，连续测试一个月后出现卡死，此版本上传数据太多，对于ESP8266来说容易卡死，目前不推荐使用，后续有时间进行优化。对应的APP界面配置文件为：[界面配置_v3.0.txt](3.%20AppInterface/界面配置_v3.0.txt)。

#### 3. AppInterface

AppInterface文件夹中提供了APP界面配置文件，版本号对应程序代码版本号。

#### 4. Docs

相关的参考文件，包括环境搭建和芯片的Datasheet等。

## 二：硬件说明

这款板子是零火版取电的，也就是86盒里面必须要有零线，如果没有的话，可以尝试加入单火取电模块，某宝有卖。

接线图如下：

<img src="https://s2.loli.net/2022/05/08/tdeuvQmYl4GoInp.png" alt="image-20220508171217312" style="zoom:30%;" />

> AC220V，一定一定要注意安全，一定要断电后操作。

## 三：程序说明

> 3.0.2 版本的代码已加入配网界面，可不修改代码，直接烧入。

将如下代码修改为自己的，设备密匙见下文。

<img src="https://s2.loli.net/2023/01/14/hS4yqLcGA1njFHW.png" alt="image-20230114151741008" style="zoom: 67%;" />

**烧入**：选择对应的串口，以及开发板型号，将程序烧入即可。

## 四：APP配置

将界面配置文件导入到app设备中。

1. 在app中添加设备，获取Secret Key

   进入App，点击右上角的“+”号，然后选择添加设备，点击选择Arduino -> WiFi接入-> 选择要接入的服务商 -> 复制申请到的Secret Key

   ![Snipaste_2023-11-18_14-23-30](https://s2.loli.net/2023/11/18/PoLrGZSQhb32fwe.png)

2. DIY界面

   在设备列表页，点击刚才新建的设备图标，进入设备控制面板。首次进入设备控制面板，会弹出向导页，在向导页点击载入示例，即可载入示例组件。点击右上角的修改，选择开关的按钮，样式选择中间那种，按键类型选择：开关按键，再点击有上角的保存。之后我们就可以通过这个按键来控制并查看灯。

   ![Snipaste_2023-11-18_14-31-04](https://s2.loli.net/2023/11/18/ZbYFrqKWoSHDEwC.png)

3. 需导入我配置的界面的话，在APP中打开刚才新建的设备，点击右上角的 **... > 界面配置**，粘贴[界面配置_v2.0.txt](3.%20AppInterface/界面配置_v2.0.txt)中的配置代码即可。
