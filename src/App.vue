<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style lang="less">
@import '~vux/src/styles/reset.less';

body {
  background-color: #fbf9fe;
}
html,
body,
#app {
  width: 100%;
  height: 97%;
  margin: 0;
}
.weui-cells__title {
  background-color: #324057;
  margin: 0 !important;
  padding: 10px;
  height: 33px;
  line-height: 33px;
}
  .headerStyle {
    width: 100%;
    position: absolute;
    left: 0;
    top: 0;
    z-index: 100;
  }
</style>
