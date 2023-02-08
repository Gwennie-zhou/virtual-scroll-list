<script setup>
import { computed, onMounted, ref } from 'vue';

const props = defineProps({
  height: Number,
  containerHeight: Number,
  dataSet: Array
})

const originalList = computed(() => props.dataSet)

// 容器内可见的item个数
const visibleItemCount = Math.ceil(props.containerHeight / props.height)
// 为平滑滚动多出的显示节点个数
// const extraPadItemCount = 3
const extraPadItemCount = Math.ceil(visibleItemCount / 2)

const renderItemCount = visibleItemCount + 2 * extraPadItemCount

const contentHeight = originalList.value.length * props.height

const scrollTop = ref(0)

let startIndex = computed(() => {
  let startNode = Math.floor(scrollTop.value / props.height) - extraPadItemCount
  return Math.max(startNode, 0)
})

let endIndex = computed(() => {
  let endNode = startIndex.value + renderItemCount
  return Math.min(endNode, originalList.value.length)
})

let newList = computed(() => originalList.value.slice(startIndex.value, endIndex.value + 1))

const offsetY = computed(() => startIndex.value * props.height)
// const bottomPadHeight = computed(() => contentHeight - offsetY.value - props.containerHeight)

onMounted(() => {
  console.log(startIndex.value, endIndex.value, originalList.value.slice(1, 10));
})

const handleScroll = (e) => {
  scrollTop.value = e.target.scrollTop
}




</script>

<template>
  <div class="scroll-container" :style="{ height: containerHeight + 'px' }" @scroll="handleScroll">
    <div class="scroll-content" :style="{ height: contentHeight + 'px' }">
      <!-- <div :style="{ padding: `${offsetY}px 0 ${bottomPadHeight}px` }"> -->
      <div :style="{ transform: `translateY(${offsetY}px)` }" class="render-items">
        <template v-for="(item, index) in newList" :key="index">
          <slot :id="item"></slot>
        </template>
      </div>
    </div>
  </div>
</template>


<style scoped>
.scroll-container {
  background: rgb(180, 180, 121);
  overflow-y: auto;
}
</style>