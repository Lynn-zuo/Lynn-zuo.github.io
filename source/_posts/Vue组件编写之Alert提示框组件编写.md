---
title: Alert提示框的vue局部组件编写
date: 2020-05-11 18:43:32
tags: [Vue]
categories: 学习
---
## Alert提示框的vue局部组件编写

最近一直学习vue，跟着视频敲代码，敲了两三个组件后，终于对编写组件有一个大致的思路了，以下通过编写一个alert提示框组件大致梳理一下我编写组件的思路。
主要分为三个部分：组件引入(注册路由器)、定义组件内容样式及实现组件间通信。

(注册路由器使用路由组件也可放到最后一步，个人习惯先引入然后定义组件及样式便于观察组件显示效果)

下面是引入本组件使用显示效果，通过登匹配验证为false触发alert提示框显示，点击确认关闭提示框：
<!--more-->

![alert提示框显示效果](alert.jpg "alert提示框显示效果")

#### 组件引入
一种是写入路由，要先在在router.js中配置路由：
```
routes: [{path:'', component:''}]]
```
通过路由组件标签
```<router-link to="/" />```
注册路由器;
另一种是通过import方式在父组件中引入，通过路由组件标签
```<router-view />```注册路由器，本文通过第二种方式注册路由器：


```
import AlertTip from '@/components/AlertTip'

export default {
  components: {
    AlertTip // 忘记会报错：'AlertTip' is defined but never used 
  }
}
```

#### 定义组件内容及样式
本文演示的alert提示框组件的定义内容如下：

```
<div id="dialog" class="dialog_container">
<!--提示框容器-->
    <section class="alert_container">
      <!--提示内容容器-->
      <div class="alert_content">
        <div class="tip_icon">
          <i class="el-icon-warning"></i>
          <span>提示信息</span>
        </div>
        <!--提示信息，接收父组件传来的参数-->
        <p class="tip_text">{{alertText}}</p>
      </div>
      <!--确认事件传递回父组件-->
      <button class="confirm" @click="closeTip">确认</button>
    </section>
  </div>
```
提示框主要样式——实现提示框位置及显示，一般采用的样式书写方式如下：

```
.dialog_container {
  // 提示框位置及显示一般样式
  position: fixed;
  z-index: 9999; // 最上层
  left:50%;
  top:50%;
}
```
提示框内提示文本及按钮样式根据类标签选择器自行编写。

#### 组件间通信
引入组件并定义好组件内容样式之后，要考虑的就是组件间通过参数传递进行通信。主要是父组件向子组件传递提示文本，子组件向父组件传递按钮点击事件状态。本文所演示提示框组件主要是通过自定义事件进行父子组件间通信。

```
 props: {
    alertText: String // 初始化显示声明类型
  },
  methods: {
    closeTip () {
      // 分发自定义事件（事件名:closeTip）
      this.$emit('closeTip')
    }
  }
```
在父组件中引入子组件时添加需要传递的参数及事件：

```
<AlertTip :alertText="alertText" v-show="alertShow" @closeTip="closeTip"/>
```
在父组件中通过调用showAlert()方法传入alertText参数值:

```
showAlert (alertText) {
  this.alertShow = true, // 是否显示提示框组件
  this.alertText = alertText
}
```

至此，将代码整合到一起，就得到一个可以动态显示的提示框组件了。
目前还是前端小白一枚，所以不足之处还希望大家多多指正呀！
