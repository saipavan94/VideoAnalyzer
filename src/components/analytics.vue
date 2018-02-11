<template>
  <div id="parent">
    <div id="left">
         <p>
           PlayCount {{play}}
         </p>
         <p>
           Pause Count {{pause}}
         </p>
     </div>
    <div id="right">
      <p>
        Tolal View Time {{timer}}
      </p>
      <p>
        Seek values : <span v-for="time in seekedTimeValue">{{time}} &nbsp;&nbsp; </span>
      </p>
    </div>
  </div>
</template>
<script type="text/javascript">
import  {EventBus}  from '@/event-bus.js';

export default {
  props:['play','pause','timer'],
  name: 'analytics',
  data(){
    return{
      seekedTimeValue:[]
    }
  },
  mounted(){
    var that = this;
    EventBus.$on('seekValue', function(seekValue){
      that.seekedTimeValue.push(seekValue);
      console.log(that.seekedTimeValue);
      console.log(seekValue);
    });
  }
}
</script>
<style media="screen">
#parent{
  width: 100%;
}
#right {
 float: right;
 width: 50%;
 text-align: center;
}
#left {
 float: left;
 width: 50%;
 text-align: center;
}
</style>
