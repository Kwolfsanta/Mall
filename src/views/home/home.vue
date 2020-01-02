<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <tab-control
      :titles="['流行', '新款', '精选']"
      @tabClick="tabClick"
      class="tab-control"
      ref="tabControl2"
      v-show="isTabShow"
    ></tab-control>
    <scroll
      class="scroll"
      ref="scroll"
      :probe-type="3"
      @scroll="scrollScroll"
      :pull-up-load="true"
      @pullingUp="loadMore"
    >
      <main-swiper :banners="banners" @imgLoad="imageLoad"></main-swiper>
      <recommend-view :recommend="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control :titles="['流行', '新款', '精选']" @tabClick="tabClick" ref="tabControl1"></tab-control>
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
      isShowBackTop: false,
      tabConTop: 0,
      isTabShow: false,
      saveY:0,
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
    },

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
    //老师解决scrollHeight载入bug方法
    // const refresh = this.debounce(this.$refs.scroll.refresh, 200);
    // this.$bus.$on('imageLoad', () => {
    //   refresh();
    // })
  },
  activated(){
    this.$refs.scroll.scrollTo(0, this.saveY, 0);
    this.$refs.scroll.refresh();
  },
  deactivated(){
    this.saveY = this.$refs.scroll.scroll.y;
  },
  methods: {
    /**
     * 弄下别的
     */
    //防抖
    debounce(func, delay) {
      let timer = null;
      return function(...args) {
        if (timer) clearTimeout(timer);
        timer = setTimeout(() => {
          func.apply(this, args);
        }, delay);
      };
    },

    //更改currentType
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
          this.$refs.tabControl2.currentIndex = index;
          this.$refs.tabControl1.currentIndex = index;
    },
    imageLoad(){
      this.tabConTop = this.$refs.tabControl1.$el.offsetTop;
      console.log(this.tabConTop);
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
      this.isTabShow = Math.abs(position.y) > this.tabConTop;
    },

    loadMore() {
      this.getHomeGoods(this.currentType);
      this.$refs.scroll.finishPullUp();
    },

    /**
     * 子组件发来的问候
     */
    imgLoad() {},

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

          //我自己的解决scrollHeight加载不正确的方法
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
  width: 100vw;
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
  position: relative;
  z-index: 9;
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