## 虚拟DOM
### 虚拟DOM的产生背景：
    * 程序越来越复杂，DOM操作越来越频繁
    * 需要监听的事件 ↑
    * 在事件回调中更新页面的DOM操作 ↑
### 虚拟DOM的功能

## 浏览器绘制页面的过程
1. 计算 CSS 规则树。
2. 生成 Render 树。
3. 计算各个节点的大小/position/z-index。（回流时触发3，4）
4. 绘制。（重绘时触发4）

## Dom和Bom
由于BOM的window包含了document，换个角度讲，BOM包含了DOM(对象)