<template>
  <div id="app"
       class="clear-fix">
    <div class="sidebar">
      <left-nav></left-nav>
    </div>
    <div class="main">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import leftNav from '@/components/common/leftNav'
export default {
  name: 'App',
  components: {
    leftNav
  }
}
</script>

<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
ul {
  padding: 0;
  margin: 0;
}
.sidebar {
  float: left;
  width: 44px;
  height: 650px;
}
.main {
  overflow: hidden;
  height: 650px;
}
.clear-fix::after {
  display: block;
  content: '';
  height: 0;
  visibility: hidden;
  clear: both;
}
</style>
