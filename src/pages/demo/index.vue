<template>
  <view
  @touchstart="handleTouchStart"
  @touchend="handleTouchEnd"
  >学习触屏事件</view>
</template>

<script>
export default {
  /* 
  1.为容器绑定两个触屏事件 touchstart 和 touchend
  2.用户按下屏幕事件
    1.记录按下屏幕的时间 date.now()时间戳 返回 1970-1-1到现在的毫秒时间
    2.记录用户按下屏幕的坐标X和Y
  3.用户离开屏幕事件
    1.记录用户离开屏幕的时间 Date.now()
    2.记录用户离开屏幕的坐标X和Y
    3.根据两个时间判断用户按下屏幕的时长是否合法
    4.根据两队坐标判断距离是否合法并判断滑动方向

  */
methods:{
  handleTouchStart(e){
    console.log("手指按下");
    console.log("按下"+e.changedTouches[0].clientX);
    console.log("按下"+e.changedTouches[0].clientY);
  },
  handleTouchEnd(e){
    console.log("结束触摸");
    console.log("离开"+e.changedTouches[0].clientX);
    console.log("离开"+e.changedTouches[0].clientY);
  }
}
}
</script>

<style>
view{
width:100%;
height:500rpx;
background-color: aqua;
}
</style>