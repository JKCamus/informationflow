<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <!-- 需要滚动的内容会被替换到slot里面 -->
      <slot></slot>
    </div>
  </div>
</template>
<script>
  import BScroll from 'better-scroll'
  export default {
    name: "Scroll",
    props: {
      probeType: {
        type: Number,
        default: 0
      },
      pullUpLoad: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        scroll: null,
      }
    },
    mounted() {
      //创建BScroll对象
      this.scroll = new BScroll(this.$refs.wrapper, {
        //   不为true，组件里的div等无法被点击
        click: true,
        probeType: this.probeType,
        pullUpLoad: this.pullUpLoad
      })
      //   2监听滚动事件。
      this.scroll.on('scroll', (position) => {
        this.$emit('scroll', position)
        // console.log(this.scroll);
      })
      this.scroll.on('pullingUp', () => {
        this.$emit('pulingUp')
      })
    },
    methods: {
      // 保留异步请求数据时刷新高度
      refresh() {
        this.scroll && this.scroll.refresh()
      },

    },
  }
</script>
<style scoped>
</style>