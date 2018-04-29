<template>
  <ul class="list">
      <li
      class="item"
      @click="handleLetterClick"
      @touchstart.prevent="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
      v-for="item of letters"
      :key="item"
      :ref="item"
      >{{item}}</li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    Cities: Object
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null //  做点击move事件的函数节流
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop //  拿到A距离顶部的高度
  },
  computed: {
    //  构建一个字母表的数组
    letters () {
      const letters = []
      for (let i in this.Cities) {
        letters.push(i)
      }
      return letters
    }
  },
  methods: {
    handleLetterClick (e) {
      //  向父组件传递数据
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 79 //  79是头部的高度
          const index = Math.floor((touchY - this.startY) / 20)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
    .list
        display flex
        flex-direction column
        justify-content center
        position absolute
        right 0
        top 1.58rem
        bottom 0
        width 0.4rem
        .item
            text-align center
            line-height .4rem
            color $bgColor
</style>
