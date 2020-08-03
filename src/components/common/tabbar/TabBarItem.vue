<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="isActive"><slot name="item-icon"></slot></div>
    <div v-else> <slot name="item-icon-active"></slot></div>
    <div :class="{active: isActive}"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  props: {
    path: String
  },
  data() {
    return {
      //isActive: true    
    
    }
  },
  computed: {
    isActive() {   // 动态决定图标与文字的颜色
      //  拿到活跃路由的path,判断里面是否有我自己的path
      return this.$route.path.indexOf(this.path) !== -1;   // 字符串方法indexOf == -1 表示里面不包含
    }
  },
  methods: {
    itemClick() {
      this.$router.push(this.path)  // 从父组件app中得到payh,不同path展示不同的item组件
    }
  }
}
</script>

<style>
  .tab-bar-item{
    flex: 1;      /* 使这四个item均分 */
    text-align: center; 
    height: 49px;
    font-size: 14px;
  }

  .tab-bar-item img{
    height: 24px;
    width: 24px;
  }
  .active {
    color: red;
  }
</style>


 