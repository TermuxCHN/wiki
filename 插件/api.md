# API



# 前言

`termux-api`总共提供了57个API

~~写死我了~~

## 下载

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

`termux-camera-photo [-c 摄像头ID] 输出文件`

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

### `termux-notification-list`

显示当前显示的通知。

#### 用法

```shell
termux-notification-list
```

对，你没看错，就是直接用🤣

### `termux-notification-remove`

删除之前使用 `termux-notification --id` 显示的通知。

#### 用法

```shell
termux-notification <ID>
```

### `termux-notification`

显示系统通知。 

#### 用法

```shell
  --action action          按下通知时执行的操作
  --alert-once             编辑通知时不提醒
  --button1 text           在第一个通知按钮上显示的文本
  --button1-action action  在第一个通知按钮上执行的操作
  --button2 text           在第二个通知按钮上显示的文本
  --button2-action action  在第二个通知按钮上执行的操作
  --button3 text           在第三个通知按钮上显示的文本
  --button3-action action  在第三个通知按钮上执行的操作
  -c/--content content     通知中显示的内容。 将优先于标准输入。 如果内容没有作为参数或标准输入传递，那么会有 3 秒的延迟。
  --channel channel-id     指定应发送此通知的通知通道 ID。在低于 8.0 的 Android 版本上，这是无操作的。 使用 termux-notification 频道创建自定义频道。如果频道 id 无效，则不会发送通知。
  --group group            通知组（同一组的通知一起显示）
  --help-actions           显示actions帮助
  -i/--id id               通知 id（将覆盖任何以前具有相同 id 的通知）
  --icon icon-name         设置状态栏中显示的图标。 在 https://material.io/resources/icons/ 上查看可用的图标（默认图标：event_note）
  --image-path path        将在通知中显示的图像的绝对路径
  --led-color rrggbb       闪烁 LED 的颜色为 RRGGBB（默认值：none）
  --led-off milliseconds   LED 在闪烁时关闭的毫秒数（默认值：800）
  --led-on milliseconds    LED 在闪烁时亮起的毫秒数（默认值：800）
  --on-delete action       清除通知时执行的操作
  --ongoing                固定通知
  --priority prio          通知优先级（高/低/最大/最小/默认）
  --sound                  用通知播放声音
  -t/--title title         要显示的通知标题
  --vibrate pattern        振动模式，逗号分隔，如 500,1000,200
  --type type              要使用的通知样式（默认/媒体）媒体操作（可与 --type "media" 一起使用）
  --media-next             在 media-next 按钮上执行的操作
  --media-pause            在媒体暂停按钮上执行的操作
  --media-play             在媒体播放按钮上执行的操作
  --media-previous         在 media-previous 按钮上执行的操作
```

###### actions的用法

```shell
此帮助指的是 --action、--on-delete、--button-1-action 和 --media-next 等选项的参数。
所有这些命令都将一个动作字符串作为它们的参数，它被馈送到`dash -c`。
使用动作时必须牢记一些重要的事情：
您应该使用在终端之外执行操作的操作，例如 --action "termux-toast hello"。
任何输出到终端的东西都是无用的，所以输出应该被重定向（--action "ls > ~/ls.txt"）或以不同的方式显示给用户（--action "ls|termux-toast" ）。
在单个操作中运行多个命令就像：
--action "command1; command2; command3"
或者"
--action "if [ -e file ]; then termux-toast yes; else termux-toast no; fi".
对于更复杂的事情，您应该将脚本放在一个文件中，使其可执行，并将其用作操作：
--action ~/bin/script
该操作在不同的环境（不是子shell）中运行。 因此，您的环境丢失了（最明显的是 $PATH），并且 ~/.profile 也没有来源。 因此，如果您需要 $PATH，您应该：
 - 如果操作是脚本，请在脚本中明确设置 (例如： export PATH="$HOME/bin:\$PATH")
 - 或使用类似的东西： --action "bash -l -c 'command1; command2'").
在 Android N 或更高版本上，您可以在您的操作中使用特殊变量 $REPLY 来使用 Android 的直接回复功能。
这会提示用户直接在通知中输入一些文本，然后将其替换为您的操作。
 - termux-notification --button1 "答案" --button1-action "termux-toast \\$REPLY"
将调用该操作：
 - termux-toast "用户输入的文本"
小心为单引号或双引号正确转义 shell 命令，例如：
  --button1-action 'something $REPLY' or --button1-action "something \\$REPLY"
  
```

### `termux-saf-create`

在Termux:API管理的文件夹中创建文件。

#### 用法

```shell
-t 指定文件的 mime 类型。 其他应用程序需要 MIME 类型来识别内容
例如 一段录像。 如果未指定，则假定为“application/octet-stream”，即原始二进制数据。返回您可以使用 termux-saf-read 和 termux-saf-write 读取和写入文件的 URI。您可以明确指定 mime 类型或根据文件扩展名猜测它。作为文件夹 URI，您可以使用 由 termux-saf-dirs 或 termux-saf-ls.Android 列出的目录的 URI 不允许创建具有相同名称的文件，因此如果具有该名称的文件或文件夹已经存在，则名称可能会更改。您 可以使用 termux-saf-stat 和返回的 URI 来获取它真正给出的名称。 
```

