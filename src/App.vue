<template>
  <div id="app">
    <v-time :lefttime='lefttime' :type='testType' @handleEnd='handletime'></v-time>
  </div>
</template>

<script>
import Time from './components/time.vue'

export default {
  name: 'app',
  data () {
    return {
      testType: "two",     //放置时间的容器样式
      lefttime: "1500274821" //开奖的时间戳
    }
  },
  components: {
    'v-time': Time,
  },
  methods: {
    handletime: function(){
      alert('end');
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
