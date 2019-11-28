<template>
  <div id="app">
    <Halo/>
    <!-- <Earth/> -->

    <!-- <div class="world"></div> -->
    <header id="header">
      <h3 class="header-title">大屏数据展示模板</h3>
     <!--  <div class="header-info header-info-l">数据来源: NASA &amp; 中国航天局</div>
      <div class="header-info header-info-r">数据日期: <span id="nowDate"></span></div> -->
    </header>
    
    <footer id="footer"></footer>


    <Container msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Container from '@/components/Container.vue'
// import Earth from '@/components/Earth.vue'
import Halo from '@/components/Halo.vue'

export default {
  name: 'home',
  components: {
    Container,
    // Earth,
    Halo,
  }
}
</script>

<style lang="scss">



* {margin:0;padding:0;box-sizing:border-box;}
html, body {
  width:100%;
  height:100%;
  min-width:1200px;
  min-height:600px;
  overflow:hidden;
  box-sizing: border-box;
  margin: 0; padding: 0;
  overflow: hidden;
}
body {
  #app{
    // font-family: 'Avenir', Helvetica, Arial, sans-serif;
    // -webkit-font-smoothing: antialiased;
    // -moz-osx-font-smoothing: grayscale;
    text-align: center;
    // color: #2c3e50;
    position:relative;
    width: 100%;
    height: 100%;
    bottom: 0;
    font-family:"Microsoft Yahei", Arial, sans-serif;
    // background:rgb(40, 30, 47) url("./assets/bg.png") 0 0 / 100% 100% no-repeat;
    // background:rgba(20, 10, 139, 1);
    // background:rgba(9, 5, 66, 1);
    // background: #000C1C;
    // background:rgba(9, 5, 6, 1);
    // background:rgba(0, 0, 0, 1);


    #header {
      // position:relative;
      position: absolute;
      top:0;
      left:0;
      right:0;
      height:72px;
      background:url("./assets/header.png") 0 0 / 100% 100% no-repeat;
      overflow:hidden;
    }
    .header-title {line-height:64px;text-align:center;font-size:34px;font-weight:400;color:#fff;}
    .header-info {position:absolute;top:32px;font-size:18px;color:#73aae5;}
    .header-info-l {left:20px;}
    .header-info-r {right:20px;}
    #footer {
      position:absolute;
      bottom:0;
      left:0;
      right:0;
      height:28px;
      background:url("./assets/footer.png") 0 0 / 100% 100% no-repeat;
    }

    .world{
      margin: 0;
      padding: 0;
      height: 100vh;
      // background: url(./assets/bgWorldMap.jpg);
      background: url(./assets/img/world.svg);
      background-size: cover;
      // animation: animateBg 60s linear infinite;
      opacity: 0.9;
    }
  }
}

// @keyframes animateBg {
//   0% {
//     background-position: 0 0;
//   }
//   100% {
//     background-position: 1600px 0;
//   }
// }
</style>