### `termux-saf-dirs`

与 `termux-saf-ls` 相同的格式列出您提供给 Termux:API 的所有目录。

#### 用法

```shell
这意味着这列出了包含您可以使用其他 termux-saf-*`` 命令访问的所有目录的“目录”。
URI 可以与其他 termux-saf-* 命令一起使用，以创建文件和文件夹并列出目录内容。
请参阅 termux-saf-managedir 以授予 Termux:API 对文件夹的访问权限。
```

### `termux-saf-ls`

列出有URI 标识的文件夹中的文件和文件夹。

#### 用法

```shell
您可以通过以下方式获取文件夹 URI：
- 使用 termux-saf-ls 列出文件夹
- 使用 termux-saf-managedir 授予 Termux:API 对文件夹的访问权限
- 使用 termux-saf-dirs 列出您授予 Termux:API 访问权限的文件夹
- 使用 termux-saf-mkdir 创建文件夹
该列表以 JSON 数组的形式返回，每个条目有一个 JSON 对象。
对象具有键：
- 'name' 用于人类可读的名称
- 'uri' 表示你可以与其他 termux-saf-* 命令一起使用的 URI
- 'type' 代表 mime 类型
- 'length' 表示大小（如果它是一个文件）
您可以通过特殊的 mime 类型“vnd.android.document/directory”识别文件夹。
```

### `termux-saf-managedir`

打开系统自带文件管理并让您指定 Termux:API 可以访问的文件夹。

#### 用法

```shell
然后，您可以使用 termux-saf-* 实用程序来管理该文件夹中的内容。
返回标识目录的 URI，此 URI 可与其他 termux-saf-* 命令一起使用以创建文件和文件夹并列出目录内容。
如果您关闭文件管理器，则会返回一个空字符串。
您可以使用 termux-saf-dirs 列出您授予 Termux:API 访问权限的所有目录。
```

### `termux-saf-mkdir`

通过 SAF 创建目录，这与 `termux-saf-create` 的行为类似，仅适用于目录。

#### 用法

`termux-saf-mkdir <目录名>`

### `termux-saf-read`

从 URI 标识的文件中读取数据并将数据写入标准输出。

#### 用法

```shell
您可以使用管道处理数据或将其重定向到文件中以制作本地副本。
请参阅 termux-saf-list 以获取文件的 URI。
```

### `termux-saf-rm`

删除指定 URI 处的文件或文件夹。 有关详细信息，请参阅其他 `termux-saf-*` 命令。

成功返回 0，如果无法删除文件或文件夹，则返回 1，如果发生另一个错误，则返回 2。

#### 用法

```shell
termux-saf-rm <文件&文件夹名字>
```

### `termux-saf-stat`

将文件或文件夹信息作为 JSON 对象返回，格式与 termux-saf-ls 中的条目相同。

#### 用法

`termux-saf-stat <文件&文件夹名字>`

### `termux-saf-write`

将标准输入写入由 URI 标识的现有文件。**先前的内容会被删除！**

#### 用法

`termux-saf-write <文件>`

### `termux-sensor`

获取有关传感器类型以及实时数据的信息。

#### 用法

```shell
  -a, all            聆听所有传感器（警告！可能对电池有影响）
  -c, cleanup        清理（释放传感器资源）
  -l, list           显示可用传感器列表
  -s, sensors [,,,]  监听的传感器（可以只包含部分名称）
  -d, delay [毫秒]    接收新传感器更新前的延迟时间（以毫秒为单位）
  -n, limit [数字]    读取传感器的次数（默认：连续）（分钟：1）
```

### `termux-share`

如果没有给出文件参数，则共享指定为参数的文件或在标准输入上接收到的文本。

#### 用法

```shell
  -a action        对共享内容执行的操作：
                     edit(编辑)/send(发送)/view(查看) (默认:view)
  -c content-type  要使用的内容类型（默认值：从文件扩展名中猜测，标准输入为 text/plain）
  -d               如果选择了一个而不是显示选择器，则共享给默认接收器
  -t title         用于共享内容的标题（默认值：shared file name）
```

### `termux-sms-inbox`

这个脚本被替换成`termux-sms-list`了，下一个🤣

### `termux-sms-list`

列出SMS短信。

#### 用法

```shell
用法: termux-sms-list [-d] [-l 限制] [-n] [-o 抵消] [-t 输出] [-c] [-f 数字]
-l 限制短信列表中的偏移量（默认值：$PARAM_LIMIT）
   -o 短信列表中的偏移量（默认值：$PARAM_OFFSET）
   -t 键入要列出的消息类型（默认值：$PARAM_TYPE）：$SUPPORTED_TYPES
   -c 对话列表（每个对话的唯一项目）
   -f number 定位消息的编号
   -n（过时）显示电话号码
   -d（过时）显示创建消息的日期
```

