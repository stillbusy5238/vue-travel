<template lang="html">
  <div>
    <detail-banner :sightName="sightName" :bannerImg="bannerImg" :gallaryImgs="gallaryImgs"></detail-banner>
    <detail-header></detail-header>
    <div class="content">
      <detail-list :list="list"></detail-list>
    </div>

  </div>

</template>

<script>
import DetailBanner from './Banner'
import DetailHeader from './header'
import DetailList from './list'
import axios from 'axios'
export default {
  name:'Detail',
  components:{
    DetailBanner,
    DetailHeader,
    DetailList


  },
  data (){
    return {
      list:[],
      sightName:'',
      bannerImg:'',
      gallaryImgs:[]


    }
  },
  methods:{
    getDetailInfo(){
      axios.get('/api/detail.json?id=',{
        params :{
          id:this.$route.params.id
        }
      }).then(this.getDetailInfoSucc)
    },
    getDetailInfoSucc(res){
      res = res.data
      if(res.ret && res.data){
        const data = res.data
        this.list = data.categoryList
        this.sightName = data.sightName
        this.bannerImg = data.bannerImg
        this.gallaryImgs = data.gallaryImgs



      }
    }


  },
  mounted (){
    this.getDetailInfo()

  }
}
</script>

<style lang="stylus" scoped>
    .content
      height: 50rem
</style>
