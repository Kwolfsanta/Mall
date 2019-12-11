<template>
  <div class="goods">
    <goods-list-item v-for="item in goodsList" :goods-list-item="item"></goods-list-item>
  </div>
</template>

<script>
import goodsListItem from "./goodsListItem";
export default {
  components: {
    goodsListItem
  },

  props: {
    goodsList: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>

<style>
.goods{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
</style>