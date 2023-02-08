<template>
  <VirtualScrollList v-bind="info" v-slot="slotProps">
    <item :id="slotProps.id"/>
  </VirtualScrollList>
  <!-- <div >
    <item v-for="(i, index) in info.dataSet" :id="i" :key="index"/>
  </div> -->
</template>

<script>
import Item from './components/Item.vue';
import VirtualScrollList from './components/VirtualScrollList.vue';
export default {
  name: 'App',
  data() {
    return {
      info: {
        height: 200, //单个item高度
        containerHeight: 600, // 容器高度
        dataSet: [...Array(10000).keys()] // 数据集
      }
    }
  },
  
  components: {
    Item,
    VirtualScrollList
  }
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  margin: 0;
}
</style>
