<template>
  <div id="start-scene" class="scene">
    <!-- 使整个开始页面可点击，触发一个事件，加载到游戏界面 -->
    <a href="#" id="start-btn" class="button" @click="startBtnClick()"></a>
  </div>
</template>

<script>
  import Constant from './constant'
  export default {
    methods: {
      // 触发事件，事件向vue的消息管道广播一个消息
      startBtnClick () {
        Constant.Event.$emit(Constant.MSG_START_SCENE)
      }
    }
  }
</script>

<style scoped>
  #start-scene {background: url(../../static/images/start-scene-bg.png) no-repeat;}

  .button {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
  }
</style>
