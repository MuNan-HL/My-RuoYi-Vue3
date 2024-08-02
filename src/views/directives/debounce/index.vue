<template>
  <div>
    <div class="content-box">
      <span class="text">防抖指令: 在等待时间内多次触发事件, 只会执行一次函数, 且如果重复触发事件会重新计算等待时间. </span>
    </div>
    <div class="content-box">
      <el-button v-debounce="{ fn: debounceClick, wait: 1000 }" type="primary"> 防抖按钮 (1 秒后执行) </el-button>
    </div>
  </div>
</template>

<script setup name="Debounce">
import { ElMessage } from 'element-plus'
/**
 * v-debounce
 * 按钮防抖指令，可自行扩展至input
 * 接收参数：function类型
 */
const vDebounce = {
  mounted(el, binding) {
    if (typeof binding.value.fn !== "function") {
      throw "callback must be a function";
    }
    let timer = null;
    el.__handleClick__ = function () {
      if (timer) {
        clearInterval(timer);
      }
      timer = setTimeout(() => {
        binding.value.fn();
      }, binding.value.wait);
    };
    el.addEventListener("click", el.__handleClick__);
  },
  beforeUnmount(el) {
    el.removeEventListener("click", el.__handleClick__);
  }
};

const debounceClick = () => {
  ElMessage.success("我是防抖按钮触发的事件 🍍🍓🍌");
};
</script>

<style lang="scss">
.content-box {
  display: flex;
  justify-content: center;
  margin-top: 5%;
}
</style>