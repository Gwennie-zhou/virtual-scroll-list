## 虚拟滚动列表
核心代码在src/components/VirtualScrollList.vue文件中

### 使用方式
```
<VirtualScrollList v-bind="info" v-slot="slotProps">
  <item :id="slotProps.id"/>
</VirtualScrollList>

data() {
  return {
    info: {
      height: 200, //单个item高度
      containerHeight: 600, // 容器高度
      dataSet: [...Array(10000).keys()] // 数据集
    }
  }
},

```

## 解说文档
https://medium.com/p/3a1c2562ca3