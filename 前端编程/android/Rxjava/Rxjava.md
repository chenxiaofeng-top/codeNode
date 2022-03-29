## Rx模式

### 使用观察者模式

- 创建：Rx可以方便的创建事件流和数据流（数据发源的地方，可以多个数据源）
- 组合：Rx使用查询式的操作符组合和变换数据流（数据处理的地址，可以多个处理方式）
- 监听：Rx可以订阅任何可观察的数据流并执行操作（数据结果，通知监听者）

### 定议

- Observable:被观察者
- Observer:观察者
- subscribe:订阅（动作），与Observer（名字，订阅的人）一样的意思

### RxJava

在RxJava中，一个实现了*Observer*接口的对象可以订阅(*subscribe*)一个*Observable* 类的实例。订阅者(subscriber)对Observable发射(*emit*)的任何数据或数据序列作出响应。这种模式简化了并发操作，因为它不需要阻塞等待Observable发射数据，而是创建了一个处于待命状态的观察者哨兵，哨兵在未来某个时刻响应Observable的通知。

## 对象

### Single

Single类似于Observable，是Observable的简化版



