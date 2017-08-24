<template>
  <div class="recommend" ref="recommend">
    <!-- 这里的:data是必要的，内部会watch这个变量来重新计算scroll的高度 -->
    <scroll ref="scroll" class="recommend-content" :data="discList">
      <div>
        <!-- 这里v-if是必要的，因为只有recmmends里有数据时才会去计算scroll内部的高度 -->
        <div v-if="recommends.length" class="slider-wrapper" ref="sliderWrapper">
          <slider>
            <div v-for="item in recommends">
              <a :href="item.linkUrl">
                <img class="needsclick" @load="loadImage" :src="item.picUrl">
              </a>
            </div>
          </slider>
        </div>
        <div class="recommend-list">
          <h1 class="list-title">热门歌单推荐</h1>
          <ul>
            <li @click="selectItem(item)" v-for="item in discList" class="item">
              <div class="icon">
                <img width="60" height="60" v-lazy="item.imgurl">
              </div>
              <div class="text">
                <h2 class="name" v-html="item.creator.name"></h2>
                <p class="desc" v-html="item.dissname"></p>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div class="loading-container" v-show="!discList.length">
        <loading></loading>
      </div>
    </scroll>
    <router-view></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import Slider from 'base/slider/slider'
  import Loading from 'base/loading/loading'
  import Scroll from 'base/scroll/scroll'
  import {getRecommend, getDiscList} from 'api/recommend'
  import {playlistMixin} from 'common/js/mixin'
  import {ERR_OK} from 'api/config'
  import {mapMutations} from 'vuex'

  export default {
    mixins: [playlistMixin],
    data() {
      return {
        recommends: [],     // 轮播图片资源
        discList: []        // 推荐歌曲列表
      }
    },
    created() {
        // 以下均为异步操作，不能确定哪个先获取到，这里处理的时候要小心
      this._getRecommend()

      this._getDiscList()
    },
    methods: {
      handlePlaylist(playlist) {
        const bottom = playlist.length > 0 ? '60px' : ''

        this.$refs.recommend.style.bottom = bottom
        this.$refs.scroll.refresh()
      },
      loadImage() { // 图片加载完成后，让scroll组件重新计算高度，由于图片高度都是一样的，所以仅需调用一次
        if (!this.checkloaded) {
          this.checkloaded = true
          this.$refs.scroll.refresh()
        }
      },
      selectItem(item) {  // 具体推荐歌曲的详情页路由
        this.$router.push({
          path: `/recommend/${item.dissid}`
        })
        this.setDisc(item)
      },
      _getRecommend() { // 请求轮播图片并初始化this.recommends
        getRecommend().then((res) => {
          if (res.code === ERR_OK) {
            this.recommends = res.data.slider
          }
        })
      },
      _getDiscList() { // 请求推荐歌单并初始化this.discList
        getDiscList().then((res) => {
          if (res.code === ERR_OK) {
            this.discList = res.data.list
          }
        })
      },
      ...mapMutations({
        setDisc: 'SET_DISC'
      })
    },
    components: {
      Slider,
      Loading,
      Scroll
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable"

  .recommend
    position: fixed
    width: 100%
    top: 88px
    bottom: 0
    .recommend-content
      height: 100%
      overflow: hidden
      .slider-wrapper
        position: relative
        width: 100%
        overflow: hidden
      .recommend-list
        .list-title
          height: 65px
          line-height: 65px
          text-align: center
          font-size: $font-size-medium
          color: $color-theme
        .item
          display: flex
          box-sizing: border-box
          align-items: center
          padding: 0 20px 20px 20px
          .icon
            flex: 0 0 60px
            width: 60px
            padding-right: 20px
          .text
            display: flex
            flex-direction: column
            justify-content: center
            flex: 1
            line-height: 20px
            overflow: hidden
            font-size: $font-size-medium
            .name
              margin-bottom: 10px
              color: $color-text
            .desc
              color: $color-text-d
      .loading-container
        position: absolute
        width: 100%
        top: 50%
        transform: translateY(-50%)
</style>
