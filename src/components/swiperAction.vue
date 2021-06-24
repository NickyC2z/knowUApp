/* 
1.slot 占位符
2.对外提供数据 滑动的方向
 */
 <template>
   <view
    @touchstart="handleTouchStart"
    @touchend="handleTouchEnd">
     <slot></slot>
   </view>
 </template>
 
 <script>
  export default {
    data(){
      return{
        starTime:0,
        endTime:0,
        startX:0,
        startY:0
      };
    },
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
  //用户按下屏幕
  handleTouchStart(e){
    //console.log("手指按下");
    //console.log("按下"+e.changedTouches[0].clientX);
    //console.log("按下"+e.changedTouches[0].clientY);
    this.startTime = Date.now();
    this.startX = e.changedTouches[0].clientX;
    this.startY = e.changedTouches[0].clientY;

  },
  handleTouchEnd(e){
    //console.log("结束触摸");
    //console.log("离开"+e.changedTouches[0].clientX);
    //console.log("离开"+e.changedTouches[0].clientY);
    const endTime = Date.now();
    const endX = e.changedTouches[0].clientX;
    const endY = e.changedTouches[0].clientY;
    //判断按下的时长
  if(endTime - this.startTime > 2000){
    return;
  }
  //滑动的方向
  let direction = "";
  //先判断用户滑动的距离 是否合法 合法：判断滑动的方向
  if( Math.abs(endX-this.startX)>10&&Math.abs(endY-this.startY)<10){
    //滑动方向
    direction = endX -this.startX > 0 ?"right" : "left";
  }else{
    return;
  }
  //用户做了合法的滑动操作
  //console.log(direction);
  this.$emit("swiperAction",{direction});
  }
  

}
}
 </script>
 
 <style>
 
 </style>