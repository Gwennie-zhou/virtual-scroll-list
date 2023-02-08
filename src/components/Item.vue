<template>
  <div class="item">
    <h3>{{ id }}</h3>
    <p>我是内容 ---{{ id }}</p>
  </div>
</template>

<script setup>
const props = defineProps({
  id: Number
})
</script>

<style>
.item {
  width: 600px;
  height: 200px;
  border-bottom: 1px solid black;
  box-sizing: border-box;
  padding: 40px;
}
</style>