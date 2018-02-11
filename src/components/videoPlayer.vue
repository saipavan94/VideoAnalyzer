<template>
  <div class="container">
    <video  width="65%" ref="videoPlayer" controls controlsList="nodownload">
        <source src="../assets/mov_bbb.mp4" type="video/mp4">
        <source src="mov_bbb.ogg" type="video/ogg">
        Your browser does not support HTML5 video.
   </video>
  </div>
</template>

<script type="text/javascript">

  export default {
    name: 'videoPlayer',
    data(){
      return{
        playCounter:0,
        pauseCounter:0,
        timer:0
      }
    },
   mounted: function () {
      var that = this;
      var vid = this.$refs.videoPlayer;
      var timer = new Timer();
      vid.onplay = function(){
        console.log(that.playCounter);
        that.playCounter +=1;
        that.$emit('playCounter',  that.playCounter );
        console.log("PLAY");
        timer.start({callback: function (t) {
          console.log(t.toString(['hours', 'minutes', 'seconds']));
          that.timer = t.toString(['hours', 'minutes', 'seconds']);
          that.$emit('timer',  that.timer )

        }});
      }
      vid.onpause = function() {
        that.pauseCounter +=1;
        that.$emit('pauseCounter',  that.pauseCounter )

        console.log("PAUSE");
        timer.pause();
      };
      vid.onseeked = function(e) {
        that.$emit('seekedTimeValue',  vid.currentTime )
      };
      timer.addEventListener('secondsUpdated', function (e) {
        console.log("inn");
      });

  }
}
</script>
<style media="screen">
.container{
  text-align: center;
}
</style>
