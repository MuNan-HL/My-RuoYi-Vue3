<template>
  <div class="content-box">
    <span class="text">长按指令 🍇🍇🍇🍓🍓🍓</span>
    <el-button v-longpress="longpress" type="primary"> 长按5秒触发事件 </el-button>
  </div>
</template>

<script setup name="Longpress">
import { ElMessage } from "element-plus";

const vLongpress = {
  mounted(el, binding) {
    if (typeof binding.value !== "function") {
      throw "callback must be a function";
    }
    // 定义变量, 存储定时器编号
    let pressTimer = null;
    // 创建计时器（ 5秒后执行函数 ）
    const start = (e) => {
      if (e.button) {
        if (e.type === "click" && e.button !== 0) {
          return;
        }
      }
      if (pressTimer === null) {
        pressTimer = setTimeout(() => {
          handler(e);
        }, 5000);
      }
    };
    // 取消计时器
    const cancel = () => {
      if (pressTimer !== null) {
        clearTimeout(pressTimer);
        pressTimer = null;
      }
    };
    // 运行函数
    const handler = (e) => {
      binding.value(e);
    };
    // 添加事件监听器
    el.addEventListener("mousedown", start);
    el.addEventListener("touchstart", start);
    // 取消计时器
    el.addEventListener("click", cancel);
    el.addEventListener("mouseout", cancel);
    el.addEventListener("touchend", cancel);
    el.addEventListener("touchcancel", cancel);
  }
};

const longpress = () => {
  ElMessage({
    type: "success",
    message: "长按事件触发成功 🎉🎉🎉"
  })
};
</script>

<style scoped lang="scss">
.content-box {
  display: flex;
  justify-content: center;
  margin-top: 5%;
}
</style>
