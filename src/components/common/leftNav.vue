<template>
  <ul class="nav">
    <li class="nav__cash">
      <i class="fa fa-cny fa-2x"></i>
      <p>收银</p>
    </li>
    <li class="nav__shop">
      <i class="fa fa-home fa-2x"></i>
      <p>店铺</p>
    </li>
    <li class="nav__goods">
      <i class="fa fa-shopping-basket fa-2x"></i>
      <p>商品</p>
    </li>
    <li class="nav__member">
      <i class="fa fa-user-circle-o fa-2x"></i>
      <p>会员</p>
    </li>
    <li class="nav__count">
      <i class="fa fa-bar-chart fa-2x"></i>
      <p>统计</p>
    </li>
  </ul>
</template>
<style lang="less" scoped>
ul,
p {
  padding: 0;
  margin: 0;
}
.nav {
  height: 100%;
  background-color: #1d8ce0;
  font-family: 'Microsoft YaHei' sans-serif;
  font-size: 12px;
  color: #fff;
  .fa {
    color: #fff;
  }
  li {
    padding: 30px 10px;
    list-style: none;
    text-align: center;
    border-bottom: 1px solid #20a0ff;
  }
}
</style>
