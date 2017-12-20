<style>


  .body
  {
    flex-direction:  column;
    height : this.screenWidth ;
    width : this.screenHeight ;
  }
  .toolbar
  {
    background-color: #EEE;
    display: -webkit-flex;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    position:fixed;
    bottom:0 ;
    left:0;
    right:0;

    height : this.toolbarheight ;

  }
  .toolbar_btn
  {
    flex: 1;

    text-align : center;
    font-size : 24px ;

    display: flex;
    align-items: center;
    justify-content: center;

    height: 100%;

  }
  .toolbar_btntitle
  {
      text-align : center;
  }


</style>




<script>
  
  export default 
  {

    data :
    {
      screenWidth : 0 ,
      screenHeight : 0 ,

      toolBar:
      {
        beSelectedIndex:0,

        menus: 
        [
          {'text':'推荐','selectedText':'被推荐','img':'http://158.58.9.47:8080/dist/error.jpg', 'imgSelected':'http://158.58.9.47:8080/dist/qrcode.png'},
          {'text':'人物','selectedText':'被人物','img':'http://158.58.9.47:8080/dist/error.jpg', 'imgSelected':'http://158.58.9.47:8080/dist/qrcode.png'},
          {'text':'干货','selectedText':'被干货','img':'http://158.58.9.47:8080/dist/error.jpg', 'imgSelected':'http://158.58.9.47:8080/dist/qrcode.png'},
          {'text':'行业','selectedText':'被行业','img':'http://158.58.9.47:8080/dist/error.jpg', 'imgSelected':'http://158.58.9.47:8080/dist/qrcode.png'},
        ],
        height : '88px' ,
        item:
        {
          image:
          {
            height : '58px' ,
            width : '96px' ,
          },
          text:
          {

          },

          selected:
          {
            backgroundColor : 'red' ,
            color : 'blue' ,
            fontSize : '30px' ,
          },
          noSelected:
          {
            backgroundColor : 'blue' ,
            color : 'red' ,
            fontSize : '24px' ,
          },

        },
      
      },
      
      redColor:'red',
      blueColor:'blue',
      isTrue:true,


    },
    methods: 
    {

      startLog:function(a)
      {
          console.log('==========================beSelectedIndex'+"==:"+a);
          this.toolBar.item.image.height = 58/1334*weex.config.env.deviceHeight ;
      },

      switchTab: function (index) 
      {
        console.log('===== : ' + (index == this.toolBar.beSelectedIndex).toString());
        this.toolBar.beSelectedIndex = index;
        this.screenWidth = weex.config.env.deviceWidth ;
        this.screenHeight = weex.config.env.deviceHeight ;
        console.log(index,this.toolBar.beSelectedIndex,this.screenWidth,this.screenHeight);


      },
      setDefaultValue:function()
      {
        this.screenWidth = weex.config.env.deviceWidth ;
        this.screenHeight = weex.config.env.deviceHeight ;
        this.toolBar.beSelectedIndex = 1 ;
      }

    },
    mounted()
    {
        this.startLog('mounted');
        this.setDefaultValue();

    },

    
  }
</script>

<template>
  <div class = "body" >

      <div class = "toolbar" >
        <div  class="toolbar_btn" 
              v-for="(menu,index) in toolBar.menus"
              v-bind:style = "index == toolBar.beSelectedIndex ? toolBar.item.noSelected : toolBar.item.selected">
                <image v-bind:style = "{width:toolBar.item.image.width,height:toolBar.item.image.height}"
                        v-bind:placeholder = "menu.img"
                        v-bind:src =  "index == toolBar.beSelectedIndex ? menu.img : menu.imgSelected"
                        resize = 'cover'
                ></image>


                <text class = "toolbar_btntitle"
                      v-bind:style = "index == toolBar.beSelectedIndex ? toolBar.item.selected : toolBar.item.noSelected">{{ index == toolBar.beSelectedIndex ?menu.selectedText : menu.text }}</text>
                <button style = "position: absolute;height:100%;width:100%;backgroundColor:rgba(0, 0, 0, 0.0)" v-on:click="switchTab(index)"></button>
        </div>

      </div>
  </div>
</template>





<!--
      divStyle : 
      {
        backgroundColor : '#666' ,
        fontSize:'28px',
      },
-->
<!--
   v-bind:style="divStyle" 
-->

<!--
  .toolbar_btn:active
  {
    background-color: #555;
    height: 80px;
  }

动态改变样式
1.
                v-bind:style = " { color: index == beSelectedIndex ? redColor : blueColor,backgroundColor:index == beSelectedIndex ? blueColor : redColor}"
2.
              v-bind:style = "index == beSelectedIndex ? tabbarItemSelected : tabbarItemNoSelected"
3.
                    {
                      backgroundColor:index == beSelectedIndex?red:blue,
                      color:index == beSelectedIndex?blue:red,
                      fontSize:index == beSelectedIndex?30:24,
                      height:weex.config.env.deviceHeight*36/1334,
                      }

标签显示与否：
1.v-if v-else



this.$getConfig() 舍弃 新的用weex.config

获取当前全局环境变量和配置信息。

Returns:

  config (object): 配置对象；
  bundleUrl (string): bundle 的 url；
  debug (boolean): 是否是调试模式；
  env (object): 环境对象； 
    weexVersion (string): Weex sdk 版本；
    appName (string): 应用名字；
    appVersion (string): 应用版本；
    platform (string): 平台信息，是 iOS、Android 还是 Web；
    osVersion (string): 系统版本；
    deviceModel (string): 设备型号 （仅原生应用）；
    deviceWidth (number): 设备宽度，默认为 750，满屏是750；
    deviceHeight (number): 设备高度。

应用：
在元素标签中使用：
    <div class='flex' style='position: fixed; bottom: 0; width: {{$getConfig().env.deviceWidth}}px;'>
在组件的方法中通过 this （Vm）上下文访问这些 API：
somemethod: function() {
      this.$getConfig().env.deviceWidth;
    }

  注意：
  坑： 标签要写规范 div上加点击 在客户端可以响应 但浏览器不能响应 得用button
-->
