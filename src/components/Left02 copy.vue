<template>
  <div>
    <info-card :frontType="'graph'"
      :frontTitle="front.title"
      :frontData="front.graphData"
      :backTitle="back.title"
      :backData="back.message" />
  </div>
</template>


<script>

import InfoCard from 'vue-info-card';

export default {
  // name: 'info-card',
  components: {
    InfoCard,
  },
  data() {
    return {
      front: {
        title: 'Daily Conversion Value',
        graphData: [3, 2, 5, 9, 5, 10, 3, 5, 0, 0, 1, 8, 2, 9, 0],
      },
      back: {
        title: 'Monthly Summary',
        message: 'Your average daily conversion value for this month is <b>50.4$</b>. It is below the average of the last six months.',
      },
    };
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
// .echarts{
// }
#center2{
  width: 100%;
  height: 100%;
  border: rgba(255,255,255,0.2) solid 1px;
  border-radius: 12px;
  background-color: rgba(255,255,255,0.06);
}
</style>
