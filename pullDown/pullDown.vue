<template>
  <div id="app" ref='wrapper'>
    <div class="inner">sdfasf</div>
    <div class="pullDown">{{pullTxt}}</div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'

export default {
  name: 'app',
  components: {
  },
  data() {
    return {
      pullTxt: '下拉刷新'
    }
  },
  mounted() {
    setTimeout(() => {
      this._initScroll()
    }, 20)
  },
  methods: {
    _initScroll() {
      const _this = this
      if (!this.$refs.wrapper) {
        return
      }
      this.scroll = new BScroll(this.$refs.wrapper, {
        probeType: 2,
        pullDownRefresh: {
          threshold: 40,
          stop: 40
        }
      })
      this.scroll.on('scroll', (pos) => {
        if(pos.y > 40) {
          this.pullTxt = '释放刷新'
        }
      })
      this.scroll.on('pullingDown', () => {
        console.log('pullingDown...')
        this.pullTxt = '加载中'
        setTimeout(() => {
          this.pullTxt = '下拉刷新'
          this.scroll.finishPullDown()
        }, 1600)
      })
    },
    enable() {
      this.scroll && this.scroll.enable()
    },
    disable() {
      this.scroll && this.scroll.disable()
    },
    refresh() {
      this.scroll && this.scroll.refresh()
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

html,
body {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

#app {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}



.inner {
  position: absolute;
  width: 100%;
  background: #ffffff;
  height: 3000px;
}

.pullDown {
  position: absolute;
  width: 100%;
  height: 50px;
  top: 0px;
}
</style>
