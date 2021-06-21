<template>
  <scroll-view class="album_scroll_view" scroll-y @scrolltolower="handleToLower">
    <!-- swiper
          1.自动轮播 autoplay
          2.指示器  indicator-dots
          3.衔接轮播  circular
          4.swiper有一个默认的高度 150px
          5.image默认宽度为320（已在styles/base.wxss重置为100%)默认高度为240px
          6.计算图片宽高比利
          7.把图片的比例也写入swiper标签样式
          8.swiper-item 100%
    -->
    <!-- 轮播图开始 -->
    <view class="album_swiper">
      <swiper
       autoplay='true'
       indicator-dots='true'
       circular='true'
      >
        <swiper-item
        v-for="item in banner"
        :key="item.id"
        >
          <image :src="item.thumb"></image>
        </swiper-item>
      </swiper>
    </view>
    <!-- 轮播图结束 -->
    <!-- 列表开始 -->
    <view class="album_list">
      <navigator class="album_item"
      v-for="item in album"
      :key="item.id"
      :url="`/pages/album/index?id=${item.id}`"
      >
        <view class="album_image">
          <image mode="aspectFill" :src="item.cover" ></image>
        </view>
        <view class="album_info">
          <view class="album_name">{{item.name}}</view>
          <view class="album_desc">{{item.desc}}</view>
          <view class="album_btn">
            <view class="album_attention">关注</view>
          </view>
        </view>
      </navigator>
    </view>
    <!-- 列表结束 -->
  </scroll-view>
</template>

<script>
export default {
  data(){
    return{
      params:{
        limit:30,
        order:"new",
        skip:0,
        //当值为1时 返回值中有album对象 表示第一次请求数据
        //当值为0时 返回之中只有wallpaper数组 表示不是第一次请求数据
        first:1
      },
      //轮播图数字
      banner:[],
      //列表数组
      album:[],
      //是否还有分页数据
      hasMore:true
    }
  },
  mounted(){
    //修改页面的标题
    uni.setNavigationBarTitle({title:"专辑"}),
    this.getList();
    },
  methods:{
    //获取接口的数据
    getList(){
      this.request({

        url:"http://157.122.54.189:9088/image/v1/wallpaper/album",
        data:this.params
      })
      .then(result=>{
        console.log(result)
        if(this.banner.length===0){
          this.banner = result.res.banner;
        }
        if(result.res.album.length===0){
          this.hasMore=false;
          uni.showToast({
            title:"没有更多数据了",
            icon:"none"
          })
          return;
        }
        this.album=[...this.album,...result.res.album];
      })
    },
    //上拉加载 执行分页
    handleToLower(){
      if(this.hasMore){
        this.params.skip+=this.params.limit;
        this.getList();
      }else{
        unishowToast({
          title:"没有数据了",
          icon:"none"
        })
      }
    }
  },
}
</script>
<style lang="scss" scoped>
.album_scroll_view{
  height: calc(100vh - 36px);
}
.album_swiper{
  swiper{
    //height:calc(750rpx/2.3);
    height: 326.1rpx;
    image{
      height:100%;
    }
  }
}
.album_list{
  padding: 10rpx;
  .album_item{
    padding: 10rpx 0;
    display: flex;
    border-bottom: 1rpx solid #ccc;
      .album_image{
        flex: 1;
        padding: 10rpx;
        image{
          width: 200rpx;
          height: 200rpx;
        }
      }
    .album_info{
      padding: 0 10rpx;
      flex: 2;
      overflow: hidden;
      .album_name{
        font-size: 30rpx;
        color:#000;
        padding: 10rpx 0;
      }
      .album_desc{
        padding: 10rpx 0;
        font-size:24 rpx;
        text-overflow: ellipsis;
        overflow:hidden;
        white-space: nowrap;
      }
      .album_btn{
        padding: 10rpx;
        display: flex;
        justify-content: flex-end;
        .album_attention{
          color: $color;
          border: 1rpx solid $color;
          padding: 10rpx;

        }
      }
    }
  }
}
</style>