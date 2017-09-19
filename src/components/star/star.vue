<template>
  <div class="star" :class="starType">
    <span v-for="item in scoreBox" class="star-item" :class="item"></span>
  </div>
</template>

<script type="text/ecmascript-6">
  const _length = 5;
  const _on = 'on';
  const _half = 'half';
  const _off = 'off';

  export default {
    props: {
      score: {
        type: Number
      },
      size: {
        type: Number
      }
    },
    computed: {
      starType() {
        return 'star-' + this.size;
      },
      scoreBox() {
        let result = [];
        let score = Math.floor(this.score * 2) / 2;
        let hasDecimal = score % 1 !== 0;
        let integer = Math.floor(score);
        for (let i = 0; i < integer; i++) {
          result.push(_on);
        }
        if (hasDecimal) {
          result.push(_half);
        }
        while (result.length < _length) {
          result.push(_off);
        }
        return result;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl";

  .star
    font-size 0
    .star-item
      display inline-block
    &.star-48
      .star-item
        width 20px
        height 20px
        margin-right 22px
        background-size 20px 20px
        &:last-child
          margin-right 0
        &.on
          bg-image('image/star48_on')
        &.off
          bg-image('image/star48_off')
        &.half
          bg-image('image/star48_half')
    &.star-36
      .star-item
        width: 15px
        height: 15px
        margin-right: 6px
        background-size: 15px 15px
        &:last-child
          margin-right: 0
        &.on
          bg-image('image/star36_on')
        &.half
          bg-image('image/star36_half')
        &.off
          bg-image('image/star36_off')
    &.star-24
      .star-item
        width: 10px
        height: 10px
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0
        &.on
          bg-image('image/star24_on')
        &.half
          bg-image('image/star24_half')
        &.off
          bg-image('image/star24_off')
</style>
