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
      default:0
    },
    click:{
      type:Boolean,
      default:true
    },
    pullUpLoad:{
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
    pullUpLoad:this.pullUpLoad
  })
  this.scroll.on('scroll', (position) => {
    // console.log(position);

    //这个用来做backTop也可以的哦
    this.$emit('scroll', position)
  })
  this.scroll.on('pullingUp', () => {
    this.$emit('pullingUp')
  })
},
methods:{
  scrollTo(x, y, time){
    this.scroll && this.scroll.scrollTo(x, y, time);
  },
  finishPullUp(){
    this.scroll && this.scroll.finishPullUp();
  },
  refresh() {
    // console.log(1);
    this.scroll && this.scroll.refresh();
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