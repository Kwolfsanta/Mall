<template>
  <div id="recommend">
    <div class="recommend-item" v-for="item in recommend">
      <a :href="item.link">
        <img :src="item.image" alt="">
      </a>
      <div>{{item.title}}</div>
    </div>
  </div>
</template>

<script>
export default {
props:{
  recommend:{
    type:Array,
    default(){
      return []
    }
  }
}
}
</script>

<style scoped>
  #recommend{
    display: flex;
    text-align: center;
    padding:15px 0 30px;
    border-bottom:10px solid #eee;
  }
  .recommend-item{
    flex:1;
    font-size: 12px;
  }
  .recommend-item img{
    width: 65px;
    height: 65px;
    margin-bottom:8px;
  }
</style>