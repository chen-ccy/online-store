<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>

  import BScroll from 'better-scroll'





  export default {
    name: "Scroll",
    props:{
      probeType: Number,
      pullUpLoad: Boolean
    },
    data(){
      return {
        scroll:null,
        pullupload:setTimeout(() => {
          this.scroll.finishPullUp()
        },1000)
      }
    },
    mounted(){
      setTimeout(this.__initScroll, 20)
    },
    methods:{
      __initScroll() {
        // 1.初始化BScroll对象
        if (!this.$refs.wrapper) return
        this.scroll = new BScroll(this.$refs.wrapper, {
          probeType: this.probeType,
          click: true,
          pullUpLoad: true
        })

        // 2.将监听事件回调
        this.scroll.on('scroll', pos => {
          this.$emit('scroll', pos)
        })

        // 3.监听上拉到底部
        this.scroll.on('pullingUp', () => {
          this.$emit('pullingUp')
        })
      },
      refresh() {
        this.scroll && this.scroll.refresh && this.scroll.refresh()
      },
      finishPullUp() {
        this.scroll && this.scroll.finishPullUp && this.scroll.finishPullUp()
      },
      scrollTo(x, y, time) {
        this.scroll && this.scroll.scrollTo && this.scroll.scrollTo(x, y, time)
      },
      scrollY(){
        return this.scroll ? this.scroll.y : 0
      }
    },

  }
</script>

<style scoped>

</style>