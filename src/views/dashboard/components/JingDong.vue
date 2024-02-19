<template>
  <div ref="JingDongBox" class="app-container center">
    <!-- <h2 class="mb10">Waterfall 瀑布流基本使用 (默认使用JS计算进行布局展示)</h2> -->
    <Waterfall
      ref="WaterfallBox"
      @wheel="handleScroll"
      :images="images"
      :columnCount="3"
      :columnGap="30"
      :width="1100"
      mode="CSS"
      backgroundColor="#F2F4F8"
    />
  </div>
</template>

<script setup lang="ts">
import Waterfall from "./JingDong/Waterfall.vue"
import { ref, onBeforeMount } from "vue"
import { getImageUrl } from "./JingDong/common.js"

const images = ref<any[]>([])
const JingDongBox = ref()
const WaterfallBox = ref()

function loadImages() {
  for (let i = 1; i <= 10; i++) {
    images.value.push({
      title: `image-${i}`,
      src: "/src/assets/images/" + getImageUrl(i) + ".jpg",
      price: "￥13900.00",
      info: "现代简约牛皮沙发三人位 Land意大利皮革皮艺沙发 【布料】颜色可选 双人位M【180cm】",
      comment: "5条评价"
    })
  }
  console.log(images.value)
}

onBeforeMount(() => {
  // 组件已完成响应式状态设置，但未创建DOM节点
  loadImages()
})

function handleScroll() {
  const dom1 = JingDongBox.value
  const { scrollHeight, clientHeight, scrollTop } = dom1
  const distance = scrollHeight - scrollTop - clientHeight

  // const scrollHeight = document.body.scrollHeight;
  // const scrollTop = document.body.scrollHeight || document.documentElement.scrollHeight;
  // const clientHeight = document.documentElement.clientHeight;
  // const distance = scrollHeight - scrollTop - clientHeight;
  // console.log(distance);
  if (distance <= 100) {
    loadImages()
  }
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

.bg {
  width: 400px;
  height: 300px;
}
</style>
