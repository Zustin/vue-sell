<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img height="64" width="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">{{seller.description}} / {{seller.deliveryTime}}分钟送达</div>
        <div class="support" v-if="seller.supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="support-count" v-if="seller.supports" @click="detailShow=!detailShow">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="detailShow=!detailShow">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img width="100%" height="100%" :src="seller.avatar" alt="">
    </div>
    <transition name="fade">
      <div class="detail" v-show="detailShow">
        <div class="detail-wrapper">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <star :score="seller.score" :size="48"></star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul class="supports" v-if="seller.supports">
              <li class="supports-item" v-for="(item, index) in seller.supports">
                <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                <span class="text">{{seller.supports[index].description}}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close"  @click="detailShow=!detailShow">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
  import Star from '../star/star';

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false
      };
    },
    mounted() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components: {
      Star
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin";

  .header
    position relative
    overflow hidden
    color #fff
    background rgba(7,17,27,0.5)
    .content-wrapper
      position relative
      padding 24px 12px 18px 24px
      font-size 0
      .avatar
        display inline-block
        vertical-align top
      .content
        display inline-block
        margin-left 16px
        .title
          margin 2px 0 8px 0
          .brand
            display inline-block
            vertical-align top
            width 30px
            height 18px
            bg-image('image/brand')
            background-size 30px 18px
          .name
            margin-left 6px
            font-size 16px
            line-height 18px
            font-weight bold
        .description
          font-size 12px
          line-height 1
          margin-bottom 10px
        .support
          .icon
            display inline-block
            vertical-align top
            width 12px
            height 12px
            margin-right 4px
            background-size 12px 12px
            &.decrease
              bg-image('image/decrease_1')
            &.discount
              bg-image('image/discount_1')
            &.special
              bg-image('image/special_1')
            &.invoice
              bg-image('image/invoice_1')
            &.guarantee
              bg-image('image/guarantee_1')
          .text
            line-height 12px
            font-size 10px
      .support-count
        position absolute
        right 12px
        bottom 14px
        padding 0 8px
        height 24px
        line-height 24px
        border-radius 14px
        background rgba(0,0,0,0.2)
        text-align center
        .count
          font-size 10px
          vertical-align top
        .icon-keyboard_arrow_right
          font-size 10px
          margin-left 2px
          line-height 24px
    .bulletin-wrapper
      position relative
      height 28px
      line-height 28px
      padding 0 22px 0 12px
      white-space nowrap
      overflow hidden
      text-overflow ellipsis
      background rgba(7,17,27,0.2)
      .bulletin-title
        margin-top 8px
        display inline-block
        vertical-align top
        width 22px
        height 12px
        bg-image('image/bulletin')
        background-size 22px 12px
      .bulletin-text
        vertical-align top
        margin 0 4px
        font-size 10px
      .icon-keyboard_arrow_right
        position absolute
        right 12px
        top 8px
        font-size 10px
    .background
      position absolute
      top 0
      left 0
      width 100%
      height 100%
      z-index -1
      filter blur(10px)
    .detail
      position fixed
      top 0
      left 0
      width 100%
      height 100%
      overflow auto
      background rgba(0,0,0,.5)
      opacity 1
      &.fade-enter-active, &.fade-leave-active
        transition: all 0.5s
      &.fade-enter, &.fade-leave-active
        opacity: 0
        background: rgba(7, 17, 27, 0)
      .detail-wrapper
        width 100%
        min-height 100%
        .detail-main
          padding-bottom 64px
          margin-top 64px
          .name
            font-size 16px
            line-height 1
            text-align center
            font-weight 700
          .star-wrapper
            margin-top 18px
            padding 2px 0
            text-align center
          .title
            display flex
            width 80%
            margin 28px auto 24px
            .line
              position relative
              top -6px
              flex 1
              border-bottom 1px solid rgba(255,255,255,0.2)
            .text
              padding 0 12px
              font-weight 700
              font-size 14px
          .supports
            width 80%
            margin 0 auto
            .supports-item
              padding 0 12px
              margin-bottom 12px
              font-size 0
              .icon
                display inline-block
                vertical-align top
                width 12px
                height 12px
                margin-right 4px
                background-size 12px 12px
                &.decrease
                  bg-image('image/decrease_1')
                &.discount
                  bg-image('image/discount_1')
                &.special
                  bg-image('image/special_1')
                &.invoice
                  bg-image('image/invoice_1')
                &.guarantee
                  bg-image('image/guarantee_1')
              .text
                line-height 16px
                font-size 12px
          .bulletin
            width 80%
            margin 0 auto
            .content
              padding 0 12px
              line-height 24px
              font-size 12px
              text-align justify
      .detail-close
        position relative
        width 32px
        height 32px
        margin -64px auto 0
        clear both
        font-size 32px
</style>
