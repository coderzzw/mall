<template>
  <div id="home" class="wrapper">
    <nav-bar class="home-nav"><div slot="center">杰尼商城</div></nav-bar>
    
    <scroll class="content" ref="scroll" :probe-type="3" @scroll="contentScroll">
      <swiper>
      <swiper-item v-for="item in banners">
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
      </swiper-item>
      </swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control :titles="['流行', '新款', '精选']" @tabClick="tabClick"></tab-control>
      <goods-list :goods="goods[currentType].list"></goods-list> 
     
    </scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
  import NavBar from '../../components/common/navbar/NavBar';    //顶部导航
  import {getHomeMultidata, getHomeGoods} from '../../network/home';   // 网络请求
  /* import Swiper from '../../components/common/swiper/Swiper';
  import SwiperItem from '../../components/common/swiper/SwiperItem' */
  import {Swiper, SwiperItem} from '../../components/common/swiper';   // 轮播图
  
  import RecommendView from '../home/childComps/RecommendView';  // 处理请求返回数据
  import FeatureView from '../home/childComps/FeatureView';
  import TabControl from '../../components/content/tabControl/TabControl';   // 中间导航栏
  import Scroll from '../../components/common/scroll/Scroll';      // 滚动
  import BackTop from '../../components/content/backTop/BackTop';     // 回到顶部
  import GoodsList from '../../components/content/goods/GoodsList';    //商品数据

  export default {
    name: "Home",
    components: {
      NavBar,
      Swiper,
      SwiperItem,
      RecommendView,
      FeatureView,
      TabControl,
      GoodsList,
      Scroll,
      BackTop
    },
    data() {
      return {
        banners: [],    //顶部轮播图数据
        recommends: [],    // 中间流行数据
        goods: {               // 下方商品数据
          'pop': {page: 0, list:[]},   
          'new': {page: 0, list:[]},
          'sell': {page: 0, list:[]},
        },
        currentType: 'pop',   // 默认展示的数据类型
        isShowBackTop: false,    // 默认不显示回到顶部按钮

        saveY: 0
      }  
    },
    created() {
      // 1.请求轮播图与流行数据
      this.getHomeMultidata();
      // 2.请求下方商品数据
      this.getHomeGoods('pop');
      this.getHomeGoods('new');
      this.getHomeGoods('sell');
      
    },
    destroyed() {
      console.log(111);
      
    },
    activated() {
      this.$refs.scroll.scrollTo(0, this.saveY, 0)  
      this.$refs.scroll.refresh()
      
      },
    deactivated() {
      this.saveY = this.$refs.scroll.getScrollY();
    },
    methods: {
      // 1.根据点击按钮的不同选择要展示的数据类型
      tabClick(index) {
        switch(index) {
          case 0:
            this.currentType = 'pop';
            break;
          case 1:
            this.currentType = 'new';
            break;
          case 2:
            this.currentType = 'sell';
            break;
        }  
      },
      backClick() {
        this.$refs.scroll.scroll.scrollTo(0, 0);   // 通过给scroll组件设置ref属性拿到该组件， 然后拿到其中的scroll属性
      },
      contentScroll(position) {
        this.isShowBackTop = (-position.y) > 1000   // 通过拿到Scroll组件中的y轴的实时位置确定是否显示按钮
      },

      // 2.网络请求相关
      getHomeMultidata() {
        getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
                    // 函数执行完即销毁。变量就消失了
        })          // 为了得到服务器的数据，提前在data中定义变量存储数据，即将数据的内存地址赋给data中的变量
      },
      getHomeGoods(type) {
        const page = this.goods[type].page + 1;
        getHomeGoods(type, page).then(res => {
          this.goods[type].list.push(...res.data.list);    // 将请求到的数据保存到data中的指定数组里
          this.goods[type].page +1;     // 每次请求完数据后页面都要加1
        
          //this.$refs.scroll.finishPullUp()
        })
      }
    }         
  }
</script>

<style scoped>
  #home {
    padding-top: 44px;
    height: 100vh;   /* vh viewheight视口高度 100vh即百分百视口 50vh即50%视口 */
    position: relative;
  }

  .home-nav {
    background-color: rgb(221, 66, 66);
    color: white;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 99;
  }

  .content {
    overflow: hidden;
    position: absolute;
    top: 44px;
    bottom: 49px;

  }
</style>