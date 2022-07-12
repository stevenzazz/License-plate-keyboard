<script setup>
  import { ref } from 'vue'
  import licensePlate from '../../components/licensePlate'
  const licensePlateRef = ref()

  const handleClick = () => {
    licensePlateRef.value.showPopup()
  }

  const licensePlateConfirm = (value) => {
    console.log('接受到的车牌号',value);
  }

</script>
<template>
   <button type="primary" @click="handleClick">点我</button>
   <licensePlate ref="licensePlateRef" @confirm="licensePlateConfirm" />
</template>
