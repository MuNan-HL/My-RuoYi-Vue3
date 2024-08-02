<template>
  <div v-waterMarker="{ text: '水印指令 🍇🍇🍇🍓🍓🍓', textColor: 'rgba(180, 180, 180, 0.6)' }" class="content-box">
  </div>
</template>

<script setup name="WaterMask">
const vWaterMarker = {
  mounted(el, binding) {
    addWaterMarker(binding.value.text, el, binding.value.font, binding.value.textColor);
  }
};
/*
  需求：给整个页面添加背景水印。

  思路：
    1、使用 canvas 特性生成 base64 格式的图片文件，设置其字体大小，颜色等。
    2、将其设置为背景图片，从而实现页面或组件水印效果
  
  使用：设置水印文案，颜色，字体大小即可
  <div v-waterMarker="{text:'版权所有',textColor:'rgba(180, 180, 180, 0.4)'}"></div>
*/
const addWaterMarker = (str, parentNode, font, textColor) => {
  // 水印文字，父元素，字体，文字颜色
  // 创建一个canvas元素
  let can = document.createElement("canvas");
  // 将canvas元素添加到父节点中
  parentNode.appendChild(can);
  // 设置canvas的宽度和高度
  can.width = 205;
  can.height = 140;
  // 隐藏canvas元素
  can.style.display = "none";
  // 获取canvas的2D绘图上下文
  let cans = can.getContext("2d");
  // 旋转画布，使水印文字倾斜
  cans.rotate((-20 * Math.PI) / 180);
  // 设置字体样式，默认为"16px Microsoft JhengHei"
  cans.font = font || "16px Microsoft JhengHei";
  // 设置文字颜色，默认为半透明的灰色
  cans.fillStyle = textColor || "rgba(180, 180, 180, 0.3)";
  // 设置文字对齐方式为左对齐
  cans.textAlign = "left";
  // 设置文字基线为中间对齐
  cans.textBaseline = "Middle";
  // 在canvas上绘制水印文字
  cans.fillText(str, can.width / 10, can.height / 2);
  // 将canvas转换为图片URL，并设置为父节点的背景图片
  parentNode.style.backgroundImage = "url(" + can.toDataURL("image/png") + ")";

};


</script>

<style scoped lang="scss">
.content-box {
  display: block;
  height: 100vh;
}
</style>
