<template>
  <div id="detail">
    <detail-nav-bar></detail-nav-bar>
    <detail-swiper :top-images="topImages"></detail-swiper>
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'    // 顶部导航
import DetailSwiper from '../detail/childComps/DetailSwiper'    // 轮播图
import {getDetail} from '../../network/detail'

export default {
  name: "Detail",
  components: {
    DetailNavBar,
    DetailSwiper
  },
  data() {
    return {
      iid: null,
      topImages: []
    }
  },
  created() {
    // 拿到单个商品的id并保存
    this.iid = this.$route.params.iid  
    // 根据iid请求详情数据
    getDetail(this.iid).then(res => {
      console.log(res);
    
    this.topImages = res.result.itemInfo.topImages
    })
  }
}
</script>

<style>

</style>