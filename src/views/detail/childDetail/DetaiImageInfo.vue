<template>
  <div class="detail-info" v-if="Object.keys(detailInfo).length !== 0">
   <div class="info-desc">
     <div class="start"></div>
     <div class="desc">
       {{detailInfo.desc}}
     </div>
     <div class="end"></div>
   </div>

    <div class="info-key"> {{detailInfo.detailImage[0].key}}</div>

    <div v-for="item in detailInfo.detailImage[0].list" class="image-info">
      <img :src="item" alt="" @load="imageLoad">
    </div>


  </div>

</template>

<script>
  export default {
    name: "DetailInfo",
    props:{
      detailInfo:{
        type:Object,
        default(){
          return {}
        }
      }
    },
    methods:{
      imageLoad(){
        this.$emit('detailImage')
      }
    }
  }
</script>

<style scoped>
  .detail-info {
    padding: 20px 0;
    border-bottom: 5px solid #f2f5f8;
  }
  .info-desc{
    padding: 0 15px;
  }
  .info-desc .start, .info-desc .end {
    width: 90px;
    height: 1px;
    background-color: #a3a3a5;
    position: relative;
  }

  .info-desc .start {
    float: left;
  }

  .info-desc .end {
    float: right;
  }

  .info-desc .start::before, .info-desc .end::after {
    content: '';
    position: absolute;
    width: 5px;
    height: 5px;
    background-color: #333;
    bottom: 0;
  }

  .info-desc .end::after {
    right: 0;
  }
  .info-desc .desc {
    padding: 15px 0;
    font-size: 14px;
  }
  .info-key {
    margin: 10px 0 10px 15px;
    color: #333;
    font-size: 15px;
  }
  .image-info img{
    width: 100%;

  }
</style>