<template>
  <!-- 为 ECharts 准备一个定义了宽高的 DOM -->
  <div id="main" :style="style"></div>
</template>

<script setup name="ECharts">
import { ref, onMounted, onBeforeUnmount, watch, computed, markRaw, nextTick, onActivated } from "vue";
import echarts from "./config";

const props = defineProps({
  option: {
    type: Object,
    required: true,
    default: ()=>{}
  },
  style: {
    type: String,
    required: true,
    default: "width: 80%; height: 80%;"
  }
})

// 不再创建周期初始化 ECharts 图表, 是因为此时只是创建 Vue 实列和创建响应式数据, 并未挂载 DOM 元素到 el 选项上去, 因此可能导致 Initialize failed: invalid dom.
onMounted(()=>{
  // 基于准备好的 dom，初始化 echarts 实例
  const myChart = echarts.init(document.getElementById('main'));
  
  // 配置图表的配置项
  // const option = {};
  
  // 使用刚指定的配置项和数据显示图表。
  myChart.setOption(props.option);
})
</script>

<style>

</style>