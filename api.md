# API



# 前言

`termux-api`总共提供了57个API

~~写死我了~~

## 安装

首先去[这里](https://github.com/termux/termux-api/releases/download/v0.50.1/termux-api_v0.50.1+github-debug.apk)下载termux-api，或者从[F-droid](https://f-droid.org/zh_Hans/packages/com.termux.api/)下载 [清华源加速](https://mirrors.tuna.tsinghua.edu.cn/fdroid/repo/com.termux.api_51.apk)

然后在Termux上安装`termux-api`软件包：

```shell
pkg i termux-api
```

## 卸载

打开设置，打开应用列表，找到termux-api，点击卸载

然后在termux中执行：
```shell
pkg remove termux-api
```

## 功能

### `termux-api-start`

启动`termux-api`

### `termux-api-stop`

停止`termux-api`

### `termux-audio-info`

输出音频信息

```shell
{
  "PROPERTY_OUTPUT_SAMPLE_RATE": "48000", #采样率
  "PROPERTY_OUTPUT_FRAMES_PER_BUFFER": "192", #每个缓冲器的属性输出帧数
  "AUDIOTRACK_SAMPLE_RATE": 48000, #音轨采样率
  "AUDIOTRACK_BUFFER_SIZE_IN_FRAMES": 3844, #帧中的音轨缓冲区大小
  "AUDIOTRACK_SAMPLE_RATE_LOW_LATENCY": 48000, #音轨采样率低延迟
  "AUDIOTRACK_BUFFER_SIZE_IN_FRAMES_LOW_LATENCY": 192, #帧中的音轨缓冲区大小低延迟
  "BLUETOOTH_A2DP_IS_ON": false, #蓝牙A2DP开启状态
  "WIREDHEADSET_IS_CONNECTED": false #有线耳机连接状态
}
```

### `termux-battery-status`

输出电池状态

```shell
{
  "health": "GOOD", #健康状态
  "percentage": 91, #当前电量
  "plugged": "PLUGGED_AC", #当前插入类型(直流/交流)
  "status": "CHARGING", #当前电池状态
  "temperature": 35.099998474121094, #温度
  "current": 641479
}
```

### `termux-brightness`

将屏幕亮度设置在 0 到 255 之间或自动

### `termux-call-log`

获取通话记录

### `termux-camera-info`

摄像头信息

```shell
[
  {
    "id": "0", #摄像头ID
    "facing": "back", #前置还是后置摄像头
    "jpeg_output_sizes": [ #jpeg支持的导出分辨率大小
      {
        "width": 4000,
        "height": 3000
      },
      {
        "width": 3840,
        "height": 2160
      }
    ],
    "focal_lengths": [ #焦距
      3.431999921798706
    ],
    "auto_exposure_modes": [ #自动曝光模式
      "CONTROL_AE_MODE_OFF",
      "CONTROL_AE_MODE_ON",
      "CONTROL_AE_MODE_ON_AUTO_FLASH",
      "CONTROL_AE_MODE_ON_ALWAYS_FLASH",
      "CONTROL_AE_MODE_ON_AUTO_FLASH_REDEYE"
    ],
    "physical_size": { #物理尺寸
      "width": 4.859361171722412, #宽
      "height": 3.6493611335754395 #长
    },
    "capabilities": [ #功能
      "backward_compatible",
      "manual_sensor",
      "manual_post_processing",
      "read_sensor_settings",
      "burst_capture",
      "private_reprocessing",
      "yuv_reprocessing",
      "raw"
    ]
  },
  {
    "id": "1",#摄像头ID
    "facing": "front",#前置还是后置摄像头
    "jpeg_output_sizes": [ #jpeg支持的导出分辨率大小
      {
        "width": 3264,
        "height": 2448
      },
      {
        "width": 3200,
        "height": 2400
      }
    ],
    "focal_lengths": [ #焦距
      2.4200000762939453
    ],
    "auto_exposure_modes": [ #自动曝光模式
      "CONTROL_AE_MODE_OFF",
      "CONTROL_AE_MODE_ON"
    ],
    "physical_size": { #物理尺寸
      "width": 3.5577609539031982,
      "height": 2.668321132659912
    },
    "capabilities": [ #功能
      "backward_compatible",
      "manual_sensor",
      "manual_post_processing",
      "read_sensor_settings",
      "burst_capture",
      "private_reprocessing",
      "yuv_reprocessing",
      "raw"
    ]
  }
]
```

### `termux-camera-photo`

拍照

#### 用法

`termux-camera-photo [-c 摄像头ID] 输出文件名`

配合`termimage`食用效果更好，拍完之后就能看：`termimage [刚刚输出的图片文件]`

### `termux-clipboard-get`

获取剪贴板信息

### `termux-clipboard-set`

写入剪贴板

#### 用法

`termux-clipboard-set [内容]`

![](https://termux-wiki.oss-cn-beijing.aliyuncs.com/1.png)

### `termux-contact-list`

列出所有联系人

### `termux-dialog`

使用不同的小部件获取用户输入

#### 用法

```shell
支持的组件:

confirm - 显示确认对话框
    [-i 提示] 文字提示 (可选)
    [-t 标题] 设置标题 (可选)

checkbox - 使用复选框选择多个值
    [-v ",,,"] 要使用的逗号分隔值 (必须)
    [-t 标题] 设置标题 (可选)

counter - 在指定范围内选择一个数字
    [-r 最小,最大,初始值] 要使用的 (3) 个数字的逗号分隔符 (可选)
    [-t 标题] 设置标题 (可选)

date - Pick a date
    [-t 标题] 设置标题 (可选)
    [-d "dd-MM-yyyy k:m:s"] 日期小部件输出的 SimpleDateFormat 模式 (可选)

radio - 从单选按钮中选择一个值
    [-v ",,,"] 要使用的逗号分隔值 (必须)
    [-t 标题] 设置标题 (可选)

sheet - 从滑动底部表中选择一个值
    [-v ",,,"] 要使用的逗号分隔值 (必须)
    [-t 标题] 设置标题 (可选)

spinner - 从下拉微调器中选择一个值
    [-v ",,,"] 要使用的逗号分隔值 (必须)
    [-t 标题] 设置标题 (可选)

speech - 录音
    [-i hint] text hint (可选)
    [-t 标题] 设置标题 (可选)

text - 输入文本（如果未指定小部件，则为默认值）
    [-i hint] 文字提示 (可选)
    [-m] 多行而不是单行 (可选)*
    [-n] 只能输入数字 (可选)*
    [-p] 输入密码 (可选)
    [-t 标题] 设置标题 (可选)
       * [-m] 和 [-n] 不能一起使用！

time - 选择时间值
    [-t 标题] 设置标题 (可选)
```

### `termux-download`

他会调用安卓内置下载管理器下载

#### 用法

`termux-download -d [描述] -t [标题] -p [目标路径] URL`

### `termux-fingerprint`

使用设备上的指纹传感器检查身份验证

```shell
{
  "errors": [], #错误
  "failed_attempts": 0, #失败次数
  "auth_result": "AUTH_RESULT_SUCCESS" #验证结果
}
```

#### 用法

`termux-fingerprint -t [标题] -d [描述] -s [子标题] -c [是否能取消]`

### `termux-infrared-frequencies`

查询红外发射器支持的载频

### `termux-infrared-transmit`

发射红外模式。 该模式以逗号分隔的开/关间隔指定，例如“20,50,20,30”。 只会传输短于 2 秒的模式。

#### 用法

`termux-infrared-transmit -f [频率模式]`

### `termux-job-scheduler`

安排脚本以指定的时间间隔运行

#### 用法

```shell
用法: termux-job-scheduler [选项]
  -p/--pending               列出待处理的作业
  --cancel-all               取消所有挂起的作业
  --cancel                   取消指定的作业 ID 并退出
调度选项：
  -s/--script path           要调用的脚本的路径
  --job-id int               作业 ID（将覆盖任何以前具有相同 ID 的作业）
  --period-ms int            大约每周期毫秒安排一次作业（默认 0 表示一次）。
                             请注意，自 Android N 起，最短周期为 900,000 毫秒（15 分钟）。
  --network text             仅在此类网络可用时运行（默认为any）： any|unmetered|cellular|not_roaming|none
  --battery-not-low boolean  仅在电池电量不低时运行，默认为 true（至少 Android O）
  --storage-not-low boolean  仅在存储不低时运行，默认false（至少Android O）
  --charging boolean         只在充电时运行，默认false
  --persisted boolean        如果作业在重新启动后仍然存在，默认为 false
  --trigger-content-uri text （至少安卓 N）
  --trigger-content-flag int default 1, （至少安卓 N）
```

### `termux-keystore`

#### 用法

```shell
支持这些命令:
  list [-d]
  delete <别名>
  generate <别名> [-a alg] [-s 大小] [-u 有效期]
  sign <别名> <算法>
  verify <别名> <算法> <签名>

list：列出存储在密钥库中的密钥。
  -d           详细结果（包括关键参数）。

delete：从密钥库中永久删除指定的密钥。
  alias        要删除的密钥的别名。

generate：在硬件密钥库中创建一个新密钥。
  alias       密钥别名
  -a alg       要使用的算法（“RSA”或“EC”）。 默认为 RSA。
  -s size      要使用的密钥大小。 对于 RSA，选项为 2048、3072
               和 4096。对于 EC，选项为 256、384 和 521。
  -u validity  用户有效期以秒为单位。 省略以禁用。
                启用后，密钥只能用于设备解锁后指定的持续时间。 后持续时间已过，用户需要重新锁定并再次解锁设备以使用此密钥。

sign：使用给定的密钥签名，数据从标准输入和签名输出到标准输出。
  alias        用于签名的密钥的别名
  algorithm    要使用的算法，例如 'SHA256withRSA'。 这应该匹配密钥的算法。

verify：验证签名。 从标准输入读取数据（原始文件）。
  alias        用于验证的密钥的别名
  algorithm    用于签署此数据的算法
  signature    用于验证的签名文件
```

### `termux-location`

获取地理位置

* 部分手机会显示："termux:api 无响应"

#### 用法

```shell
usage: $SCRIPTNAME [-p 提供者] [-r 请求]
  -p provider  位置提供者 [gps/network/passive] (默认: gps)
  -r request   提出的要求 [once/last/updates] (默认: once)
```



### `termux-media-player`

顾名思义，媒体播放器

#### 用法

```shell
info        显示当前播放信息
play        如果暂停则继续播放
play <文件> 播放指定的媒体文件
pause       暂停播放
stop        退出播放
```

### `termux-media-scan`

扫描指定文件并将其添加到“媒体内容提供商”

#### 用法

```shell
termux-media-scan [-v] [-r] file [文件...]
-r 递归扫描目录
-v 详细模式
```

### `termux-microphone-record`

使用设备上的麦克风录制音频（~~又名Termux牌录音机~~）

#### 用法

```shell
-d           使用默认值开始录音
-f <文件>     开始录音到特定文件
-l <限制秒数>  以指定的限制开始录音（以秒为单位，0 无限制）
-e <编码器>   使用指定的编码器开始录音（aac、amr_wb、amr_nb）
-b <比特率>   以指定的比特率开始录音（以 kbps 为单位）
-r <采样率>   以指定的采样率开始录音（以赫兹为单位）
-c <数字>     使用指定的通道数开始录音（1、2、...）
-i           获取有关当前录音的信息
-q           退出录音
```

### `termux-nfc`

~~这名字一看就知道~~从/向 NDEF 标签读取/写入数据

#### 用法

```shell
-r, 读取 short，从NFC中读取短信息 full，从NFC中读取完整信息
-w, 在NFC上写信息
-t, NFC的文本
```

### `termux-notification-channel`

创建或删除通知(**仅支持Android 8.0+**)

#### 用法

```shell
termux-notification-channel -d channel-id
termux-notification-channel channel-id channel-name
使用 -d 删除通知。
创建通知需要通知 ID 和通知名称。
该名称将在选项中可见，该 ID 用于在该特定通知上发送通知。
再次创建具有相同 id 的通知将更改名称。
创建与已删除通知具有相同 id 的通知将恢复已删除通知的用户设置。
使用 termux-notification --channel channel-id 在自定义通知上发送通知。
```



```she
```

