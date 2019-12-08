<template>
  <div id='tabbar'>
    <slot></slot>
  </div>
</template>

<script>
import tabBarItem from './tabBarItem'
export default {
name:'tabBar',
components:{
  tabBarItem
}
}
</script>

<style>
#tabbar{
  display: flex;
  position:fixed;
  bottom:0;
  left:0;
  right:0;
  background: #f2f2f2;
  box-shadow: 0 -2px  rgba(0,0,0,.05);
  color:#333;
}

</style>