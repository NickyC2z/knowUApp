<template>
  <view>
    <!-- 用户信息开始 -->
    <view class="userinfo">
      <view class="user_icon">
        <image :src="imgDetail.user.avatar" mode="widthFix"></image>
      </view>
      <view class="user_desc">
        <view class="user_name">{{imgDetail.user.name}}</view>
        <view class="user_time">{{imgDetail.atime}}</view>
      </view>
    </view>
    <!-- 用户信息结束 -->
    <!-- 高清大图 开始 -->
    <view class="high_img">
      <image mode="widthFix" :src="imgDetail.newThumb"></image>
    </view>
    <!-- 高清大图结束 -->
    <!-- 点赞开始 -->
    <view class="user_rank">
      <view class="rank">
        <text class="iconfont icondianzan">{{imgDetail.rank}}</text>
      </view>
      <view class="user_collect">
        <text class="iconfont iconshoucang">收藏</text>
      </view>
    </view>
    <!-- 点赞结束 -->
  </view>
</template>

<script>

export default {
data(){
  return{
    //图片信息对象 包含着用户头像
    imgDetail:{}
  }
},
onLoad(){
  //console.log(getApp().globalData);
  const {imgList,imgIndex} = getApp().globalData;
  this.imgDetail=imgList[imgIndex];
  this.imgDetail.newThumb=this.imgDetail.thumb+this.imgDetail.rule.replace('$<Height>',360)
}
}
</script>

<style lang="scss" scoped>
.userinfo {
  display: flex;
  padding: 20rpx;
  .user_icon {
    padding: 0 20rpx;
    image {
      width:90rpx;
      border-radius: 50%;

    }
  }

  .user_desc {
    .user_name {
      color:#000;
      font-weight: 600;
    }

    .user_time {
      color:#ccc;
      font-size: 24rpx;
      padding:10rpx 0;
    }
  }
}
.user_rank {
  .rank {
    .iconfont {

    }
  }

  .user_collect {
    .iconfont {

    }
  }
}
</style>