<template>
  <swiper class="detail-swiper">
    <swiper-item v-for="link in topImages" >
      <img :src="link" alt="">
    </swiper-item>
  </swiper>
</template>

<script>
import {swiper, swiperItem} from "components/common/swiper";
export default {
  props:{
    topImages:{
      type:Array,
      default:null
    },
  },
components:{
  swiper,
  swiperItem
},

};
</script>

<style scoped>
.detail-swiper{
  height: 300px;
  overflow: hidden;
}
</style>

