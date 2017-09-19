<template>
  <div id="app">
    <m-header :seller="seller"></m-header>
    <div class="tab border-1px">
      <span class="tab-item">
        <router-link to="/goods">商品</router-link>
      </span>
      <span class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </span>
      <span class="tab-item">
        <router-link to="/seller">商家</router-link>
      </span>
    </div>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script type="text/ecmascript-6">
  import MHeader from './components/header/header';

  const ERR_OK = 0;

  export default {
    data() {
      return {
        seller: {}
      };
    },
    mounted() {
      this.$http.get('/api/seller').then((res) => {
        res = res.body;
        if (res.errno === ERR_OK) {
          this.seller = res.data;
        }
      });
    },
    // name: 'app',
    components: {
      MHeader
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"

  .tab
    display flex
    width 100%
    height 40px
    line-height 40px
    border-1px(rgba(7, 17, 27, 0.1))
    .tab-item
      flex 1
      text-align center
      font-size 14px
      .router-link-active
        color rgb(240, 20, 20)
</style>
