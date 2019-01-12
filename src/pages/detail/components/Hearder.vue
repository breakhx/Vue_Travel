<template>
  <div>
    <router-link
      tag="div"
      to="/"
      class="hearder-abs"
      v-show="showabs"
    ><div class="iconfont hearder-abs-icon">&#xe624;</div></router-link>
    <div
      class="hearder-fixed"
      v-show="!showabs"
      :style="opacityStyle"
    >
      <router-link to="/">
        <div class="iconfont hearder-fixed-back">&#xe624;</div>
      </router-link>
      景点详情
    </div>
  </div>
</template>

<script>
export default {
  name: 'Hearder',
  data () {
    return {
      showabs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handelScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity }
        this.showabs = false
      } else {
        this.showabs = true
      }
    }
  },
  mounted () {
    window.addEventListener('scroll', this.handelScroll)
  },
  unmounted () {
    window.removeEventListener('scroll', this.handelScroll)
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .hearder-abs
    position: absolute
    top: .2rem
    left: .2rem
    width: .8rem
    height: .8rem
    border-radius: .4rem
    background: rgba(0, 0, 0, .8)
    line-height: .8rem
    text-align: center
    .hearder-abs-icon
      color: #fff
      font-size: .4rem
  .hearder-fixed
    z-index: 2
    position: fixed
    top: 0
    left: 0
    right: 0
    height: $headerHeight
    line-height: $headerHeight
    text-align: center
    color: #fff
    background: $bgColor
    font-size: .32rem
    .hearder-fixed-back
      position: absolute
      left: 0px
      top: 0px
      width: .64rem
      font-size: .4rem
      text-align: center
      color: #fff
</style>
