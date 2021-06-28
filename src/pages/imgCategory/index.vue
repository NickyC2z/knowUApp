<template>
  <view>
     <view class="category_tab">
       <view class="category_tab_title">
        <view class="title_inner">
          <uni-segmented-control
            :current="current"
            :values="items.map(v=>v.title)"
            @clickItem="onClickItem"
            style-type="text"
            active-color="#d4237a"
          ></uni-segmented-control>
        </view>
        <view class="iconfont icon-search"></view>
        </view>
        <view class="category_tab_content">
          <view class="cate_item"
          v-for="item in vertical"
          :key="item.id"
          >
            <image :src="item.thumb" mode="widthFix"></image>
          </view>
        </view>
       </view>
     </view>
</template>

<script>
import {uniSegmentedControl} from '@dcloudio/uni-ui';
export default {
  components:{
    uniSegmentedControl
  },
  data(){
    return{
      items:[
        {title:"最新",order:"new"},
        {title:"热门",order:"hot"}
      ],
      current: 0,
      params:{
        limit:30,
        skip:0,
        order:"new"
      },
      id:0,
      //页面显示数据的数组
      vertical:[]
    };
  },
  onLoad(options){
    this.id=options.id;
    this.getList();
  },
  methods:{
    onClickItem(e){
      /* 
      1.根据点击的标题切换标题
      2.切换order
      3.重新发送请求
      */
     this.params.order= this.items[e.currentIndex].order;
      if(this.current !== e.currentIndex){
          this.current = e.currentIndex; 
          this.getList()
      }
    },
    getList(){
      this.request({
        url:`http://service.picasso.adesk.com/v1/vertical/category/${this.id}/vertical`,
        data:this.params
      }).then(result=>{
        console.log(result)
        this.vertical=result.res.vertical
      })
    }
  }

}
</script>

<style lang="scss">
.category_tab{
  .category_tab_title{
    position: relative;
    .title_inner{
      width: 60%;
      margin: 0 auto;
    }
    .icon-search{
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      right: 5%;
    }
  }
  .category_tab_content{
    display: flex;
    flex-wrap: wrap;
    .cate_item{
      width:33.33%;
        border: 5rpx solid #fff;
      image{
        
      }
    }
  }
}

</style>