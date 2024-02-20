<template>Mouse position is at {{ x }}, {{ y }}</template>

<script setup>
import { useMouse } from "./mouse.js"

const { x, y } = useMouse()
</script>

<style scoped lang="less"></style>
