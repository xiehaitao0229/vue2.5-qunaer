<template>
   <div class="wrapper">
    <swiper :options="swiperOption" v-if="showSwiper">
    <!-- slides -->
    <swiper-slide v-for="item of list" :key="item.id">
        <img class="swiper-img" :src="item.imgUrl">
    </swiper-slide>
    <!-- Optional controls -->
    <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
   </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      }
    }
  },
  computed: {
    showSwiper () {
      return this.list.length
    }
  }
}
</script>

<style scoped lang="stylus">
    .wrapper >>> .swiper-pagination-bullet-active
        background red !important
    .wrapper
        width 100%
        height 0
        overflow hidden
        padding-bottom 31.25%
        background #eeeeee
        .swiper-pagination-bullets
          color #fff
        .swiper-img {
            width: 100%;
}
</style>
