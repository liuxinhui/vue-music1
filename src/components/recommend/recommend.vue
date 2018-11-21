<template>
   <div>
      <div class="wrapper">
         <!-- v-if="recommend.length>1" 就可以循环播放了 -->
         <swiper v-if="recommend.length>1" :options="swiperOption" ref="mySwiper">
            <!-- slides -->
            <swiper-slide v-for="item of recommend" :key="item.id">
               <img class="swiper-img" :src="item.picUrl" /> 
            </swiper-slide>
            <!-- Optional controls -->
            <div class="swiper-pagination"  slot="pagination"></div>
         </swiper>  
      </div>
   </div>
</template>

<script>
import { getRecommend } from 'api/recommend'
import { ERR_OK } from 'api/config'

export default {
   data() {
      return {
         recommend:[],
         swiperOption: {
            pagination: {
               el: '.swiper-pagination',
               type: 'bullets'
            },
            autoplay: true,
            speed: 400,
            loop:true,
         },
         swiperSlides: [1, 2, 3, 4, 5]
      }
   },
   created() {
      this._getRecommend()
   },
   methods: {
      _getRecommend() {
         getRecommend().then((res) =>{
            if (res.code === ERR_OK) {
               this.recommend = res.data.slider
               console.log(this.recommend)
            }
         })
      }
   }
}
</script>

<style lang="stylus" scoped>
   .wrapper >>> .swiper-pagination-bullet-active
    background: #fff
  .wrapper
    overflow: hidden
    width: 100%
    height: 0
    padding-bottom: 40%
    background: #eee
    .swiper-img
      width: 100%
</style>
