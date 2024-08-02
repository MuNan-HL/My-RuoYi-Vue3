<template>
  <div>
    <div class="content-box">
      <span class="text">复制指令 </span>
    </div>
    <div class="content-box">
      <el-input v-model="copyData" placeholder="请输入内容" style="width: 500px">
        <template #append>
          <el-button v-copy="copyData"> 复制 </el-button>
        </template>
      </el-input>
    </div>
  </div>
</template>

<script setup name="Copy">
import { ref } from "vue";
import { ElMessage } from "element-plus";

const vCopy = {
  mounted(el, binding) {
    el.copyData = binding.value;
    el.addEventListener("click", handleClick);
  },
  updated(el, binding) {
    el.copyData = binding.value;
  },
  beforeUnmount(el) {
    el.removeEventListener("click", handleClick);
  }
};

async function handleClick() {
  try {
    await navigator.clipboard.writeText(this.copyData);
    ElMessage({
      type: "success",
      message: "复制成功"
    });
  } catch (err) {
    console.error("复制操作不被支持或失败: ", err);
  }
}

const copyData = ref("我是被复制的内容 🍒 🍉 🍊");
</script>

<style lang="scss">
.content-box {
  display: flex;
  justify-content: center;
  margin-top: 5%;
}
</style>