<template>
<div id="main-swiper">
    <swiper>
    <swiper-item v-for="item in banners">
      <a :href="item.link">
        <img :src="item.image" alt="" @load="imgLoad">
      </a>
    </swiper-item>
  </swiper>
</div>
</template>

<script>
import {swiper, swiperItem} from 'components/common/swiper'
export default {
  data(){
    return {
    isLoad:false
    }
  },
  props:{
    banners:{
      type:Array,
    }
  },
components:{
  swiper,
  swiperItem
},
methods:{
  imgLoad(){
    if (!this.isLoad){
    this.$emit("imgLoad");
    this.isLoad = true;
    }
  }
}
}
</script>

<style>

</style>