<template>
  <div>
    <div class="content-box">
      <span class="text">节流指令: 在等待时间内多次触发事件, 只会执行一次函数, 但是如果重复触发事件不会重新计算等待时间. </span>
    </div>
    <div class="content-box">
      <el-button v-throttle="{ fn: throttleClick, wait: 1000 }" type="primary"> 节流按钮 (1 秒后执行) </el-button>
    </div>
  </div>
</template>

<script setup name="Throttle">
import { ElMessage } from 'element-plus'
/**
 * v-throttle
 * 按钮防抖指令，可自行扩展至input
 * 接收参数：function类型
 */
const vThrottle = {
  mounted(el, binding) {
    if (typeof binding.value.fn !== "function") {
      throw "callback must be a function";
    }
    let timer = null;
    el.__handleClick__ = function () {
      if (timer) {
        clearTimeout(timer);
      }
      if (!el.disabled) {
        el.disabled = true;
        binding.value.fn();
        timer = setTimeout(() => {
          el.disabled = false;
        }, binding.value.wait);
      }
    };
    el.addEventListener("click", el.__handleClick__);
  },
  beforeUnmount(el) {
    el.removeEventListener("click", el.__handleClick__);
  }
};

const throttleClick = () => {
  ElMessage.success("我是节流按钮触发的事件 🍍🍓🍌");
};
</script>

<style lang="scss">
.content-box {
  display: flex;
  justify-content: center;
  margin-top: 5%;
}
</style>