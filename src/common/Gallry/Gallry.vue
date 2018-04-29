<template>
  <div class="container" @click="handleGallryClick">
      <div class="wrapper">
        <swiper :options="swiperOptions">
            <!-- slides -->
            <swiper-slide v-for="(item,index) of imgs" :key="index">
                <img class="gallry-img" :src="item">
            </swiper-slide>
            <!-- Optional controls -->
            <div class="swiper-pagination"  slot="pagination"></div>
        </swiper>
      </div>
  </div>
</template>

<script>
export default {
  name: 'CommonGallry',
  props: {
    imgs: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      swiperOptions: {
        pagination: '.swiper-pagination',
        loop: true,
        paginationType: 'fraction',
        observerParents: true,
        observer: true
      }
    }
  },
  methods: {
    handleGallryClick () {
      this.$emit('clone')
    }
  }
}
</script>

<style lang="stylus" scoped>
    .container >>> .swiper-container
        overflow inherit
    .container
        display flex
        flex-direction column
        justify-content center
        position fixed
        left 0
        right 0
        top 0
        bottom 0
        z-index 99
        background #000
        .wrapper
            height 0
            width 100%
            padding-bottom 100%
            .gallry-img
                width 100%
            .swiper-pagination
                color #ffffff
                bottom -1rem
</style>
