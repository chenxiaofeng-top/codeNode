## 设计

- ### 模块

  1. **后台js（service_worker）**，用于全局处理事件，拥有的权限比较大。
     - 可以理解为项目开发的**后端**，提供相应的**接口**。
     - 可调用chrome的所有api
     - 用于接收popup页面及页面js的调用
     - 也可以主动发信息给到popup页面及页面js，但比较麻烦，需要定位到哪个标签
  2. popup页面，即浏览器右上角的的扩展图标点击之后弹出的页面
     - 可以理解为用户的后台，一个简单的配置页面，主要向后端（service_worker）发送用户选择的配置信息
     - 可调用chrome部分api
     - 可以引用其它js文件，如jquery.js
  3. 内容js
     - 注入到页面的js,共享dom，但与页面的js分离，独立运行
     - 可操作dom
     - 可调用chrome少量api
     - 可以引用其它js文件，如jquery.js
     - 可以service_worker发送请求
  4. manifest.json
     - 文件清单
     - 指定可以使用的权限
     - 指定app各种信息，如果名称，图标，版本号等等

  

- ## 文档

  - 直接看https://developer.chrome.com/docs/extensions/
  - api不断更新，需要看源文档。
  - 理解了模块中的用途，需要什么功能就查下当时的文档

