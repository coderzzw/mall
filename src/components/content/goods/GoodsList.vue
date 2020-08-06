<template>
  <div class="goods">     <!-- :goodes-item="item" 将遍历出来的单独数据传给GoodsListItem组件-->
    <goods-list-item v-for="item in goods" :goods-item="item"></goods-list-item>
  </div>
</template>

<script>
import GoodsListItem from './GoodsListItem';

export default {
  name: "GoodsList",
  components: {
    GoodsListItem
  },
  props: {      //从Home组件中拿到数据
    goods: {
      type: Array,
      default() {
        return []
      }
    }
  }
}
</script>

<style>
  .goods {
    display: flex;
    flex-wrap: wrap;   /* 包裹，它会自动根据宽度决定一行展示几个 */
    justify-content: space-around;   /* 均等分 */
  }
</style>