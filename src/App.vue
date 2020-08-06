<template>
  <div id="app" class="wrapper">
    <keep-alive exclude="Detail">   <!-- keep-alive是为了保证组件不自动新建 但是Detail组件需要不断刷新，因为每次获取的商品数据都不同 -->
      <router-view></router-view>
    </keep-alive>
    <main-tab-bar></main-tab-bar>
  </div>
</template>

<script>
  import MainTabBar from './components/content/mainTabbar/MainTabBar'
  export default {
    name: 'App',
    components: {
      MainTabBar
    }
  }
</script>

<style>
  @import "./assets/css/base.css";   /*在style中引用文件必须加@符号*/
</style>
