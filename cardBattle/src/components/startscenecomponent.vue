<template>
  <div id="start-scene" class="scene">
    <a href="#" id="start-btn" class="button" @click="startBtnClick()"></a>
  </div>
</template>

<script>
  import Constant from './constant'
  export default {
    methods: {
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
