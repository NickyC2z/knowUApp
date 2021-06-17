<template>
  <view>专辑</view>
</template>

<script>
export default {
  data(){
    return{
      params:{
        limit:30,
        order:"new",
        skip:0
      }
    }
  },
  mounted(){
    //修改页面的标题
    uni.setNavigationBarTitle({title:"专辑"})
    this.getList();
    },
  methods:{
    //获取接口的数据
    getList(){
      this.requset({
        url:"https://service.picasso.adesk.com/v1/wallpaper/album",
        data:this.parmas
      })
      .then(result=>{
        console.log(result);
      })
    }
  },
}
</script>

<style>

</style>