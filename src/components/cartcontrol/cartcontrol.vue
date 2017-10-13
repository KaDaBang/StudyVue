<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart">
          <i class="inner icon-remove_circle_outline"></i>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add" @click="addCart">
      <i class="icon-add_circle"></i>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue'
  export default {
    props: {
      food: {
        type: Object
      }
    },
    created () {
    },
    methods: {
      addCart () {
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1)
        } else {
          this.food.count++
        }
        this.$emit('add', event.target)
      },
      decreaseCart () {
        if (this.food.count) {
          this.food.count--
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease, .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 18px
      color: rgb(0, 160, 220)
    .cart-count
      display: inline-block
      vertical-align : top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(157, 153, 159)
    .cart-decrease
      transform: translate3D(0, 0, 0)
      .inner
        transition: all .4s linear
        transform: rotate(0)
      &.move-enter-active, &.move-leave-active
        transition: all .4s linear
      &.move-enter, &.move-leave-to
        transform: translate3D(24px, 0, 0)
        opacity: 0
        .inner
          transform: rotate(180deg)
</style>
