<template>
  <div>
      <DetailBanner
      :sightName="sightName"
      :bannerImg="bannerImg"
      :gallaryImgs="gallaryImgs"
      ></DetailBanner>
      <DetailHeader></DetailHeader>
      <div class="contaniner">
        <DetailList :categoryList="categoryList"></DetailList>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
import DetailList from './components/List'
export default {
  name: 'Detail',
  components: {
    DetailBanner,
    DetailHeader,
    DetailList
  },
  data () {
    return {
      sightName: '',
      bannerImg: '',
      gallaryImgs: [],
      categoryList: []
    }
  },
  methods: {
    getDetailInfo () {
      axios.get('/api/detail.json?id+', {
        params: {
          id: this.$route.params.id
        }
      }).then(this.handleGetDataSucc)
    },
    handleGetDataSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.sightName = data.sightName
        this.bannerImg = data.bannerImg
        this.gallaryImgs = data.gallaryImgs
        this.categoryList = data.categoryList
        // console.log(data)
      }
    }
  },
  mounted () {
    this.getDetailInfo()
  }
}
</script>

<style lang="stylus" scoped>
.contaniner
  height 50rem
</style>
