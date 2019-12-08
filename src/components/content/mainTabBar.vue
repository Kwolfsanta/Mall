<template>
  <div id="main-tabbar">
    <tab-bar>
          <tab-bar-item path='/home' activeColor='blue'>
            <img slot='item-icon' src="~assets/img/tabbar/home.png" alt="">
            <img slot='item-icon-active' src="~assets/img/tabbar/home (1).png" alt="">
            <div slot='item-text'>首页</div> 
          </tab-bar-item>
    <tab-bar-item path='/category' activeColor='pink'>
      <img slot='item-icon' src="~assets/img/tabbar/category.png" alt="">
      <img slot='item-icon-active' src="~assets/img/tabbar/category (1).png" alt="">
      <div slot='item-text'>目录</div> 
    </tab-bar-item>
    <tab-bar-item path='/cart' activeColor='teal'>
      <img slot='item-icon' src="~assets/img/tabbar/cart.png" alt="">
      <img slot='item-icon-active' src="~assets/img/tabbar/cart (1).png" alt="">
      <div slot='item-text'>购物车</div> 
    </tab-bar-item>
    <tab-bar-item path='/profile' activeColor='deeppink'>
      <img slot='item-icon' src="~assets/img/tabbar/profile.png" alt="">
      <img slot='item-icon-active' src="~assets/img/tabbar/profile (1).png" alt="">
      <div slot='item-text'>我的</div> 
    </tab-bar-item>
    </tab-bar>
  </div>
</template>

<script>
import tabBar from 'components/common/tabbar/tabBar.vue';
import tabBarItem from 'components/common/tabbar/tabBarItem.vue'
export default {
components:{
  tabBar,
  tabBarItem
}
}
</script>

<style>

