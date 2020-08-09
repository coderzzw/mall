<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav" @titleClick="titleClick"></detail-nav-bar>
    <scroll ref="scroll" class="content">
      <detail-swiper :top-images="topImages"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
     <!--  <detail-goods-info :detailInfo="detailInfo"></detail-goods-info> -->     <!-- 加入详情图片加载影响其它部分的渲染导致bug -->
      <detail-param-info ref="params" :param-info="paramInfo"></detail-param-info>
      <detail-comment-info ref="comment" :comment-info="commentInfo"></detail-comment-info>
      <goods-list ref="recommend" :goods="recommends"></goods-list>
    </scroll> 
    <detail-bottom-bar  @addCart="addToCart"></detail-bottom-bar>
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'    // 顶部导航
import DetailSwiper from '../detail/childComps/DetailSwiper'    // 轮播图
import DetailBaseInfo from '../detail/childComps/DetailBaseInfo'    // 商品基本信息
import DetailShopInfo from '../detail/childComps/DetailShopInfo'    // 店铺信息
import DetailGoodsInfo from '../detail/childComps/DetailGoodsInfo'    // 商品详细信息
import DetailParamInfo from '../detail/childComps/DetailParamInfo'    // 商品参数
import DetailCommentInfo from '../detail/childComps/DetailCommentInfo'   // 评论信息
import GoodsList from '../../components/content/goods/GoodsList'   // 用于推荐商品的展示
import DetailBottomBar from '../detail/childComps/DetailBottomBar'   // 底部工具栏

import Scroll from '../../components/common/scroll/Scroll'
import {getDetail, Goods, Shop, GoodsParam, getRecommend} from '../../network/detail'    // 网络请求

export default {
  name: "Detail",
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    Scroll,
    DetailGoodsInfo,
    DetailParamInfo,
    DetailCommentInfo,
    GoodsList,
    DetailBottomBar
  },
  data() {
    return {
      iid: null,
      topImages: [],
      goods: {},
      shop: {},
      detailInfo: {},
      paramInfo: {},
      commentInfo: {},
      recommends: [],
      themeTopYs: []
      //getThemeTopY: null

    }
  },
  created() {
    // 1.拿到单个商品的id并保存
    this.iid = this.$route.params.iid  
    // 2.根据iid请求详情数据
    getDetail(this.iid).then(res => {
     // console.log(res);
      const data = res.result;
      // 2.1保存获取的顶部轮播图数据
      this.topImages = res.result.itemInfo.topImages
      // 2.2保存获取的商品信息
      this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
      // 2.3保存获取的店铺信息
      this.shop = new Shop(data.shopInfo)
      // 2.4保存获取的商品详情数据
      this.detailInfo = data.detailInfo
      // 2.5保存获取的参数信息
      this.paramInfo = new GoodsParam(data.itemParams.info, data.itemParams.rule)
      // 2.6评论信息
      if(data.rate.cRate !== 0) {    // 评论不为空才展示
        this.commentInfo = data.rate.list[0]
      }
    })
    // 3.请求推荐商品数据
    getRecommend().then(res => {
      
      this.recommends = res.data.list
    })
    // 4.给getThemeTopY赋值
    /* this.getThemeTopY = debouce(() => {
      
    })  */
  }, 
  methods: {
    detailImageLoad() {
      this.$refs.scroll.refresh()
    
      
      //this.themeTopYs = [];
      this.themeTopYs.push(0); 
      this.themeTopYs.push(this.$refs.params.$el.offsetTop); 
      this.themeTopYs.push(this.$refs.comment.$el.offsetTop); 
      this.themeTopYs.push(this.$refs.recommend.$el.offsetTop); 
      //console.log(this.themeTopYs);
      
    },
    titleClick(index) {
      //console.log(index);
      // 点击标题之后切换到对应内容
      this.themeTopYs.push(0); 
      this.themeTopYs.push(this.$refs.params.$el.offsetTop); 
      this.themeTopYs.push(this.$refs.comment.$el.offsetTop); 
      this.themeTopYs.push(this.$refs.recommend.$el.offsetTop); 
      //console.log(this.themeTopYs);

      this.$refs.scroll.scrollTo(0, -this.themeTopYs[index], 100)
      //console.log(this.themeTopYs[index]);
      
    },
    addToCart() {
    // 1.获取商品在购物车中所要展示信息
      const product = {};
      //console.log(this.goods);
      product.image = this.topImages[0];
      product.title = this.goods.title;
      product.desc = this.goods.desc;
      product.price = this.goods.oldPrice;
      product.iid = this.iid
     // console.log(product);
      
    // 2.将商品添加到购物车
      this.$store.commit('addCart', product)

    }
  }
}
</script>

<style scoped>
  #detail {
    position: relative;
    z-index: 9;
    background-color: #fff;     /* 盖住首页底部的导航栏 */
    height: 100vh;
  }
  .detail-nav {
    position: relative;
    z-index: 9;
    background-color: #fff;   /* 保证顶部导航栏不移动 */
  }
  .content {
    height: calc(100% - 44px);
  }
</style>