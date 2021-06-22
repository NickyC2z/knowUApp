<template>
  <view>
    <!-- 用户信息开始 -->
    <view class="userinfo">
      <view class="user_icon">
        <image :src="imgDetail.user.avatar" mode="widthFix"></image>
      </view>
      <view class="user_desc">
        <view class="user_name">{{imgDetail.user.name}}</view>
        <view class="user_time">{{imgDetail.cnTime}}</view>
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
        <text class="iconfont icon-dianzan">{{imgDetail.rank}}</text>
      </view>
      <view class="user_collect">
        <text class="iconfont icon-shoucang">收藏</text>
      </view>
    </view>
    <!-- 点赞结束 -->
    <!-- 专辑开始 -->
    <view class="album_wrap">
      <view class="album_title">相关</view>
      <view class="album_list">
        <view class="album_item"
        v-for="item in album"
        :key="item.id"
        >
          <view class="album_cover">
            <image :src="item.cover" mode="widthFix"></image>
          </view>
          <!-- 右边 -->
          <view class="album_info">
            <view class="album_info_text">专辑</view>
            <view class="album_name">{{}}item.name</view>
          </view>
        </view>
      </view>
    </view>
    <!-- 专辑结束 -->
  </view>
</template>

<script>
import moment from "moment";
//设置moment 语言为中文
moment.locale("zh-cn")
export default {
data(){
  return{
    //图片信息对象 包含着用户头像
    imgDetail:{},
    //专辑数据
    album:[],
    //最热评论
    hot:[],
   //最新评论
   comment:[],
   //是否还有下一页
   hasMore:true,
  }
},
onLoad(){
  console.log(getApp().globalData);
  const {imgList,imgIndex} = getApp().globalData;
  this.imgDetail=imgList[imgIndex];
  this.imgDetail.newThumb=this.imgDetail.thumb+this.imgDetail.rule.replace('$<Height>',360)
  //xxx年前的数据
  this.imgDetail.cnTime=moment(this.imgDetail.atime*1000).fromNow();
  //获取图片详情的ID
  //this.imgDetail.id
  this.getComments(this.imgDetail.id);
},
methods:{
  getComments(id) {
      this.request({
        url: `http://157.122.54.189:9088/image/v2/wallpaper/wallpaper/"591ab1d8e7bce713483c6542"/comment`
      })
      .then(result=>{
        console.log(result);          
        this.album=result.res.album;
        this.hot=result.res.hot;
        this.comment=result.res.comment;

      })
  }
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
  display: flex;
  height:80rpx;
  border-bottom: 5rpx solid #eee;
  .rank {
    display: flex;
    justify-content: center;
    align-items: center;
    flex: 1;
    .iconfont {

    }
  }

  .user_collect {
    flex: 1;
        display: flex;
    justify-content: center;
    align-items: center;
    .iconfont {

    }
  }
}
</style>