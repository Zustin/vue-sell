<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li class="menu-item" v-for="item in goods">
          <span class="text">
            <span class="icon" :class="classMap[item.type]" v-show="item.type>0"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li class="foods-list" v-for="item in goods">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li class="food-item border-1px" v-for="food in item.foods">
              <div class="icon">
                <img width="57" height="57" :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">{{food.sellCount}}</span>
                  <span>{{food.rating}}</span>
                </div>
                <div class="price">{{food.price}}</div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  const ERR_OK = 0;

  export default {
    data() {
      return {
        goods: []
      };
    },
    mounted() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];

      this.$http.get('/api/goods').then((res) => {
        res = res.body;
        if (res.errno === ERR_OK) {
          this.goods = res.data;
        }
      });
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"

  .goods
    display flex
    position absolute
    top 174px
    bottom 46px
    width 100%
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
        z-index 10
        .text
          display table-cell
          width 56px
          vertical-align middle
          font-size 12px
          .icon
            display inline-block
            vertical-align top
            width 12px
            height 12px
            margin-right 2px
            background-size 12px 12px
            &.decrease
              bg-image('image/decrease_3')
            &.discount
              bg-image('image/discount_3')
            &.special
              bg-image('image/special_3')
            &.invoice
              bg-image('image/invoice_3')
            &.guarantee
              bg-image('image/guarantee_3')
    .foods-wrapper
      flex 1
</style>
