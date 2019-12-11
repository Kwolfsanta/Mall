<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll';
export default {
  props:{
    probeType:{
      type:Number,
      default:3
    },
    click:{
      type:Boolean,
      default:true
    },
    pullingUp:{
      type:Boolean,
      default:true
    }
  },
  data(){
    return {
      scroll:null
    }
  },
mounted(){
  this.scroll = new BScroll(this.$refs.wrapper, {
    probeType:this.probeType,
    click:this.click,
    pullingUp:this.pullingUp
  })
  this.scroll.on('scroll', (position) => {
    // console.log(position);
  })
},
methods:{
  scrollTo(x, y, time){
    this.scroll.scrollTo(x, y, time);
  }
}
}
</script>

<style scoped>
.wrapper {
  /* height:400px; */
  /* background-color: yellow; */
  /* overflow: hidden; */
}
</style>