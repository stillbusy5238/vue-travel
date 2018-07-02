<template lang="html">
  <div class="">
    <home-header></home-header>
    <home-swiper :list="swiperList"></home-swiper>
    <home-icons  :list="iconList"></home-icons>
    <home-recommend :list="recommendList"></home-recommend>
    <home-weekend :list="weekendList"></home-weekend>


  </div>

</template>

<script>
import HomeHeader from './header'
import HomeSwiper from './swiper'
import HomeIcons from './icon'
import HomeRecommend from './recommend'
import HomeWeekend from './weekend'
import {mapState} from 'vuex'
import axios from 'axios'
export default {
  name:'Home',
  components:{
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend


  },
  data (){
    return {
      lastCity:'',
      swiperList: [],
      iconList: [],
      recommendList: [],
      weekendList: []
    }
  },
  mounted (){
    this.lastCity = this.city
    this.getHomeInfo()

  },
  computed:{
    ...mapState(['city'])

  },
  // 加入keepalive之后
  activated(){
    if(this.lastCity !== this.city){
      this.lastCity = this.city
      this.getHomeInfo()

    }

  },
  methods:{
    getHomeInfo(){
      axios.get('/api/index.json?city=' + this.city)
           .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc(res){
      res = res.data
      if(res.ret && res.data){
        const data = res.data

        this.swiperList = data.swiperList
        this.iconList = data.iconList
        this.recommendList = data.recommendList
        this.weekendList = data.weekendList

      }
      console.log(res);

    }
  }
}
</script>

<style >
</style>
