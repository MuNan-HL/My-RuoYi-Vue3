<template>
  <div class="content-box">
    <!-- 为 ECharts 准备一个定义了宽高的 DOM -->
    <!-- <div id="main" style="width: 100vw; height: 100vh;"></div> -->
    <ECharts :option="option"></ECharts>
  </div>
</template>

<script setup name="PieChart">
import * as echarts from "echarts";
import "echarts-liquidfill";
import { ref, onMounted } from 'vue'
import ECharts from "../components/ECharts/index.vue"

// 配置图表的配置项
const option = {
  // 配置工具提示，当鼠标悬停在图表元素上时显示的信息
  tooltip: {
    // 配置触发方式, 为点击图表项
    trigger: "item",
    // 配置提示框显示的格式，包括系列名、数据名、数据值和百分比
    formatter: "{a} <br/>{b} : {c} ({d}%)"
  },
  // 配置图例, 用于显示对应的系列
  legend: {
    left: "center",
    top: "bottom",
    // 配置图例数据, 和 series 系列中的 data 数据中的 name 名称对应
    data: ["rose 1", "rose 2", "rose 3", "rose 4", "rose 5", "rose 6", "rose 7", "rose 8", "rose 9"],
    textStyle: {
      color: "#a1a1a1"
    }
  },
  // 配置工具箱，包括标记、数据视图、还原、保存为图片等功能
  toolbox: {
    show: true,
    feature: {
      mark: { show: true },
      dataView: { show: true, readOnly: false },
      restore: { show: true },
      saveAsImage: { show: true }
    }
  },
  // 配置系列，每个系列对应一个图表。
  series: [
    {
      name: "Radius Mode",
      // 配置图表类型, 为饼图
      type: "pie",
      // 配置饼图的半径范围
      radius: [60, 280],
      // 配置饼图的中心位置
      center: ["50%", "50%"],
      // 配置饼图类型, 为南丁格尔玫瑰图
      roseType: "radius",
      // 配置饼图边缘圆角
      itemStyle: {
        borderRadius: 5
      },
      // 配置标签
      label: {
        show: true
      },
      // 配置强调状态下, 显示标签
      emphasis: {
        label: {
          show: true
        }
      },
      // 配置系列数据
      data: [
        { value: 40, name: "rose 1" },
        { value: 33, name: "rose 2" },
        { value: 28, name: "rose 3" },
        { value: 22, name: "rose 4" },
        { value: 20, name: "rose 5" },
        { value: 15, name: "rose 6" },
        { value: 12, name: "rose 7" },
        { value: 10, name: "rose 8" },
        { value: 5, name: "rose 9" }
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