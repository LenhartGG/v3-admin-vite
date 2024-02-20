<script setup>
import { ref, computed } from "vue"

const prop = defineprop({
  model: Object
})

const isOpen = ref(false)
const isFolder = computed(() => {
  return prop.model.children && prop.model.children.length
})

function toggle() {
  isOpen.value = !isOpen.value
}

function changeType() {
  if (!isFolder.value) {
    prop.model.children = []
    addChild()
    isOpen.value = true
  }
}

function addChild() {
  prop.model.children.push({ name: "new stuff" })
}
</script>

<template>
  <li>
    <div :class="{ bold: isFolder }" @click="toggle" @dblclick="changeType">
      {{ model.name }}
      <span v-if="isFolder">[{{ isOpen ? "-" : "+" }}]</span>
    </div>
    <ul v-show="isOpen" v-if="isFolder">
      <!--
        一个可以通过其“name”选项递归渲染自己的组件，
        (如果使用单文件组件，则从文件名推断)
      -->
      <TreeItem class="item" v-for="(model, index) in model.children" :key="index" :model="model" />
      <li class="add" @click="addChild">+</li>
    </ul>
  </li>
</template>
