<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-bottom">
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
import Header from 'components/header/Header'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    'v-header': Header
  },
  data () {
    return {
      seller: {}
    }
  },
  methods: {
    getSellerInfo () {
      axios.get('/api/seller.json').then(this.getSellerInfoSucc)
    },
    getSellerInfoSucc (res) {
      this.seller = res.data.seller
    }
  },
  created () {
    this.getSellerInfo()
  }
}
</script>

<style lang="stylus" scoped>
.tab
  display: flex
  width: 100%
  height: 40px
  line-height: 40px

  .tab-item
    flex: 1
    text-align: center

    & > a
      display: block
      font-size: 14px
      color: rgb(77, 85, 93)

      &.active
        color: rgb(240, 20, 20)
</style>
