<template>
  <div ref="wrapper" class="city-list wrapper">
    <ul>
      <div v-for="(item,key) in cityList" :key="key">
        <div :ref="key" class="letter">{{key}}</div>
        <div @click="handleChangeCity(city.name)" v-for="city in item" :key="city.id" class="city b-1px-b">{{city.name}}</div>
      </div>
    </ul>
  </div>
</template>
<script>
import BScroll from "better-scroll";
import { mapMutations, mapActions } from "vuex";
export default {
  props: {
    cityList: [Object, Array],
    letter:[String]
  },
  data() {
    return {};
  },
  mounted() {
    this.$nextTick(() => {
      this.scroll = new BScroll(this.$refs.wrapper);
      // console.log(this.scroll);
    });
  },
  methods:{
    ...mapMutations(['changeCity']),
    // ...mapActions(['changeCity']),
    handleChangeCity(cityName){
      
      this.changeCity(cityName);
      this.$router.push('/');
    }
  },
  watch:{
    letter(newLetter, oldLetter){
      if (newLetter !== oldLetter) {
        // console.log(this.$refs[newLetter][0])
        this.scroll.scrollToElement(this.$refs[newLetter][0]);
      } 
    }
  }
  
};
</script>
<style lang="stylus" scoped>
.city-list
  position absolute
  top 44px
  left 0
  bottom 0
  right 0
  overflow hidden
  background-color #f5f5f5
  font-size 12px
  color #212121
  .letter
    padding 12px 15px
  .city
    font-size 14px
    height 44px
    padding-left 15px
    background-color white
    line-height 44px
    padding-right 20px
</style>
