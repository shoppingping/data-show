<template>
  <div class="world">

  </div>
</template>

<!-- <script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script> -->

<script>


export default {

  // data() {
  //   let data = []
  //   return {}
  // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.world {
  margin: 0;
  padding: 0;
  height: 100vh;
  background: url(../assets/bgWorldMap.jpg);
  background-size: cover;
  animation: animateBg 60s linear infinite;
  opacity: 0.3;
}

@keyframes animateBg {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 1600px 0;
  }
}


</style>
