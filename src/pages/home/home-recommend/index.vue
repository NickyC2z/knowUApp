<template>
  <view>
    <!-- 推荐开始 -->
    <view class="recommend_wrap">
      <view class="recommend_item"
      v-for="item in recommends"
      :key="item.id"
      >
      <image mode="widthFix" :src="item.thumb"></image>
      </view>
    </view>
    <!-- 推荐结束 -->
    <!-- 月份开始 -->
    <view class="moneths_wrap">
      <view class="moneths_title">
        <view class="moneths_title_info">
          <view class="moneths_info">
            <text>18/</text>
            01 月
          </view>
          <view class="moneths_text">你负责美丽就好</view>
        </view>
        <view class="moneths_title_more">更多></view>
      </view>
      <view class="moneths_content"></view>
    </view>
    <!-- 月份结束 -->
  </view>
</template>

<script>
export default {
  data(){
    return{
      //推荐列表
      recommends:[]
    }
  },
  mounted(){
    this.request({
      url:"http://service.picasso.adesk.com/v3/homepage/vertical",
      data:{
        //获取几条数据
        limit:30,
        //关键字
        order:"hot",
        //要调过几条
        skip:0
      }
    })
    .then(result=>{
      console.log(result);
      this.recommends=result.res.homepage[1].items;
    })
  }
}
</script>

<style lang="scss" scoped>
.recommend_wrap{
  //flex布局
  display: flex;
  flex-wrap: wrap;
  .recommend_item{
    width: 50%;
    border: 5rpx solid #fff;
  }
}
.moneths_wrap{
  .moneths_title{
    display: flex;
    padding: 20rpx;
    justify-content: space-between;
    .moneths_title_info{
      color: $color;
      font-size: 30rpx;
      font-weight: 600;
      display: flex;
      .moneths_info{
        text{
          font-size: 36rpx;
        }
      }
      .moneths_text{
        font-size: 34rpx;
        color:#666;
        margin-left: 30rpx;
      }
    }
    .moneths_title_more{
      font-size: 24rpx;
      color: $color;
    }
  }
  .moneths_content{

  }
}
</style>