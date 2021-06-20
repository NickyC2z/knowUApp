<template>
  <view>
    <!-- 专辑背景开始 -->
    <view class="album_bg">
      <image mode="widthFix" :src="album.cover"></image>
      <view class="album_info">
        <view class="album_name">{{album.name}}</view>
        <view class="album_btn">关注专辑</view>
      </view>
    </view>
    <!-- 专辑背景结束 -->
  </view>
</template>

<script>
export default {
  data(){
    return{
      params:{
        limit:30,
        order:"new",
        skip:0,
        first:1
      },
      id:-1,
      album:{},
      wallpaper:[]
    }
  },
  onLoad(options){
    console.log(options);
    //this.id=options.id;
    this.id="60c84c0ae7bce753543a6a4e",
    this.getList();
  },
  methods:{
    getList(){
      this.request({
        url:`http://service.picasso.adesk.com/v1/wallpaper/album/${this.id}/wallpaper`,
        data:this.params
      })
      .then(result=>{
        console.log(result);
        this.album=result.res.album
        this.wallpaper=result.res.wallpaper
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.album_bg {
  position: relative;
  image {

  }

  .album_info {
    position: absolute;
    width: 1010%;
    left: 0;
    bottom:0;
    display: flex;
    justify-content: space-between;
    height:80rpx;
    align-items: center;
    color:#fff;
    padding:0 15rpx;
    .album_name {
      font-size: 40rpx;

    }

    .album_btn {
      background-color: $color;
      width: 152rpx;
      height: 50rpx;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 10rpx;
    }
  }
}
</style>