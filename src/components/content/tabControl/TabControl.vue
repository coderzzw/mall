<template>
  <div class="tab-control">
    <div v-for="(item, index) in titles" 
    class="tab-control-item" 
    :class="{active: index === currentIndex}"  
    @click="itemClick(index)">    <!-- 选中变色 -->
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  props: {
    titles: {
      type: Array,
      dafault() {
        return []
      }
    }
  },
  data() {
    return {
      currentIndex: 0   //这个变量用于标记哪个item处于选中状态,当与index相等时就变色
    }
  },
  methods: {
    itemClick(index) {
      this.currentIndex = index;   // 同上
      this.$emit('tabClick', index);
    }
  }
}
</script>

<style>
  .tab-control {
    display: flex;
    text-align: center;
    font-size: 15px;
    height: 40px;
    line-height: 40px;
  }
  .tab-control-item {
    flex: 1;
  }
  .tab-control-item span {
    padding: 5px;
  }
  .active {
    color: rgb(221, 66, 66);
    
  }
  .active span {
     border-bottom: 2px solid rgb(221, 66, 66);
  }

</style>