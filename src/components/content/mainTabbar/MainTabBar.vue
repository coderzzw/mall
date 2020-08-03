<template>
  <tab-bar>
    <tab-bar-item path="/home">
        <img slot="item-icon" src="../../../assets/img/tabbar/home1.jpg" alt="">
        <img slot="item-icon-active" src="../../../assets/img/tabbar/home.jpg" alt="">
        <div slot="item-text">首页</div>
      </tab-bar-item>
      <tab-bar-item path="/category">
        <img slot="item-icon" src="../../../assets/img/tabbar/fenlei1.jpg" alt="">
        <img slot="item-icon-active" src="../../../assets/img/tabbar/fenlei.jpg" alt="">
        <div slot="item-text">分类</div>
      </tab-bar-item>
      <tab-bar-item path="cart">
         <img  slot="item-icon" src="../../../assets/img/tabbar/car.jpg" alt="">
         <img slot="item-icon-active" src="../../../assets/img/tabbar/car1.jpg" alt="">
        <div slot="item-text">购物车</div>
      </tab-bar-item>
      <tab-bar-item path="profile">
         <img  slot="item-icon" src="../../../assets/img/tabbar/user1.jpg" alt="">
         <img slot="item-icon-active" src="../../../assets/img/tabbar/user.jpg" alt="">
        <div slot="item-text">我的</div>
      </tab-bar-item>
  </tab-bar>
</template>

  <script>
    import TabBar from '../../common/tabbar/TabBar'
    import TabBarItem from '../../common/tabbar/TabBarItem'

    export default {
      name: "MainTabBar",
      components: {
        TabBar, TabBarItem
      }
    }
  </script>

<style scoped>

</style>
