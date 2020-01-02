<template>
    <div class="tab-bar-item"  @click='itemClick'>
        <div v-if='!isActive'><slot name='item-icon'></slot></div>
        <div v-else><slot name='item-icon-active'></slot></div>
        <div :style='activeStyle'><slot name='item-text'></slot></div>
    </div>
</template>

<script>
export default {
name:'tabBarItem',
props:{
  path:String,
  activeColor:{
    type:String,
  default:'red'
  }
},
data(){
  return{
    // isActive: this.$route.path.indexOf(this.path) != -1
  }
},
computed:{
  isActive(){
    return this.$route.path.indexOf(this.path) != -1
  },
  activeStyle(){
    return this.isActive ? {color: this.activeColor} : {}
  }
},
methods:{
  itemClick(){
    if(this.path != this.$route.path)
    this.$router.replace(this.path);
  }
}
}
</script>

<style>
.tab-bar-item{
  flex:1;
  text-align: center;
  height: 49px;
  font-size: 12px;
}

.tab-bar-item img{
  width: 22px;
  height: 22px;
  margin-bottom:2px;
  margin-top:5px;
}

/* 一种方法 */
/* .text-active{
  color:rgba(226, 88, 88);
} */
</style>