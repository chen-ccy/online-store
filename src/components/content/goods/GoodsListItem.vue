<template>
  <div class="goods-list-item" @click="goodItemClick" v-if="true">
    <img :src="goodsItemImage" alt="" @load="imageLoad">
    <div class="goods-info">
    <p>{{goodsItem.title}}</p>
    <span class="price">{{goodsItem.price}}</span>
    <span class="collect">{{goodsItem.cfav}}</span></div>

  </div>
</template>

<script>
  export default {
    name: "GoodsListItem",
    props:{
      goodsItem:{
        type:Object,
        default(){
          return {}
        }
      }
    },
    computed:{
      goodsItemImage(){
        return this.goodsItem.img || this.goodsItem.image || this.goodsItem.show.img
      }
    },
    mounted(){
    },
    methods:{
      imageLoad(){
        this.$bus.$emit("itemImageLoad")
      },
      goodItemClick(){
        this.$router.push('/detail/'+this.goodsItem.iid)
      }
    }
  }
</script>

<style scoped>
  .goods-list-item{
    padding-bottom: 40px;
    width: 46%;
    position: relative;
    cursor: pointer;
  }
  .goods-list-item img{
    width: 100%;
    border-radius: 5px;
  }
  .goods-info {
    font-size: 12px;
    position: absolute;
    bottom: 5px;
    left: 0;
    right: 0;
    overflow: hidden;
    text-align: center;
  }
  .goods-info .price{
    color: var(--color-high-text);
    margin-right: 35px;
  }
  .goods-info .collect{
    position: relative;
  }
  .goods-info .collect::before {
    content: '';
    position: absolute;
    left: -15px;
    top: -1px;
    width: 14px;
    height: 14px;
    background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
  }
  .goods-info p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    margin-bottom: 3px;
  }
</style>