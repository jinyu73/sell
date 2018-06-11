<template>
    <div class="cartcontrol">
      <transition-group leave-active-class="fadeOutRight" enter-active-class="fadeInRight">
        <div class="cart-decrease icon-remove_circle_outline animated" v-show="food.count > 0"
            @click="decreaseCart" :key="1"></div>
        <div class="cart-count animated" v-show="food.count>0" :key="2">{{food.count}}</div>
      </transition-group>
        <div class="cart-add icon-add_circle" @click="addCart"></div>
    </div>
</template>

<script>
import Vue from 'vue'
import Hub from '@/Hub.js'
export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart () {
      console.log(this.food)
      if (!this.food.count) {
        console.log(1)
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
      // 体验优化，异步执行下落代码
      this.$nextTick(() => {
        Hub.$emit('cartAdd', event.target)
      })
    },
    decreaseCart () {
      if (this.food.count === 0) {
        return
      }
      this.food.count--
    }
  }
}
</script>

<style lang="stylus">
.cartcontrol
    font-size 0
    position relative
    z-index 5
    .cart-decrease, .cart-add
        display inline-block
        padding 6px
        line-height 24px
        font-size 24px
        color rgb(0, 160, 220)
    .cart-count
        display inline-block
        vertical-align top
        width 12px
        padding-top 6px
        line-height 24px
        text-align center
        font-size 10px
        color rgb(147, 153, 159)
</style>
