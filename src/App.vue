<template>
  <div id="app">
    <m-header :seller="seller"></m-header>
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

<style>
</style>
