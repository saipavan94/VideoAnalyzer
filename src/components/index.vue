<template>
  <div class="">
    <h1 >{{title}}</h1>
    <div>
      <div id="container">  </div>
      <video  width="65%" ref="videoPlayer" controls>
          <source src="../assets/mov_bbb.mp4" type="video/mp4">
          <source src="mov_bbb.ogg" type="video/ogg">
          Your browser does not support HTML5 video.
     </video>
     <div id="parent">
       <div id="left">
            <p>
              PlayCount {{playCounter}}
            </p>
            <p>
              Pause Count {{pauseCounter}}
            </p>
        </div>
       <div id="right">
         <p>
           Tolal View Time {{timer}}
         </p>
         <p>
           Seek values : <span v-for="time in seekedTimeValues">{{time}} &nbsp;&nbsp; </span>
         </p>
       </div>
     </div>
    </div>

  </div>

</template>

<script type="text/javascript">

  export default {
    name: 'index',
    data(){
      return{
        title : 'Video Player Analyzer',
        playCounter:0,
        pauseCounter:0,
        seekedTimeValues : [],
        timer:0
      }
    },
    computed:{
      // timerValue : function(){
      //   return this.timer.getTimeValues().toString();
      // }
    },
   mounted: function () {
      var that = this;
      var vid = this.$refs.videoPlayer;
      var timer = new Timer();
      vid.onplay = function(){
        console.log(that.playCounter);
        that.playCounter +=1;
        console.log("PLAY");
        timer.start({callback: function (t) {
          console.log(t.toString(['hours', 'minutes', 'seconds']));
          that.timer = t.toString(['hours', 'minutes', 'seconds']);
        }});
      }
      vid.onpause = function() {
        that.pauseCounter +=1;
        console.log("PAUSE");
        timer.pause();
      };
      vid.onplay
      vid.onseeked = function(e) {
        that.seekedTimeValues.push(vid.currentTime);
        console.log(that.seekedTimeValues);
      };
      timer.addEventListener('secondsUpdated', function (e) {
        console.log("inn");
      });

  }
}
</script>
<style >
#right {
 float: right;
 width: 50%;
 text-align: center;
}
#left {
 float: left;
 width: 50%;
}
</style>
