<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav"></detail-nav-bar>
    <scroll class="wrapper" ref="scroll">
      <detail-swiper :top-images="topImages"></detail-swiper>
      <detail-base-info :goods="goods" />
      <detail-shop-info :shop="shop"></detail-shop-info>
      <detail-goods-info :detail-info="detailInfo"></detail-goods-info @imgLoad="imageLoad">
      <detail-param-info :param-info="paramInfo"></detail-param-info>
      {{iid}}
    </scroll>
  </div>
</template>

<script>
import { getGoodsDetail, Goods, Shop, GoodsParam } from "network/detail.js";
import detailNavBar from "./childCpns/detailNavBar.vue";
import detailSwiper from "./childCpns/detailSwiper.vue";
import detailBaseInfo from "./childCpns/detailBaseInfo";
import detailShopInfo from "./childCpns/detailShopInfo";
import detailGoodsInfo from "./childCpns/detailGoodsInfo";
import detailParamInfo from "./childCpns/detailParamInfo";

import scroll from "components/common/scroll/bscroll.vue";
export default {
  name: "detail",
  data() {
    return {
      iid: null,
      topImages: null,
      goods: {},
      shop: {},
      detailInfo:{},
      paramInfo:{},
    };
  },
  components: {
    detailNavBar,
    detailSwiper,
    detailBaseInfo,
    detailShopInfo,
    detailGoodsInfo,
    detailParamInfo,
    scroll
  },
  created() {
    this.iid = this.$route.params.iid;
    getGoodsDetail(this.iid).then(res => {
      console.log(res);
      const data = res.result;
      // 1.获取顶部的轮播图数据
      this.topImages = data.itemInfo.topImages;

      // 2.获取商品信息
      this.goods = new Goods(
        data.itemInfo,
        data.columns,
        data.shopInfo.services
      );
      
      // 3.获取店铺信息
      this.shop = new Shop(data.shopInfo);
      console.log(this.shop);
      
      // 4.保存商品详情数据
      this.detailInfo = data.detailInfo;

      // 5.获取参数的信息
      this.paramInfo = new GoodsParam(data.itemParams.info, data.itemParams.rule);
      console.log(this.paramInfo);
    });
  },
  methods:{
    imageLoad(){
      this.$refs.scroll.refresh();
    }
  }
};
</script>

<style scoped>
#detail {
  position: relative;
  z-index: 9;
  background-color: #fff;
  height:100vh;
}

.detail-nav{
  position: relative;
  z-index:9;
  background-color: #fff;
}

.wrapper{
  height:calc(100% - 44px);
}
</style>
