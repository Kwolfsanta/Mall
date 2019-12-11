<template>
<div id="main-swiper">
    <swiper>
    <swiper-item v-for="item in banners">
      <a :href="item.link">
        <img :src="item.image" alt="">
      </a>
    </swiper-item>
  </swiper>
</div>
</template>

<script>
import {swiper, swiperItem} from 'components/common/swiper'
export default {
  props:{
    banners:{
      type:Array,
    }
  },
components:{
  swiper,
  swiperItem
}
}
</script>

<style>

</style>