<template>
  <div class="tab-control">
    <div class="tab-control-item" v-for="(item, index) in titles" @click="tabConClick(index)" :class="{active: index === currentIndex}">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    titles: {
      type: Array
    }
  },
  data() {
    return {
      currentIndex: 0
    };
  },
  methods: {
    tabConClick(index) {
      this.currentIndex = index;
      this.$emit('tabClick', index);
    }
  }
};
</script>

<style scoped>
.tab-control{
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
  text-align: center;
  background-color: #fff;
  box-shadow: 0 1px 3px rgba(0, 0, 0, .2)
}
.tab-control-item{
  flex:1

}
.active span{
  border-bottom:3px solid var(--color-tint);
  color:var(--color-high-text);
  padding:5px;
}
</style>