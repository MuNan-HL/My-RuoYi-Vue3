<template>
  <div class="content-box">
    <!-- 为 ECharts 准备一个定义了宽高的 DOM -->
    <!-- <div id="main" style="width: 100vw; height: 100vh;"></div> -->
    <ECharts :option="option"></ECharts>
  </div>
</template>

<script setup name="RadarChart">
import * as echarts from "echarts";
import "echarts-liquidfill";
import { ref, onMounted } from 'vue'
import ECharts from "../components/ECharts/index.vue"

// 配置图表的配置项
const option = {
  // 配置标题
  title: {
    text: "Basic Radar Chart",
    textStyle: {
      color: "#a1a1a1"
    }
  },
  // 配置图例
  legend: {
    data: ["Allocated Budget", "Actual Spending"],
    textStyle: {
      color: "#a1a1a1"
    }
  },
  // 配置雷达
  radar: {
    // 配置雷达形状
    // shape: 'circle',
    // 配置雷达显示器
    indicator: [
      { name: "Sales", max: 6500 },
      { name: "Administration", max: 16000 },
      { name: "Information Technology", max: 30000 },
      { name: "Customer Support", max: 38000 },
      { name: "Development", max: 52000 },
      { name: "Marketing", max: 25000 }
    ]
  },
  // 配置系列
  series: [
    {
      name: "Budget vs spending",
      type: "radar",
      // 配置系列数据
      data: [
        {
          value: [4200, 3000, 20000, 35000, 50000, 18000],
          name: "Allocated Budget"
        },
        {
          value: [5000, 14000, 28000, 26000, 42000, 21000],
          name: "Actual Spending"
        }
      ]
    }
  ]
};
</script>

<style lang="scss" scoped>
.content-box {
  display: flex;
  justify-content: space-between;
  height: 50vh;
  .ECharts {
    height: 50%;
  }
}
</style>