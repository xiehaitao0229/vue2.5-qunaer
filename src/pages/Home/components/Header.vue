<template>
  <div class="header">
      <div class="header-left">
          <span class="iconfont back-icon">&#xe624;</span>
      </div>
      <div class="header-input">
           <span class="iconfont">&#xe632;</span>
          输入城市/景点/游玩主题
          </div>
      <router-link to="/city">
        <div class="header-right">
          {{this.city}}
           <span class="iconfont arrow-icon">&#xe64a;</span>
        </div>
      </router-link>
  </div>
</template>

<script>
import {mapState} from 'vuex'
export default {
  name: 'homeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>

<style lang="stylus" scoped>
    @import '~styles/varibles.styl'
    .header
        display: flex
        line-height .86rem
        color #fff
        background $bgColor
        .header-left
            width 0.64rem
            float left
            .back-icon
                text-align center
                font-size .4rem
        .header-input
            padding-left .2rem
            flex 1
            background #ffffff
            border-radius .1rem
            margin-top .12rem
            margin-left .2rem
            height 0.64rem
            line-height .64rem
            color #ccc
        .header-right
            min-width 1.04rem
            padding 0 .1rem
            text-align center
            color #ffffff
            .arrow-icon
                margin-left -.04rem
                font-size .24rem
</style>
