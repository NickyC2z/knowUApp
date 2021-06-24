<template>
  <view class="home_category">
    <view class="cate_item"
    v-for="item in category"
    :key="item.id"
    >
      <image mode="widthFix" :src="item.cover"></image>
      <view class="cate_name">{{item.name}}</view>
    </view>
  </view>
</template>

<script>
export default {
  data(){
    return{
      category:[]
    }
  },
  mounted(){
    //修改页面的标题
    uni.setNavigationBarTitle({title:"分类"})
    this.getList()
  },
  methods:{
    getList(){
      this.request({
        url:"http://157.122.54.189:9088/image/v1/vertical/category"
      })
      .then(result=>{
        console.log(result)
        this.category=result.res.category;
      })
    }
  }
}
</script>

<style>

</style>