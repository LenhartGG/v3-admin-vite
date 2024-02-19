<template>
  <div class="app-container center">
    <div
      v-for="(item, index) in ImageList"
      :key="index"
      class="solution-card transition"
      :class="{ 'is-active': index == curIndex }"
      :style="{ backgroundImage: 'url(' + item.src + ')' }"
      @mouseenter="(e) => mouseenterHandler(e, item, index)"
    >
      <p class="p1">{{ item.title }}</p>
      <p class="p2">{{ item.info }}</p>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue"

const ImageList = ref<any[]>([
  {
    title: "音视频通讯",
    src: "/src/assets/images/solution/solution1.jpg",
    info: "提供坚实的云端一体音视频 PaaS 能力"
  },
  {
    title: "游戏云",
    src: "/src/assets/images/solution/solution2.jpg",
    info: "致力于打造高质量、全方位生态的游戏云服务平台"
  },
  {
    title: "微搭低代码",
    src: "/src/assets/images/solution/solution3.jpg",
    info: "高性能低代码开发平台，拖拽式构建小程序及其他应用"
  },
  {
    title: "金融",
    src: "/src/assets/images/solution/solution4.jpg",
    info: "新基建、新连接、新服务，全面助力行业数字化转型"
  },
  {
    title: "制造业",
    src: "/src/assets/images/solution/solution5.jpg",
    info: "助力制造业实现生产透明化、办公无纸化、车间无人化"
  }
])
const curIndex = ref(0)

function mouseenterHandler(e: any, item: object, index: number) {
  console.log(e, item, index)
  curIndex.value = index
}
</script>

<style lang="scss" scoped>
.center {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.app-container {
  height: 500px;
  height: 500px;
  overflow: auto;
}

.solution-card {
  width: 192px;
  height: 426px;
  margin-right: 20px;
  padding: 20px;
  background-size: auto 100%;
  background-repeat: no-repeat;
  background-position: 100% 0;
  color: #fff;
  .p1 {
    font-size: 20px;
  }
  .p1 {
    font-size: 14px;
  }
}
.is-active {
  width: 460px;
  box-shadow: 8px 8px 20px rgba(55, 99, 170, 0.1), -8px -8px 20px #fff;
}
.transition {
  transition: width 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}
</style>
