<template>
  <div class="content-box">
    <div class="canvas-box">
      <!-- 为 ECharts 准备一个定义了宽高的 DOM -->
      <!-- <div id="main" style="width: 100vw; height: 100vh;"></div> -->
      <ECharts :option="option"></ECharts>
    </div>
  </div>
</template>

<script setup name="LineChart">
import * as echarts from "echarts";
import "echarts-liquidfill";
import { ref, onMounted } from 'vue'
import ECharts from "../components/ECharts/index.vue"

// 配置图表的配置项
const option = {
  // 配置标题
  title: {
    text: "Stacked Area Chart",
    textStyle: {
      color: "#a1a1a1"
    }
  },
  // 配置工具提示
  tooltip: {
    // 配置触发方式, 触发方式为坐标轴触发
    trigger: "axis",
    // 配置指示器, 指示器指鼠标悬浮在坐标系上时出现的竖线、阴影区域等样式
    axisPointer: {
      // 配置指示器类型, 为十字准星
      type: "cross",
      label: {
        backgroundColor: "#6a7985"
      }
    }
  },
  // 配置图例
  legend: {
    // 配置图例数据
    data: ["Email", "Union Ads", "Video Ads", "Direct", "Search Engine"],
    textStyle: {
      color: "#a1a1a1"
    }
  },
  // 配置工具箱
  toolbox: {
    feature: {
      saveAsImage: {}
    }
  },
  // 配置网格
  grid: {
    left: "3%",
    right: "4%",
    bottom: "3%",
    // 配置是否包含坐标轴的标签
    containLabel: true
  },
  // 配置 x 轴
  xAxis: [
    {
      // 坐标轴类型为类目型
      type: "category",
      // 两端不显示间隙
      boundaryGap: false,
      // x轴数据
      data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
      axisLabel: {
        color: "#a1a1a1"
      }
    }
  ],
  // 配置 y 轴
  yAxis: [
    {
      // 坐标轴类型为数值型
      type: "value",
      axisLabel: {
        color: "#a1a1a1"
      }
    }
  ],
  // 配置系列, 一个系列就是一幅图
  series: [
    {
      // 系列名称
      name: "Email",
      // 系列类型为折线图
      type: "line",
      // 配置堆叠, 同个类目轴上配置相同的 stack 堆叠值, 可以实现堆叠放置
      stack: "Total",
      // 配置标签
      label: {
        show: true,
        position: "top"
      },
      // 区域样式配置
      // areaStyle: {},
      // 配置重点强调方式
      emphasis: {
        // 配置焦点, 高亮当前系列 
        focus: "series"
      },
      // 系列数据
      data: [120, 132, 101, 134, 90, 230, 210]
    },
    {
      name: "Union Ads",
      type: "line",
      stack: "Total",
      // areaStyle: {},
      emphasis: {
        focus: "series"
      },
      data: [220, 182, 191, 234, 290, 330, 310]
    },
    {
      name: "Video Ads",
      type: "line",
      stack: "Total",
      // areaStyle: {},
      emphasis: {
        focus: "series"
      },
      data: [150, 232, 201, 154, 190, 330, 410]
    },
    {
      name: "Direct",
      type: "line",
      stack: "Total",
      // areaStyle: {},
      emphasis: {
        focus: "series"
      },
      data: [320, 332, 301, 334, 390, 330, 320]
    },
    {
      name: "Search Engine",
      type: "line",
      stack: "Total",
      label: {
        show: true,
        position: "top"
      },
      // areaStyle: {},
      emphasis: {
        focus: "series"
      },
      data: [820, 932, 901, 934, 1290, 1330, 1320]
    }
  ]
};
</script>

<style lang="scss" scoped>
.content-box {
  height: 100vh;
  .canvas-box {
    height: 100%;
  }
}
</style>