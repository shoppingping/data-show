<template>

  <div class="earth" ref="chartdiv">
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
import * as am4core from "@amcharts/amcharts4/core";
// import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";

import * as am4maps from "@amcharts/amcharts4/maps";
import am4geodata_worldLow from "@amcharts/amcharts4-geodata/worldLow";


// Themes begin
am4core.useTheme(am4themes_animated);
// Themes end


export default {

  // name: 'Earth',
  // data() {
  //   let data = []
  //   return {}
  // }
  mounted(){
    // console.log('this.initEarth()',typeof(this.initEarth()));
    // this.initChart();
    // this.initEarth();

      var chart = am4core.create(this.$refs.chartdiv, am4maps.MapChart);


      // Set map definition
      chart.geodata = am4geodata_worldLow;


      // Set projection
      chart.projection = new am4maps.projections.Orthographic();
      chart.panBehavior = "rotateLongLat";
      chart.deltaLatitude = 10;
      // chart.padding(20,20,20,20);


      // Create map polygon series
      var polygonSeries = chart.series.push(new am4maps.MapPolygonSeries());


      // Make map load polygon (like country names) data from GeoJSON
      polygonSeries.useGeodata = true;


      // Configure series
      // 国家形状配置
      var polygonTemplate = polygonSeries.mapPolygons.template;
      // polygonTemplate.tooltipText = "{name}";
      // polygonTemplate.fill = am4core.color("#47c78a");
      polygonTemplate.fill = am4core.color("rgba(35, 160, 250, 0.1)");
      // polygonTemplate.stroke = am4core.color("#454a58");
      // polygonTemplate.stroke = am4core.color("rgba(90, 180, 250, 0.9)");
      polygonTemplate.stroke = am4core.color("rgba(4, 74, 143, 0.1)");
      polygonTemplate.strokeWidth = 1.4;


      // 经纬线
      // var graticuleSeries = chart.series.push(new am4maps.GraticuleSeries());
      // graticuleSeries.mapLines.template.line.stroke = am4core.color("#ffffff");
      // graticuleSeries.mapLines.template.line.strokeOpacity = 0.08;
      // graticuleSeries.fitExtent = false;

      let colors = {
        ocean:"rgba(4, 74, 143, 0.9)",
      }
      chart.backgroundSeries.mapPolygons.template.polygon.fillOpacity = 0.2;
      chart.backgroundSeries.mapPolygons.template.polygon.fill = am4core.color(colors.ocean);


      // Create hover state and set alternative fill color
      // var hs = polygonTemplate.states.create("hover");
      // hs.properties.fill = chart.colors.getIndex(0).brighten(-0.5);


      let animation;
      setTimeout(function(){
        animation = chart.animate({property:"deltaLongitude", to:40000}, 20000000);
        // animation = chart.animate({property:"deltaLatitude", to:10000}, 2000000);
        // animation = chart.animate({property:"deltaGamma", to:10000}, 2000000);
      }, 3000)

      chart.seriesContainer.events.on("down", function(){
        if(animation){
          animation.stop();
        }
      })







      
  },

  // beforeDestroy() {
  //   if (this.chart) {
  //     this.chart.dispose();
  //   }
  // },

  method: {
    initEarth(){
      console.log('initEarth')
    },

    // initChart(){
    //   let chart = am4core.create(this.$refs.chartdiv, am4charts.XYChart);

    //   chart.paddingRight = 20;

    //   let data = [];
    //   let visits = 10;
    //   for (let i = 1; i < 366; i++) {
    //     visits += Math.round((Math.random() < 0.5 ? 1 : -1) * Math.random() * 10);
    //     data.push({ date: new Date(2018, 0, i), name: "name" + i, value: visits });
    //   }

    //   chart.data = data;

    //   let dateAxis = chart.xAxes.push(new am4charts.DateAxis());
    //   dateAxis.renderer.grid.template.location = 0;

    //   let valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
    //   valueAxis.tooltip.disabled = true;
    //   valueAxis.renderer.minWidth = 35;

    //   let series = chart.series.push(new am4charts.LineSeries());
    //   series.dataFields.dateX = "date";
    //   series.dataFields.valueY = "value";

    //   series.tooltipText = "{valueY.value}";
    //   chart.cursor = new am4charts.XYCursor();

    //   let scrollbarX = new am4charts.XYChartScrollbar();
    //   scrollbarX.series.push(series);
    //   chart.scrollbarX = scrollbarX;

    //   this.chart = chart;
    // }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.earth {
  width: 160%;
  // height: 100%;
  bottom: 0;
  height: 2300px;
  top: 200px;
  left: -30%;
}


</style>
