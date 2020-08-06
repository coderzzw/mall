<template>
  <div class="wrapper" ref="wrapper">    <!-- 设置ref属性是为了准确拿到当前组件 如果用queryselctor拿到的可能不准确 -->
    <div class="content">
      <slot></slot>     <!-- 这里使用两个div嵌套是因为bscroll要求的格式 -->
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll';

export default {
  name: "Scroll",
  props: {
        probeType: {
          type: Number,
          default: 0
        }
      },
  data() {
    return {
      scroll: null,
    }
  },
  mounted() {
    // 1.创建BScroll对象
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,
      probeType: this.probeType     //这里可以直接给probType一个值, 但是有的地方需要实时监听又的地方不需要，所以封装起来，自己获取使用地方传来的值
    })
    // 2.监听滚动的位置
    this.scroll.on('scroll', (position) => {
      // console.log(position);   // position 就是实时的位置
      this.$emit('scroll', position)    // 通过自定义事件将当前位置发射出去
    })
  },

  methods: {
   scrollTo(x, y, time=300) {
     this.scroll && this.scroll.scrollTo(x, y, time)
   },
   refresh() {
     this.scroll && this.scroll.refresh();
   },
   getScrollY() {
     return this.scroll ? this.scroll.y : 0
   },

   /* finishPullUp() {
     this.scroll && this.finishPullUp()
   } */
  }
}
</script>

<style>

</style>