<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <main-swiper :banners='banners'></main-swiper>
    <recommend-view :recommend = 'recommends'></recommend-view>
  </div>
</template>

<script>
import navBar from "components/common/navbar/navBar.vue";
import { getHomeMultidata } from "network/home.js";
import mainSwiper from "./childCpns/mainSwiper";
import recommendView from './childCpns/recommendView'

export default {
  data() {
    return {
      banners: [],
      recommends: []
    };
  },
  components: {
    navBar,
    mainSwiper,
    recommendView
  },
  created() {
    getHomeMultidata().then(res => {
      console.log(res);
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
  }
};
</script>
<style>
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
}
</style>