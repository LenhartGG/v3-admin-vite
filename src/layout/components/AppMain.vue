<script lang="ts" setup>
import { computed } from "vue"
import { useRoute } from "vue-router"
import { useTagsViewStore } from "@/store/modules/tags-view"

const route = useRoute()
const tagsViewStore = useTagsViewStore()

const key = computed(() => {
  // 返回 route.path 和 route.fullPath 有着不同的效果，大多数时候 path 更通用
  return route.path
})
</script>

<template>
  <section class="app-main">
    <div class="app-scrollbar">
      <keep-alive :include="tagsViewStore.cachedViews">
        <transition name="el-fade-in" mode="out-in">
          <router-view v-slot="{ Component }">
            <component :is="Component" :key="key" />
          </router-view>
        </transition>
      </keep-alive>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@import "@/styles/mixins.scss";

.app-main {
  min-height: calc(100vh - var(--v3-navigationbar-height));
  width: 100%;
  position: relative;
  overflow: hidden;
  background-color: var(--v3-body-bg-color);
}

.app-scrollbar {
  height: 100%;
  overflow: auto;
  @include scrollbar;
}

.fixed-header + .app-main {
  padding-top: var(--v3-navigationbar-height);
  height: 100vh;
  overflow: auto;
}

.hasTagsView {
  .app-main {
    min-height: calc(100vh - var(--v3-header-height));
  }
  .fixed-header + .app-main {
    padding-top: var(--v3-header-height);
  }
}
</style>
