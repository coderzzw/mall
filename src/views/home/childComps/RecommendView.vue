<template>
  <div class="recommend">
    <div v-for="item in recommends" class="recommend-item">
      <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "RecommendView",
  props: {
    recommends: {
      type: Array,
      default() {
        return []
      }
    }
  }
}
</script>

<style>
  .recommend {
    display: flex;
    width: 100%;
    text-align: center;
    padding: 8px 0 12px 0;
    border-bottom: 8px solid #eee;
  }
  .recommend-item {
    flex: 1;
    font-size: 12px;
  }
  .recommend-item img {
    width: 70px;
    height: 70px;
    margin-bottom: 8px;
   }
</style>