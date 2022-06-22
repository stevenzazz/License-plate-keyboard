<script setup>
  import { ref } from 'vue'
  
  const licensePlateRef = ref()

  const handleClick = () => {
    licensePlateRef.value.showPopup()
  }

  const licensePlateConfirm = (value) => {
    console.log('接受到的车牌号',value);
  }

</script>
<template>
   <nut-button type="primary" @click="handleClick">点我</nut-button>
   <licensePlate ref="licensePlateRef" @confirm="licensePlateConfirm" />
</template>
