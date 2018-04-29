<template>
    <div>
        <div class="banner" @click="handleBannerClick">
            <img class="banner-img" :src="bannerImg" alt="">
            <div class="banner-info">
                <div class="banner-title">{{this.sightName}}</div>
                <div class="banner-number">
                    <span class="iconfont arrow-icon">&#xe63d;</span>
                    {{this.gallaryImgs.length}}
                </div>
            </div>
        </div>
        <CommonFade>
            <CommonGallry
                :imgs="gallaryImgs"
                v-show="showGallry"
                @clone="handleGallryClose">
            </CommonGallry>
        </CommonFade>
    </div>
</template>

<script>
import CommonGallry from 'common/Gallry/Gallry'
import CommonFade from 'common/Fade/Fade'
export default {
  name: 'Banner',
  props: {
    sightName: String,
    bannerImg: String,
    gallaryImgs: Array
  },
  data () {
    return {
      showGallry: false
    }
  },
  components: {
    CommonGallry,
    CommonFade
  },
  methods: {
    handleBannerClick () {
      this.showGallry = true
    },
    handleGallryClose () {
      this.showGallry = false
    }
  }
}
</script>

<style lang="stylus" scoped>
    .banner
        overflow hidden
        position relative
        height 0
        padding-bottom 55%
        .banner-img
            width 100%
        .banner-info
            position absolute
            top 3.5rem
            left 0
            bottom 0
            right .5rem
            display flex
            line-height 0.6rem
            color #ffffff
            .banner-title
                flex 1
                padding-left .2rem
            .banner-number
                padding 0 .4rem
                line-height .4rem
                height 0.4rem
                border-radius .2rem
                background rgba(0,0,0,.8)
</style>
