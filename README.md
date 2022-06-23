### 一款使用vue3编写的车牌键盘

- 请确保安装node vue3.2+ 
- 本项目用taro编写 实际语法跟vue3差不多
- 使用到了taro 一个popup相关组件 如需用到自己的非taro框架项目中 请替换popup组件 （components/licensePlate/index 59行）

<br/>

## 使用方法

复制 components/licensePlate/index 代码到自己的项目中 如非taro项目 请替换popup组件

<br/>

引入组件：

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
   <nut-button type="primary" @click="handleClick">点我</nut-button>
   <licensePlate ref="licensePlateRef" @confirm="licensePlateConfirm" />
</template>

```

## 项目效果
![](https://s3.bmp.ovh/imgs/2022/06/22/5d7674d86087e09b.png)
