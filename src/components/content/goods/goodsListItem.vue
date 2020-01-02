<template>
  <div class="goods-list-item" @click="itemClick">
    <img :src="goodsListItem.show.img" alt @load="imageLoad"/>
    <div class="goods-title">{{goodsListItem.title}}</div>
    <div class="goods-num">
      <span class="goods-price">{{goodsListItem.orgPrice}}</span>

      <span class="goods-fav">{{goodsListItem.cfav}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    goodsListItem: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  methods:{
    imageLoad(){
      this.$bus.$emit("imageLoad")
    },
    itemClick(){
      this.$router.push('/detail/' + this.goodsListItem.iid);
      // this.$router.push({
      //   path:'/detail/',
      //   query:{
      //     iid: this.goodsListItem.iid
      //   }
      // })
    }
  }
};
</script>

<style scoped>
.goods-list-item {
  width: 48%;
  text-align: center;
  font-size: 12px;
  color: var(--color-text);
  overflow: hidden;
  margin-bottom:6px;
}
.goods-list-item img {
  width: 100%;
  margin-bottom: 3px;
}
.goods-title {
  overflow: hidden;
  padding: 5px 10px;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.goods-price {
  color: var(--color-high-text);
  margin-right:15px;
}
.goods-fav{
  position: relative;
  margin-left:15px;
}
.goods-fav::before {
  content: '';
  width: 14px;
  height: 14px;
  position: absolute;
  left:-15px;
  top:-1px;  
  background: url('~assets/img/goods/fav.svg') 0 0/14px 14px;
}
</style>