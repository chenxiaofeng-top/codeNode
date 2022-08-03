### 设备

1. 支持nfc的Android设备
2. nfc标签（贴纸）

### 交互

- nfc的Android设备与nfc的Android设备
- nfc的Android设备与nfc标签（贴纸）

### 逻辑

- 可读
- 可写
- 部分提供计算的操作
- 最复杂的nfc贴纸包含操作环境
- 大多数的Android framework api 都是基于[NFC FORUM](http://nfc-forum.org/)（nfc组织，和蓝牙组织sig一样，初始由飞利浦，诺基亚，索尼创建的）定义的NDEF数据标准（NFC Data Exchange Format）

### 操作模式

- Reader/Writer mode（读卡器模式）

​		这种模式允许nfc设备读或者写被动的nfc卡片或者nfc贴纸。

- P2P mode（点对点模式）

​		这种模式允许nfc设备和其他的nfc设备交换数据，Android 系统应用 Androidbeam就是基于这种模式实现的。

- Card emulation mode （卡模式）

​		允许nfc设备自己作为nfc卡片，这种nfc卡片可以被其他的nfc读卡器访问，即使用nfc设备来模拟卡片的交易。nfc卡片可以代替现实生活中的ic卡，公交卡，门禁卡，车票，门票等（现实中的卡有用的也都是一些信息，完全可以把这些信息通过虚拟卡片储存起来通过nfc方式被nfc读卡设备读取，这样就可以把现实中的卡片都存储到支持nfc的手机中去）。当前银行的芯片ic卡支持nfc，在手机支付宝的nfc手机上可以读取芯片ic卡的信息。

### android标签调度系统

1. 解析 NFC 标签并确定 MIME 类型或 URI（后者用于标识标签中的数据负载）。
2. 将 MIME 类型或 URI 与负载一起封装到 Intent 中。[如何将 NFC 标签映射到 MIME 类型和 URI](https://developer.android.com/guide/topics/connectivity/nfc/nfc.html#ndef) 中介绍了前两个步骤。
3. 根据 Intent 启动 Activity。[如何将 NFC 标签分发到应用](https://developer.android.com/guide/topics/connectivity/nfc/nfc.html#dispatching)中介绍了此步骤。













