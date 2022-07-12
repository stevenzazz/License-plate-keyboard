## 你的支持才是我更新维护的最大动力，麻烦支持一下点一个小星星哦~

请点击 [Github地址](https://github.com/xiatianFun/licensePlate.git)

<br/>

<br/>

<br/>

### 一款使用vue3编写的车牌键盘

- 请确保安装node taro vue nutui(使用到了一个nut-popup组件 也可以无需安装nutui自行替换popup组件或其他方式)
- 本项目用taro编写 实际语法跟vue3差不多 所以同样适用于其他vue3项目

<br/>

## 使用方法

复制 components/licensePlate/index 代码到自己的项目中 如不想使用nutui 请替换popup组件

<br/>

app.js：

```javascript
import { createApp } from 'vue'
import { Popup, OverLay } from '@nutui/nutui-taro';

const App = createApp()

App.use(Popup).use(OverLay)

export default App

```

使用组件：

```javascript
<script setup>
  import { ref } from 'vue'
  import licensePlate from '@/components/licensePlate'
  const licensePlateRef = ref()
  
  // 调用此方法显示组件
  const handleClick = () => {
    licensePlateRef.value.showPopup()
  }
  
  // 车牌填写完成后 返回填写完成后的车牌号码
  const licensePlateConfirm = (value) => {
    console.log('接受到的车牌号',value);
  }

</script>
<template>
   <button type="primary" @click="handleClick">点我</button>
   <licensePlate ref="licensePlateRef" @confirm="licensePlateConfirm" />
</template>

```
