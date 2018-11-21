<template>
   <div>
      <ul v-for="item in recommend" :key="item.id">
         <li>
            <img :src="item.picUrl" />
         </li>
      </ul>   
   </div>
</template>

<script>
import { getRecommend } from 'api/recommend'
import { ERR_OK } from 'api/config'

export default {
   data() {
      return {
         recommend:[]
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

</style>
