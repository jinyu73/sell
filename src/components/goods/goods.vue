<template>
    <div class="goods">
        <div class="menu-wrapper">
            <ul>
                <li v-for="(item, index) in goods" :key="index" class="menu-item">
                    <span class="text border-1px">
                        <span v-show="item.type>0" class="icon"
                            :class="classMap[item.type]"></span>{{item.name}}
                    </span>
                </li>
            </ul>
        </div>
        <div class="foods-wrapper"></div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: []
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    axios.get('/api/data.json')
      .then(res => {
        if (res.status === 200) {
          this.goods = res.data.goods
          console.log(this.goods)
        } else {
          alert('获取数据失败')
        }
      })
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin.styl'
.goods
    display flex
    position absolute
    width 100%
    top 174px
    bottom 46px
    overflow hidden
    .menu-wrapper
        flex 0 0 80px
        width 80px
        background #f3f5f7
        .menu-item
            display table
            height 54px
            width 56px
            padding 0 12px
            line-height 14px
            .icon
                display inline-block
                vertical-align top
                width 12px
                height 12px
                margin-right 2px
                background-size 12px 12px
                background-repeat no-repeat
                &.decrease
                    bg-image('decrease_3')
                &.discount
                    bg-image('discount_3')
                &.guarantee
                    bg-image('guarantee_3')
                &.invoice
                    bg-image('invoice_3')
                &.special
                    bg-image('special_3')
            .text
                display table-cell
                width 16px
                vertical-align middle
                font-size 12px
                border-1px(rgba(7, 17, 27, 0.1))
    .foods-wrapper
        flex 1
</style>
