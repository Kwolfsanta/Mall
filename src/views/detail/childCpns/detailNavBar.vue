<template>
<div class="detail-nav-bar">
  <nav-bar>
    <div class="back" slot="left" @click="backClick">
      <img src="~assets/img/home/back.png" alt="">
    </div>
    <div slot="center" class="title">
      <div class="title-item" v-for="(item, index) in titles" :class="{active: index === currentIndex}"
      @click="titleClick(index)">
        {{item}}
      </div>
    </div>
  </nav-bar>
</div>
</template>

<script>
import navBar from "components/common/navbar/navBar.vue";
export default {
  data(){
    return{
      titles:['商品', "参数","评论", "推荐"],
      currentIndex:0
    }
  },
  components:{
    navBar
  },
  methods:{
    titleClick(index){
      this.currentIndex = index;
    },
    backClick(){
      this.$router.back();
    }
  }
};
</script>

<style scoped>
.title{
  display: flex;
  text-align: center;
  font-size: 13px;
}
.title-item{
  flex:1;
}
.back{
  display: flex;
}
.back img{
  width: 70%;
  margin:0 auto
}
.active{
  color:var(--color-high-text);
}
</style>
