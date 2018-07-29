<template lang="html">
  <div class="recommend">
    <div class="recommend-content">
      <div class="slide-wrapper">
        <slider v-if="recommends.length">
          <div class=""
            v-for="item of recommends"
            :key="item.id"
          >
            <a :href="item.linkUrl">
              <img :src="item.picUrl" />
            </a>
          </div>
        </slider>
      </div>
      <div class="recommend-list">
        <h1 class="list-title">热门歌单推荐</h1>
        <ul>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import { getRecommend } from 'api/recommend'
import { ERR_OK } from 'api/config'
import Slider from 'base/slider/slider'
export default {
  name: 'recomend',
  data () {
    return {
      recommends: []
    }
  },
  components: {
    Slider
  },
  methods: {
    _getRecommend () {
      getRecommend().then((res) => {
        if (res.code === ERR_OK) {
          console.log(res.data.slider)
          this.recommends = res.data.slider
        }
      })
    }
  },
  created () {
    this._getRecommend()
  }
}
</script>
<style lang="stylus" scoped>
@import "~common/stylus/variable"
  .recommend
    position: fixed
    width: 100%
    top: 80px
    bottom: 0
    background: #ccc
    .recommend-content
      height: 100%
      background: #999
      overflow: hidden
      .slide-wrapper
        position: relative
        width: 100%
        overflow: hidden
        background: #666
      .recommend-list
        .list-title
          height: 65px
          line-height: 65px
          text-align: center
          font-size: $font-size-medium
          color: $color-theme
          background: #333
</style>
