<template>
  <div id="app">
     <v-header :seller="seller"></v-header>
   <div class="tab border-1px">
     <div class="tab-item">
       <router-link to="/goods">商品</router-link>
       </div>
     <div class="tab-item">
       <router-link to="/ratings">评论</router-link>
       </div>
     <div class="tab-item">
       <router-link to="/seller">商家</router-link>
       </div>
   </div>
   <router-view></router-view>
  </div>
</template>

<script>
import header from '@/components/header/header.vue'
import axios from 'axios'
export default {
  data () {
    return {
      seller: {}
    }
  },
  components: {
    'v-header': header
  },
  created () {
    axios.get('/api/data.json')
      .then(res => {
        if (res.status === 200) {
          let data = res.data
          this.seller = data.seller
        } else {
          alert('请求数据失败')
        }
      })
  }
}
</script>

<style scoped lang="stylus">
@import './common/stylus/mixin.styl'
#app
  .tab
    display flex
    height 40px
    line-height 40px
    border-1px(rgba(7, 17, 27, .1))
    .tab-item
      flex 1
      text-align center
      >a
        display block
        font-size 14px
        color rgb(77, 85, 93)
      .router-link-active
        color rgb(240, 20, 20)
</style>
