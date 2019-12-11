<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <scroll
      class="scroll"
      ref="scroll"
      :probe-type="3"
      @scroll="scrollScroll"
      :pull-up-load="true"
      @pullingUp="loadMore"
    >
      <main-swiper :banners="banners"></main-swiper>
      <recommend-view :recommend="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control :titles="['流行', '新款', '精选']" @tabClick="tabClick" class="tab-control"></tab-control>
      <goods-list :goods-list="showGoods"></goods-list>
    </scroll>
    <back-top class="back-top" @click.native="backTop" v-show="isShowBackTop"></back-top>
    <ul>
      <li v-for="item in this.banners">
        <a :href="item.link">
          <img :src="item.image" alt />
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
// components/common
import navBar from "components/common/navbar/navBar.vue";
import scroll from "components/common/scroll/bscroll.vue";

//components/content
import tabControl from "components/content/tabControl/tabControl.vue";
import goodsList from "components/content/goods/goodsList.vue";
import backTop from "components/content/backTop/backTop.vue";

// childCpns
import mainSwiper from "./childCpns/mainSwiper";
import recommendView from "./childCpns/recommendView";
import featureView from "./childCpns/featureView";

import { getHomeMultidata, getHomeGoods } from "network/home.js";

export default {
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      },
      currentType: "pop",
      isShowBackTop: false
    };
  },
  components: {
    navBar,
    scroll,
    tabControl,
    goodsList,
    backTop,
    mainSwiper,
    recommendView,
    featureView
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    }
  },
  created() {
    // 1.获取navbar信息啥的
    this.getHomeMultidata();
    // 2.获取列表展示信息
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  mounted() {
    //显示backTop，自己的方法
    // this.showBackTop();
  },
  methods: {
    /**
     * 弄下别的
     */
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
          break;
        case 2:
          this.currentType = "sell";
          break;
        default:
          break;
      }
    },
    //回到顶部
    backTop() {
      this.$refs.scroll.scrollTo(0, 0, 300);
      // this.backTop.style.display ="none"
    },

    // 显示backTop
    scrollScroll(position) {
      // console.log(position);
      this.isShowBackTop = Math.abs(position.y) > 700;
    },

    loadMore(){
      this.getHomeGoods(this.currentType);
      this.$refs.scroll.finishPullUp();
    },

    //显示backTop 自己的方法
    // showBackTop() {
    //   let backTop = document.querySelector('.back-top');
    //   this.$refs.scroll.scroll.on("scroll", position => {
    //     if (position.y < -552) {
    //       backTop.style.display = "block"
    //     }
    //     else{
    //       backTop.style.display = 'none'
    //     }
    //   });
    // },

    /**
     * 网络控制
     */
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page)
        .then(res => {
          this.goods[type].list.push(...res.data.list);
          this.$refs.scroll.refresh();
        })
        .catch(err => {
          console.log(err);
        });
      this.goods[type].page += 1;
    }
  }
};
</script>
<style scoped>
#home {
  padding-top: 44px;
  height: 100vh;
  /* width: 100vw; */
  position: relative;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 9;
}
.tab-control {
  position: sticky;
  top: 44px;
}
.scroll {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
  /* margin-top:44px; */
  /* height:calc(100% - 93px); */
}
ul {
  display: flex;
}
ul li {
  flex: 1;
}
ul li img {
  width: 100%;
}
.back-top {
  position: absolute;
  top: 480px;
  right: 5px;
}
</style>