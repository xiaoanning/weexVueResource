<template>
  <div class="body">
      <controller style="width:750px;flex: 1" :src="src" tag="lychee"></controller>
      <controller style="width:500px;flex: 1;margin-top: 20px;"
                  src="http://158.58.9.47:8080/temp/fragment4.js"
                  tag="lychee1"></controller>
      <div class="toolbar">
        <div class="toolbar_btn" @click="function_src(1)">1</div>
        <div class="toolbar_btn" @click="function_src(2)">2</div>
        <div class="toolbar_btn" @click="function_src(3)">3</div>
      </div>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        src : 'http://158.58.9.47:8080/temp/fragment1.js'
      }
    },
    methods: {
      function_src : function(number){
        var _this = this;
        switch (number) {
          case 1:
          _this.src = 'http://158.58.9.47:8080/temp/fragment1.js';
            break;
          case 2:
            _this.src = 'http://158.58.9.47:8080/temp/fragment2.js';
            break;
          case 3:
            _this.src = 'http://158.58.9.47:8080/temp/fragment3.js';
            break;
        }
      }
    }
  }
</script>
<style>
.body{
  flex-direction:  column;
}
.toolbar{
  background-color: #EEE;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  width: 750px;
  height: 80px;
}
.toolbar_btn{
  flex: 1;
  text-align: center;
  align-items: center;
  height: 80px;
  justify-content: center;
}
.toolbar_btn:active{
  background-color: #999;
  height: 80px;
}
</style>
