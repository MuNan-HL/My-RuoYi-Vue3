<template>
  <div class="content-box">
    <span class="text">拖拽指令</span>
    <img v-drag src="./精灵.jpg" alt="粉色精灵">
  </div>
</template>

<script setup name="Drag">
const vDrag = {
  mounted: function (el) {
    // 拖拽预处理
    el.style.cursor = "move";
    el.style.position = "absolute";
    el.ondragstart = () => false;

    // 拖拽时的处理: 鼠标按下, 鼠标移动, 鼠标弹起
    el.onmousedown = function (e) {
      // 计算鼠标的起始位置时, 减去偏移量的原因是, 防止第二次拖拽元素时, 以元素最初位置作为起始位置.
      // 需要注意的时, 此时托转元素的父元素必须是定位元素, 因为偏移量是按照其定位的父元素计算的.
      let startX = e.pageX - el.offsetLeft;
      let startY = e.pageY - el.offsetTop;

      // 错误计算的方法
      // let startX = e.pageX;
      // let startY = e.pageY;
      document.onmousemove = function (e) {
        // 计算鼠标拖拽后的位置
        let endX = e.pageX - startX;
        let endY = e.pageY - startY;
        
        // 计算鼠标最大可拖拽距离.
        let maxX = el.parentNode.offsetWidth - el.offsetWidth;
        let maxY = el.parentNode.offsetHeight - el.offsetHeight;

        // 限制鼠标的拖拽区域
        if (endX < 0) {
          endX = 0;
        } else if (endX > maxX) {
          endX = maxX;
        }

        if (endY < 0) {
          endY = 0;
        } else if (endY > maxY) {
          endY = maxY;
        }
        el.style.left = endX + "px";
        el.style.top = endY + "px";
      };

      document.onmouseup = function () {
        document.onmousemove = document.onmouseup = null;
      };
    };
  }
};
</script>

<style scoped lang="scss">
@import "./index.scss"
</style>