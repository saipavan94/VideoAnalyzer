<template>
  <div id="app">
    <header-component></header-component>
    <video-player @pauseCounter="pauseCount = $event" @playCounter="playCount = $event" @timer="timer = $event" @seekedTimeValue="addSeekedTimeValues($event)"></video-player>
    <analytics-component :play="playCount" :pause="pauseCount" :timer="timer" ></analytics-component>
  </div>
</template>

<script>
import videoPlayer from '@/components/videoPlayer'
import header from '@/components/header'
import analytics from '@/components/analytics'
import {EventBus}  from '@/event-bus.js';


// import SideBar from './SideBar.vue'

export default {
  name: 'App',
  components: {
    'video-player': videoPlayer,
    'header-component':header,
    'analytics-component' : analytics
  },
  data(){
    return{
      playCount:0,
      pauseCount:0,
      timer:'',
      seekedTimeValue:[]
    }
  },
  methods:{
    addSeekedTimeValues(data){
      console.log(data);
      EventBus.$emit('seekValue', data);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
.center{
text-align: center;

}
</style>
