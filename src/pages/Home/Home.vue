<template>
  <div>
      <HomeHeader></HomeHeader>
      <HomeSwiper :list="swiperList"></HomeSwiper>
      <HomeIcons :list="iconList"></HomeIcons>
      <HomeRecommend :list="recommendList"></HomeRecommend>
      <HomeWeenkend :list="weekendList"></HomeWeenkend>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import axios from 'axios'
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeenkend from './components/Weekend'
export default {
  name: 'Home',
  data () {
    return {
      lastCity: '',
      swiperList: [],
      recommendList: [],
      iconList: [],
      weekendList: []
    }
  },
  computed: {
    ...mapState(['city'])
  },
  components: {
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeenkend
  },
  methods: {
    getHomeInfo () {
      axios.get('/api/index.json?city=' + this.city)
        .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.swiperList = data.swiperList
        this.recommendList = data.recommendList
        this.iconList = data.iconList
        this.weekendList = data.weekendList
      }
    }
  },
  mounted () {
    this.lastCity = this.city
    this.getHomeInfo()
  },
  activated () {
    if (this.lastCity !== this.city) {
      this.lastCity = this.city
      this.getHomeInfo()
    }
  }
}
</script>

<style>

</style>
