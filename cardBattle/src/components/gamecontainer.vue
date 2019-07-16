<template>
 <div>
  <header>
    <div class="row">
      <h1>Card Battle!</h1>
      <section id="game" class="row">
        <!-- 开始组件 -->
        <start-scene></start-scene>
        <!-- 游戏进行的组件 -->
        <game-scene></game-scene>
        <!-- 游戏结束的组件 -->
        <game-over-scene></game-over-scene> 
      </section>
    </div>
  </header>
  <section class='how-to-play'>
    <h2>玩法介绍</h2>
    <p>选择任意一张牌，然后观看点数的pk结果</p>
  </section>
 </div>  
</template>

<script>
  import StartScene from './startscenecomponent'
  import GameScene from './gamescenecomponent'
  import GameOverScene from './gameoverscenecomponent'
  export default {
    components: {
      StartScene,
      GameScene,
      GameOverScene
    }
  }
</script>

<style scoped>
  /* 游戏界面的大小，三个组件都在此页面 */
  #game {
    width: 480px;
    height: 600px;
    border-radius: 8px;
    overflow: hidden;
  }
   
  .scene {
    width: 100%;
    height: 100%;
    position: absolute;
    overflow: hidden;
    border-radius: 8px;
    transition: all .3s ease-out;
  }

  .scene.out {
    transform: translate3d(100%, 0, 0);
  }

  .scene.in {
    transform: translate3d(0, 0, 0)
  }


</style>
