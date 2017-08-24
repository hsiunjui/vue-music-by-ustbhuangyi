<template>
  <div ref="wrapper">
    <slot></slot>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll'

  export default {
    props: {
      probeType: {        // 滚动的类型，1表示会派发事件，会截流
        type: Number,
        default: 1
      },
      click: {           // 是否允许在滚动上点击，可能和fastclick有冲突，可以用class="needsclick"解决
        type: Boolean,
        default: true
      },
      listenScroll: {   // 是否派发滚动事件
        type: Boolean,
        default: false
      },
      data: {
        type: Array,    // 传入的列表数据
        default: null
      },
      pullup: {         // 是否派发滚动到底部的事件，用于上拉加载
        type: Boolean,
        default: false
      },
      beforeScroll: {   // 是否派发列表滚动开始的事件
        type: Boolean,
        default: false
      },
      refreshDelay: {   // 当数据更新后，刷新scroll的延时
        type: Number,
        default: 20
      }
    },
    mounted() {
      setTimeout(() => {      // 20是保证dom已经ready
        this._initScroll()
      }, 20)
    },
    methods: {
      _initScroll() {
        if (!this.$refs.wrapper) {    // 确保dom已经就绪
          return
        }
        this.scroll = new BScroll(this.$refs.wrapper, {   // 在mounted时初始化一个better-scroll对象
          probeType: this.probeType,
          click: this.click
        })

        if (this.listenScroll) {      // 如果有监听就触发一个事件并把相关参数传出去
          let me = this
          this.scroll.on('scroll', (pos) => {
            me.$emit('scroll', pos)
          })
        }

        if (this.pullup) {
          this.scroll.on('scrollEnd', () => {       // 适应底部
            if (this.scroll.y <= (this.scroll.maxScrollY + 50)) {
              this.$emit('scrollToEnd')
            }
          })
        }

        if (this.beforeScroll) {        // 开始滚动之前钩子
          this.scroll.on('beforeScrollStart', () => {
            this.$emit('beforeScroll')
          })
        }
      },
      disable() {     // 禁用滚动
        this.scroll && this.scroll.disable()
      },
      enable() {      // 允许滚动
        this.scroll && this.scroll.enable()
      },
      refresh() {     // 刷新
        this.scroll && this.scroll.refresh()
      },
      scrollTo() {    // 滚动到固定位置
        this.scroll && this.scroll.scrollTo.apply(this.scroll, arguments)
      },
      scrollToElement() {   // 滚动到固定 dom
        this.scroll && this.scroll.scrollToElement.apply(this.scroll, arguments)
      }
    },
    watch: {
      data() {  // 监控容器内部高度变化
        setTimeout(() => {
          this.refresh()
        }, this.refreshDelay)
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">

</style>
