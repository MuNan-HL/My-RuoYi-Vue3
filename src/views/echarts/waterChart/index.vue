<template>
  <div class="content-box">
    <!-- 为 ECharts 准备一个定义了宽高的 DOM -->
    <!-- <div id="main" style="width: 100vw; height: 100vh;"></div> -->
    <ECharts :option="option"></ECharts>
  </div>
</template>

<script setup name="WaterChart">
import * as echarts from "echarts";
import "echarts-liquidfill";
import { ref, onMounted } from 'vue'
import ECharts from "../components/ECharts/index.vue"

// 配置图表的配置项
const option = {
title: [
  {
    text: "预约量",
    x: "25%",
    y: 30,
    textAlign: "center",
    textStyle: {
      color: "#a1a1a1",
      fontSize: 16,
      fontFamily: "Microsoft Yahei",
      fontWeight: "100",
      textAlign: "center"
    }
  },
  {
    text: "实时客流量",
    x: "75%",
    y: 30,
    textAlign: "center",
    textStyle: {
      color: "#a1a1a1",
      fontSize: 16,
      fontFamily: "Microsoft Yahei",
      fontWeight: "100",
      textAlign: "center"
    }
  },
  {
    text: (0.5 * 100).toFixed(0) + "%",
    left: "25%",
    top: "38%",
    textAlign: "center",
    textStyle: {
      fontSize: "50",
      fontWeight: "300",
      color: "#a06a0a",
      textAlign: "center",
      textBorderColor: "rgba(0, 0, 0, 0)",
      textShadowColor: "#fff",
      textShadowBlur: "0",
      textShadowOffsetX: 0,
      textShadowOffsetY: 1
    }
  },
  {
    text: (0.5 * 100).toFixed(0) + "%",
    left: "75%",
    top: "38%",
    textAlign: "center",
    textStyle: {
      fontSize: "50",
      fontWeight: "300",
      color: "#02456d",
      textAlign: "center",
      textBorderColor: "rgba(0, 0, 0, 0)",
      textShadowColor: "#fff",
      textShadowBlur: "0",
      textShadowOffsetX: 0,
      textShadowOffsetY: 1
    }
  }
],
series: [
  {
    type: "liquidFill",
    radius: "50%",
    z: 6,
    center: ["25%", "50%"],
    color: [
      {
        type: "linear",
        x: 0,
        y: 0,
        x2: 0,
        y2: 1,
        colorStops: [
          {
            offset: 1,
            color: "rgba(251, 173, 23, 0)"
          },
          {
            offset: 0.5,
            color: "rgba(251, 173, 23, .2)"
          },
          {
            offset: 0,
            color: "rgba(251, 173, 23, 1)"
          }
        ],
        globalCoord: false
      }
    ],
    data: [0.5, 0.5, 0.5],
    backgroundStyle: {
      borderWidth: 1,
      color: "transparent"
    },
    label: {
      normal: {
        formatter: ""
      }
    },
    outline: {
      show: true,
      itemStyle: {
        borderWidth: 0
      },
      borderDistance: 0
    }
  },
  {
    name: "第二层白边",
    type: "pie",
    z: 3,
    radius: ["0%", "55%"],
    center: ["25%", "50%"],
    hoverAnimation: false,
    itemStyle: {
      normal: {
        label: {
          show: false
        }
      }
    },
    data: [
      {
        value: 100,
        itemStyle: {
          normal: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
              {
                offset: 0,
                color: "#fefefe"
              },
              {
                offset: 1,
                color: "#e7e8ea"
              }
            ])
          }
        }
      },
      {
        value: 0,
        itemStyle: {
          normal: {
            color: "transparent"
          }
        }
      }
    ]
  },
  {
    name: "最外绿边",
    type: "pie",
    z: 1,
    radius: ["0%", "58%"],
    center: ["25%", "50%"],
    hoverAnimation: false,
    itemStyle: {
      normal: {
        label: {
          show: false
        }
      }
    },
    data: [
      {
        value: 100,
        itemStyle: {
          color: "#fdc56e"
        }
      },
      {
        value: 0,
        itemStyle: {
          normal: {
            color: "transparent"
          }
        }
      }
    ]
  },
  {
    type: "liquidFill",
    radius: "50%",
    z: 6,
    center: ["75%", "50%"],
    color: ["#c1dce7", "#90d3f0", "#009bdb"],
    data: [0.6, { value: 0.5, direction: "left" }, 0.4, 0.3],
    backgroundStyle: {
      borderWidth: 1,
      color: "transparent"
    },
    label: {
      normal: {
        formatter: ""
      }
    },
    outline: {
      show: true,
      itemStyle: {
        borderWidth: 0
      },
      borderDistance: 0
    }
  },
  {
    name: "第二层白边",
    type: "pie",
    z: 3,
    radius: ["0%", "55%"],
    center: ["75%", "50%"],
    hoverAnimation: false,
    itemStyle: {
      normal: {
        label: {
          show: false
        }
      }
    },
    data: [
      {
        value: 100,
        itemStyle: {
          normal: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
              {
                offset: 0,
                color: "#fefefe"
              },
              {
                offset: 1,
                color: "#e7e8ea"
              }
            ])
          }
        }
      },
      {
        value: 0,
        itemStyle: {
          normal: {
            color: "transparent"
          }
        }
      }
    ]
  },
  {
    name: "最外蓝边",
    type: "pie",
    z: 1,
    radius: ["0%", "58%"],
    center: ["75%", "50%"],
    hoverAnimation: false,
    itemStyle: {
      normal: {
        label: {
          show: false
        }
      }
    },
    data: [
      {
        value: 100,
        itemStyle: {
          color: "#07a2e3"
        }
      },
      {
        value: 0,
        itemStyle: {
          normal: {
            color: "transparent"
          }
        }
      }
    ]
  }
]
};

