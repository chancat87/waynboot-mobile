<template>
  <div class="tab-bar">
    <van-goods-action>
      <van-goods-action-icon icon="home-o" text="首页" @click="goHome" />
      <van-goods-action-icon icon="cart-o" text="购物车" :badge="count" @click="cartClick" />
      <van-goods-action-button type="warning" text="加入购物车" @click="handleClick" />
      <van-goods-action-button :color="variables.red" text="立即购买" @click="handleClick" />
    </van-goods-action>
    <div class="tabbar--placeholder" style="width:100%;height:50px" />
  </div>
</template>

<script>
import { getCartGoodsCount } from '@/api/cart'
import variables from '@/styles/variables.scss'

export default {
  data() {
    return {
      count: 0
    }
  },
  computed: {
    variables() {
      return variables
    }
  },
  mounted() {
    this.getCartGoodsCount()
  },
  methods: {
    getCartGoodsCount() {
      getCartGoodsCount().then(res => {
        const { data } = res
        this.count = data
      }).catch(e => {})
    },
    handleClick() {
      this.$emit('input', true)
    },
    cartClick() {
      this.$router.push({ name: 'Cart' })
    },
    goHome() {
      this.$router.push({ name: 'Home' })
    }
  }
}
</script>

<style>
</style>