### `termux-sms-send`

用人话来讲就是发短信。![doge](https://alpha-q3.sourcegcdn.com/2022/06/28/fjId9OKu.png)

#### 用法

```shell
用法: termux-sms-send -n 电话号码[,号码2,号码3,...] [-s 卡1/卡2] [文字]
向指定的收件人号码发送 SMS 消息。 要发送的文本要么作为参数提供，要么从标准输入中读取（如果没有给出参数）。
  -n number(s)  收件人号码 - 用逗号分隔多个号码
  -s slot       要使用的 sim 插槽 - 如果插槽号无效或缺少 READ_PHONE_STATE 权限，则失败
```

### `termux-speech-to-text`

~~一看就知道这是语音转文字~~

#### 用法

```shell
termux-speech-to-text
```

~~对，你没看错，就是直接用~~

其实还能加个进度条：

`termux-speech-to-text -p`

### `termux-storage-get`

向系统请求文件并输出到指定文件。

#### 用法

```shell
termux-storage-get <文件>
```

### `termux-telephony-call`

用人话讲就是打电话![doge](https://alpha-q3.sourcegcdn.com/2022/06/28/fjId9OKu.png)

#### 用法

```shell
termux-telephony-call <电话号码(例如：114514)>
```

### `termux-toast`

在 [Toast](https://baike.baidu.com/item/toast/13002938) 中显示文本（短暂弹出）。

#### 用法

```shell
Toast 文本要么作为参数提供，要么从标准输入中读取
如果没有给出参数。 参数将优先于标准输入。
如果 toast 文本没有作为参数或标准输入传递，那么会有
延迟 3 秒。
 -b  设置背景颜色~~（默认：gay）~~(默认：gray（灰色）)
 -c  设置文本颜色（默认：white(白色)）
 -g  设置吐司的位置：[top(上)、middle(中)，bottom(下)]（默认值：middle）
 -s  只展示亿会儿吐司
注意：颜色可以是标准名称（即红色）或 6 / 8 位十六进制值（即“#FF0000”或“#FFFF0000”），其中 order 为 (AA)RRGGBB。 无效颜色将恢复为默认值
```

### `termux-torch`

打开/关闭手电筒

#### 用法

`termux-torch [on(开)/off(关)]`

### `termux-tts-engines`

获取有关可用文本转语音 (TTS) 引擎的信息。 可以使用 -e 选项将引擎的名称提供给 `termux-tts-speak` 命令。

### `termux-tts-speak`

用人话讲就是调用系统TTS引擎来语音转文字

#### 用法

```shell
用法: termux-tts-speak [-e engine] [-l language] [-n region] [-v variant] [-p pitch] [-r rate] [-s stream] [text-to-speak]
-e engine 要使用的 TTS 引擎（参见 termux-tts-engines）
   -l language 语言（部分引擎可能不支持）
   -n region 说话的语言区域
   -v 语言的变体变体
   -p 在语音中使用的音高。 1.0 是正常音高，较低的值会降低合成语音的音调，较大的值会增加它。
   -r 要使用的语速。 1.0 是正常语速，较低的值会减慢语音（0.5 是正常语速的一半），而较大的值会加速语音（2.0 是正常语速的两倍）。
   -s 要使用的流音频流（默认：NOTIFICATION），以下之一：ALARM、MUSIC、NOTIFICATION、RING、SYSTEM、VOICE_CALL
```

### `termux-usb`

列出或访问 USB 设备，**无法直接访问USB设备**

#### 用法

```shell
  -l           列出可用USB设备
  -r           如有必要，显示权限请求对话框
  -e command   使用引用设备的文件描述符作为参数执行指定的命令（除非给出 -E 参数）
  -E           将文件描述符作为 env var 而不是作为命令行参数传输
```

### `termux-vibrate`

用人话讲就是~~移动版本的筋膜枪~~

#### 用法

```shell
-d duration 以毫秒为单位振动的持续时间（默认值：1000）
-f 即使在静音模式下也强制振动(社死)
```

### `termux-wallpaper`

更改你的手机壁纸。

**这个不是用来改Termux背景的！**

#### 用法

```shell
-f <file>  从文件设置壁纸
-u <url>   从URL资源设置壁纸
-l         为锁屏设置壁纸（Android 7及更高版本）
```

### `termux-wifi-connectioninfo`

获取有关当前 wifi 连接的信息。

#### 用法

`termux-wifi-connection-info`

你没看错，它什么参数都不用加![doge](https://alpha-q3.sourcegcdn.com/2022/06/28/fjId9OKu.png)

### `termux-wifi-enable`

打开/关闭 WIFI

#### 用法

```shell
termux-wifi-enable [true(打开)/false(关闭)]
```

### `termux-wifi-scaninfo`

获取有关wifi 扫描的信息。

#### 用法

```shell
termux-wifi-scaninfo
```

你没看错，它也没有参数，~~除了help~~![doge](https://alpha-q3.sourcegcdn.com/2022/06/28/fjId9OKu.png)