// // 不再创建周期初始化 ECharts 图表, 是因为此时只是创建 Vue 实列和创建响应式数据, 并未挂载 DOM 元素到 el 选项上去, 因此可能导致 Initialize failed: invalid dom.
// onMounted(()=>{
//   // 基于准备好的 dom，初始化 echarts 实例
//   const myChart = echarts.init(document.getElementById('main'));
  
//   // 配置图表的配置项
//   const option = {
//   title: [
//     {
//       text: "预约量",
//       x: "25%",
//       y: 30,
//       textAlign: "center",
//       textStyle: {
//         color: "#a1a1a1",
//         fontSize: 16,
//         fontFamily: "Microsoft Yahei",
//         fontWeight: "100",
//         textAlign: "center"
//       }
//     },
//     {
//       text: "实时客流量",
//       x: "75%",
//       y: 30,
//       textAlign: "center",
//       textStyle: {
//         color: "#a1a1a1",
//         fontSize: 16,
//         fontFamily: "Microsoft Yahei",
//         fontWeight: "100",
//         textAlign: "center"
//       }
//     },
//     {
//       text: (0.5 * 100).toFixed(0) + "%",
//       left: "25%",
//       top: "38%",
//       textAlign: "center",
//       textStyle: {
//         fontSize: "50",
//         fontWeight: "300",
//         color: "#a06a0a",
//         textAlign: "center",
//         textBorderColor: "rgba(0, 0, 0, 0)",
//         textShadowColor: "#fff",
//         textShadowBlur: "0",
//         textShadowOffsetX: 0,
//         textShadowOffsetY: 1
//       }
//     },
//     {
//       text: (0.5 * 100).toFixed(0) + "%",
//       left: "75%",
//       top: "38%",
//       textAlign: "center",
//       textStyle: {
//         fontSize: "50",
//         fontWeight: "300",
//         color: "#02456d",
//         textAlign: "center",
//         textBorderColor: "rgba(0, 0, 0, 0)",
//         textShadowColor: "#fff",
//         textShadowBlur: "0",
//         textShadowOffsetX: 0,
//         textShadowOffsetY: 1
//       }
//     }
//   ],
//   series: [
//     {
//       type: "liquidFill",
//       radius: "50%",
//       z: 6,
//       center: ["25%", "50%"],
//       color: [
//         {
//           type: "linear",
//           x: 0,
//           y: 0,
//           x2: 0,
//           y2: 1,
//           colorStops: [
//             {
//               offset: 1,
//               color: "rgba(251, 173, 23, 0)"
//             },
//             {
//               offset: 0.5,
//               color: "rgba(251, 173, 23, .2)"
//             },
//             {
//               offset: 0,
//               color: "rgba(251, 173, 23, 1)"
//             }
//           ],
//           globalCoord: false
//         }
//       ],
//       data: [0.5, 0.5, 0.5],
//       backgroundStyle: {
//         borderWidth: 1,
//         color: "transparent"
//       },
//       label: {
//         normal: {
//           formatter: ""
//         }
//       },
//       outline: {
//         show: true,
//         itemStyle: {
//           borderWidth: 0
//         },
//         borderDistance: 0
//       }
//     },
//     {
//       name: "第二层白边",
//       type: "pie",
//       z: 3,
//       radius: ["0%", "55%"],
//       center: ["25%", "50%"],
//       hoverAnimation: false,
//       itemStyle: {
//         normal: {
//           label: {
//             show: false
//           }
//         }
//       },
//       data: [
//         {
//           value: 100,
//           itemStyle: {
//             normal: {
//               color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
//                 {
//                   offset: 0,
//                   color: "#fefefe"
//                 },
//                 {
//                   offset: 1,
//                   color: "#e7e8ea"
//                 }
//               ])
//             }
//           }
//         },
//         {
//           value: 0,
//           itemStyle: {
//             normal: {
//               color: "transparent"
//             }
//           }
//         }
//       ]
//     },
//     {
//       name: "最外绿边",
//       type: "pie",
//       z: 1,
//       radius: ["0%", "58%"],
//       center: ["25%", "50%"],
//       hoverAnimation: false,
//       itemStyle: {
//         normal: {
//           label: {
//             show: false
//           }
//         }
//       },
//       data: [
//         {
//           value: 100,
//           itemStyle: {
//             color: "#fdc56e"
//           }
//         },
//         {
//           value: 0,
//           itemStyle: {
//             normal: {
//               color: "transparent"
//             }
//           }
//         }
//       ]
//     },
//     {
//       type: "liquidFill",
//       radius: "50%",
//       z: 6,
//       center: ["75%", "50%"],
//       color: ["#c1dce7", "#90d3f0", "#009bdb"],
//       data: [0.6, { value: 0.5, direction: "left" }, 0.4, 0.3],
//       backgroundStyle: {
//         borderWidth: 1,
//         color: "transparent"
//       },
//       label: {
//         normal: {
//           formatter: ""
//         }
//       },
//       outline: {
//         show: true,
//         itemStyle: {
//           borderWidth: 0
//         },
//         borderDistance: 0
//       }
//     },
//     {
//       name: "第二层白边",
//       type: "pie",
//       z: 3,
//       radius: ["0%", "55%"],
//       center: ["75%", "50%"],
//       hoverAnimation: false,
//       itemStyle: {
//         normal: {
//           label: {
//             show: false
//           }
//         }
//       },
//       data: [
//         {
//           value: 100,
//           itemStyle: {
//             normal: {
//               color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
//                 {
//                   offset: 0,
//                   color: "#fefefe"
//                 },
//                 {
//                   offset: 1,
//                   color: "#e7e8ea"
//                 }
//               ])
//             }
//           }
//         },
//         {
//           value: 0,
//           itemStyle: {
//             normal: {
//               color: "transparent"
//             }
//           }
//         }
//       ]
//     },
//     {
//       name: "最外蓝边",
//       type: "pie",
//       z: 1,
//       radius: ["0%", "58%"],
//       center: ["75%", "50%"],
//       hoverAnimation: false,
//       itemStyle: {
//         normal: {
//           label: {
//             show: false
//           }
//         }
//       },
//       data: [
//         {
//           value: 100,
//           itemStyle: {
//             color: "#07a2e3"
//           }
//         },
//         {
//           value: 0,
//           itemStyle: {
//             normal: {
//               color: "transparent"
//             }
//           }
//         }
//       ]
//     }
//   ]
//   };
  
//   // 使用刚指定的配置项和数据显示图表。
//   myChart.setOption(option);
// })
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