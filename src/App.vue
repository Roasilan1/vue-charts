<template>
  <Echarts class="charts"  :seriesData="[{name:'mon',value:30},{name:'tue',value:20}]" :extraOptions="{}"></Echarts>
</template>

<script>
import Echarts from '@/components/Echarts/Echarts.vue'

export default {
  components:{
    Echarts
  },
  mounted() {
    console.log(Echarts);
  },
}
</script>

<style scoped>
  .charts{
    width: 400px;
    height: 600px;
  }
</style>