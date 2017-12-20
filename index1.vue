//<1!--

<template>
  <div>

	<div class = "wrapper0" @click = "startTime">
      <text class="title"> {{startNum}}</text>
    </div>

    <div class="wrapper" @click="update">
      <image src = "http://img1.vued.vanthink.cn/vued08aa73a9ab65dcbd360ec54659ada97c.png" class = "logo"> </image>
      <text class="title">Hello {{target}}</text>
      <text class="desc">******** XIAO, Now, let's use vue to build your weex app.</text>
    </div>

    <div class = "wrapper2" @click = "gotoBaiDu">
      <text class="title"> https://www.baidu.com</text>
    </div>

    <div class = "wrapper3" @click = "getReturnValue">
      <text class="title">{{returnValue}}</text>
    </div>

    <div class = "wrapper4" >
    	<wxbutton class = "button" ref = "wxbuttonjs" @click="button"> </wxbutton>
    </div>

  </div>
</template>

<style>
  .wrapper0 { align-items: center; margin-top: 20px; }
  .wrapper { align-items: center; margin-top: 50px; }
  .wrapper2 { align-items: center; margin-top: 60px; }
  .wrapper3 { align-items: center; margin-top: 60px; }
  .wrapper4 { margin-top: 50px; padding-left:1px;padding-right:1px; margin-right:1px ;margin-left:1px }
  .title { padding-top:20px; padding-bottom: 20px; padding-left:20px; font-size: 48px; text-align:left; }
  .desc { padding-top: 20px; color:#888; font-size: 24px;border-left-style:solid; border-left-width:5px;border-left-color:#000000}
  .logo { width: 360px; height: 156px; }
  .button { font-size:48px ;align:center}
  .button1 {}

</style>

<script>
  export default {
    data: {
      target: 'World',
      returnValue:'please click to get return value',
      startNum:10,
    },
    methods: {

      callback : function(ad) 
      { 
        console.log(this.target)
        this.target = ad

      },
      aliveCallback:function(e)
      {
      	console.log(e)
      	this.startNum = e
      },

      update: function (e) 
      {

        this.target = 'Weex测试'
        var eventModule = weex.requireModule('event')
        eventModule.showAlert(this.target,this.callback)
        console.log('target:', this.target)
      },
      gotoBaiDu:function(e){
        var eventModule = weex.requireModule('eventOpenURL')
        eventModule.openURL('https://www.baidu.com',this.callback)
      },
      getReturnValue:function(e)
      {
        var eventModule = weex.requireModule('event')
        this.returnValue =  eventModule.getString() + '\n'+eventModule.getString()
      },
      button:function(e)
      {
      //wxbuttonjs 为ref属性 自己设置
      	 this.$refs.wxbuttonjs.setTitle('肖湍')
      },
      onEvent:function(e)
      {
        this.target = e
        console.log('============',e)
      },
      startTime:function(e)
      {
        var eventModule = weex.requireModule('timeModule')
        eventModule.time(this.startNum,this.aliveCallback)

      },
    }
  }
</script>

//-->


<!--
//事件冒泡
//需要注意的是: 为了兼容之前的版本，Weex 默认不会开启事件冒泡机制。需要在根元素的属性上，添加 bubble="true" 来开启冒泡机制。否则，将不会向上传播事件，保持与之前版本的效果相同
<template>
	//bubble="true" 来开启冒泡机制 默认false 不开启
	<div class = "root" @click = "rootClick" bubble = "true" >

		<text style = "font-size : 40px;">{{rootText}} </text>

		<div class = "outer" @click = "parentClick" >

			<div>
	        	<text style="font-size: 40px;">{{parentText}}</text>
      		</div>

      		<text class="inner" @click="click">{{innerText}}</text>
   		</div>
  	</div>

</template>

<script>

  module.exports = 
  {

    data: 
    {
      innerText: 'click me',
      parentText: '',
      rootText: ''
    },

    methods: 
    {

      click: function(e) 
      {
        this.innerText = 'inner bubble'
      },


      parentClick: function(e) 
      {
        this.parentText = 'parent bubble'
        //e.stopPropagation() 方法，来阻止本次事件向上的传递过程
        e.stopPropagation()

      },


      rootClick: function(e) 
      {
        this.rootText = 'root bubble'
      },
    }

  }

</script>


<style scoped>

  .inner 
  {
    font-size: 40px;
    text-align: center;
    background-color: #7a9b1b;
    padding: 40px;
  }

  .outer 
  {
    font-size: 40px;
    text-align: center;
    background-color: #9b7a1b;
    padding: 120px;
  }


  .root 
  {
    font-size: 40px;
    text-align: center;
    background-color: #7a1b9b;
    padding: 80px;
  }

</style>

-->