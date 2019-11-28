<template>
  <v-chart class="dashboard" :options="polar"/>
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
import ECharts from 'vue-echarts'
import 'echarts/lib/chart/line'
import 'echarts/lib/chart/gauge'
import 'echarts/lib/component/polar'

export default {
  components: {
    'v-chart': ECharts
  },
  data () {
    let data = []

    for (let i = 0; i <= 360; i++) {
        let t = i / 180 * Math.PI
        let r = Math.sin(2 * t) * Math.cos(2 * t)
        data.push([r, i])
    }

    return {
      polar: {
        // title: {
        //   text: '极坐标双数值轴'
        // },
        // legend: {
        //   data: ['line']
        // },
        // polar: {
        //   center: ['50%', '54%']
        // },
        // tooltip: {
        //   trigger: 'axis',
        //   axisPointer: {
        //     type: 'cross'
        //   }
        // },
        // angleAxis: {
        //   type: 'value',
        //   startAngle: 0
        // },
        // radiusAxis: {
        //   min: 0
        // },
        // animationDuration: 2000,
        // backgroundColor: '#1b1b1b',
        tooltip : {
            formatter: "{a} <br/>{c} {b}"
        },
        toolbox: {
            show : true,
            feature : {
                mark : {show: true},
                restore : {show: true},
                saveAsImage : {show: true}
            }
        },
        series: [
          // {
          //   coordinateSystem: 'polar',
          //   name: 'line',
          //   type: 'line',
          //   showSymbol: false,
          //   data: data
          // }
          {
            name:'速度',
            type:'gauge',
            min:0,
            max:100,
            splitNumber:5,
            radius: '60%',
            axisLine: {            // 坐标轴线
                lineStyle: {       // 属性lineStyle控制线条样式
                    color: [[0.09, 'lime'],[0.82, '#1e90ff'],[1, '#ff4500']],
                    width: 1,
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            axisLabel: {            // 坐标轴小标记
                textStyle: {       // 属性lineStyle控制线条样式
                    fontWeight: 'bolder',
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            axisTick: {            // 坐标轴小标记
                length :15,        // 属性length控制线长
                lineStyle: {       // 属性lineStyle控制线条样式
                    color: 'auto',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            splitLine: {           // 分隔线
                length :25,         // 属性length控制线长
                lineStyle: {       // 属性lineStyle（详见lineStyle）控制线条样式
                    width:3,
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            pointer: {           // 分隔线
                shadowColor : '#fff', //默认透明
                shadowBlur: 5
            },
            title : { 
                offsetCenter: [16, '100%'],
                textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    fontSize: 12,
                    fontStyle: 'italic',
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10,
                }
            },
            detail : {
                // backgroundColor: 'rgba(30,144,255,0.8)',
                // borderWidth: 1,
                // borderColor: '#fff',
                shadowColor : '#fff', //默认透明
                shadowBlur: 5,
                offsetCenter: [-16, '100%'],       // x, y，单位px
                textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    color: '#fff',
                    fontSize: 12,
                }
            },
            data:[{value: 40, name: 'km/h'}],
          },
          {
            name:'转速',
            type:'gauge',
            center : ['20%', '55%'],    // 默认全局居中
            radius : '66%',
            min:0,
            max:100,
            endAngle:50,
            splitNumber:4,
            axisLine: {            // 坐标轴线
                lineStyle: {       // 属性lineStyle控制线条样式
                    color: [[0.29, 'lime'],[0.86, '#1e90ff'],[1, '#ff4500']],
                    width: 1,
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            axisLabel: {            // 坐标轴小标记
                textStyle: {       // 属性lineStyle控制线条样式
                    fontWeight: 'bolder',
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            axisTick: {            // 坐标轴小标记
                length :12,        // 属性length控制线长
                lineStyle: {       // 属性lineStyle控制线条样式
                    color: 'auto',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            splitLine: {           // 分隔线
                length :20,         // 属性length控制线长
                lineStyle: {       // 属性lineStyle（详见lineStyle）控制线条样式
                    width:3,
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            pointer: {
                width:5,
                shadowColor : '#fff', //默认透明
                shadowBlur: 5
            },
            title : {
                offsetCenter: [16, '80%'],       // x, y，单位px
                textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    fontStyle: 'italic',
                    fontSize: 12,
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            detail : {
                //backgroundColor: 'rgba(30,144,255,0.8)',
               // borderWidth: 1,
                borderColor: '#fff',
                shadowColor : '#fff', //默认透明
                shadowBlur: 5,
                width: 80,
                height: 30,
                offsetCenter: [-16, '80%'],       // x, y，单位px
                textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    color: '#fff',
                    fontSize: 12,
                }
            },
            data:[{value: 1.5, name: 'x1000 r/min'}]
          },
          {
            name:'转速',
            type:'gauge',
            center : ['80%', '55%'],    // 默认全局居中
            radius : '66%',
            min:0,
            max:100,
            startAngle: 130,
            // endAngle: 50,
            splitNumber:4,
            axisLine: {            // 坐标轴线
                lineStyle: {       // 属性lineStyle控制线条样式
                    color: [[0.29, 'lime'],[0.86, '#1e90ff'],[1, '#ff4500']],
                    width: 1,
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            axisLabel: {            // 坐标轴小标记
                textStyle: {       // 属性lineStyle控制线条样式
                    fontWeight: 'bolder',
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            axisTick: {            // 坐标轴小标记
                length :12,        // 属性length控制线长
                lineStyle: {       // 属性lineStyle控制线条样式
                    color: 'auto',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            splitLine: {           // 分隔线
                length :20,         // 属性length控制线长
                lineStyle: {       // 属性lineStyle（详见lineStyle）控制线条样式
                    width:3,
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            pointer: {
                width:5,
                shadowColor : '#fff', //默认透明
                shadowBlur: 5
            },
            title : {
                offsetCenter: [16, '80%'],       // x, y，单位px
                textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    fontStyle: 'italic',
                    fontSize: 12,
                    color: '#fff',
                    shadowColor : '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            detail : {
                //backgroundColor: 'rgba(30,144,255,0.8)',
               // borderWidth: 1,
                borderColor: '#fff',
                shadowColor : '#fff', //默认透明
                shadowBlur: 5,
                width: 80,
                height: 30,
                offsetCenter: [-16, '80%'],       // x, y，单位px
                textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    color: '#fff',
                    fontSize: 12,
                }
            },
            data:[{value: 1.5, name: 'x1000 r/min'}]
          },
          // {
          //   name:'油表',
          //   type:'gauge',
          //   center : ['75%', '50%'],    // 默认全局居中
          //   radius : '30%',
          //   min:0,
          //   max:2,
          //   startAngle:135,
          //   endAngle:45,
          //   splitNumber:2,
          //   axisLine: {            // 坐标轴线
          //       lineStyle: {       // 属性lineStyle控制线条样式
          //           color: [[0.2, 'lime'],[0.8, '#1e90ff'],[1, '#ff4500']],
          //           width: 2,
          //           shadowColor : '#fff', //默认透明
          //           shadowBlur: 10
          //       }
          //   },
          //   axisTick: {            // 坐标轴小标记
          //       length :12,        // 属性length控制线长
          //       lineStyle: {       // 属性lineStyle控制线条样式
          //           color: 'auto',
          //           shadowColor : '#fff', //默认透明
          //           shadowBlur: 10
          //       }
          //   },
          //   axisLabel: {
          //       textStyle: {       // 属性lineStyle控制线条样式
          //           fontWeight: 'bolder',
          //           color: '#fff',
          //           shadowColor : '#fff', //默认透明
          //           shadowBlur: 10
          //       },
          //       formatter:function(v){
          //           switch (v + '') {
          //               case '0' : return 'E';
          //               case '1' : return 'Gas';
          //               case '2' : return 'F';
          //           }
          //       }
          //   },
          //   splitLine: {           // 分隔线
          //       length :15,         // 属性length控制线长
          //       lineStyle: {       // 属性lineStyle（详见lineStyle）控制线条样式
          //           width:3,
          //           color: '#fff',
          //           shadowColor : '#fff', //默认透明
          //           shadowBlur: 10
          //       }
          //   },
          //   pointer: {
          //       width:2,
          //       shadowColor : '#fff', //默认透明
          //       shadowBlur: 5
          //   },
          //   title : {
          //       show: false
          //   },
          //   detail : {
          //       show: false
          //   },
          //   data:[{value: 0.5, name: 'gas'}]
          // },
          // {
          //   name:'水表',
          //   type:'gauge',
          //   center : ['75%', '50%'],    // 默认全局居中
          //   radius : '30%',
          //   min:0,
          //   max:2,
          //   startAngle:315,
          //   endAngle:225,
          //   splitNumber:2,
          //   axisLine: {            // 坐标轴线
          //       lineStyle: {       // 属性lineStyle控制线条样式
          //           color: [[0.2, 'lime'],[0.8, '#1e90ff'],[1, '#ff4500']],
          //           width: 2,
          //           shadowColor : '#fff', //默认透明
          //           shadowBlur: 10
          //       }
          //   },
          //   axisTick: {            // 坐标轴小标记
          //       show: false
          //   },
          //   axisLabel: {
          //       textStyle: {       // 属性lineStyle控制线条样式
          //           fontWeight: 'bolder',
          //           color: '#fff',
          //           shadowColor : '#fff', //默认透明
          //           shadowBlur: 10
          //       },
          //       formatter:function(v){
          //           switch (v + '') {
          //               case '0' : return 'H';
          //               case '1' : return 'Water';
          //               case '2' : return 'C';
          //           }
          //       }
          //   },
          //   splitLine: {           // 分隔线
          //       length :15,         // 属性length控制线长
          //       lineStyle: {       // 属性lineStyle（详见lineStyle）控制线条样式
          //           width:3,
          //           color: '#fff',
          //           shadowColor : '#fff', //默认透明
          //           shadowBlur: 10
          //       }
          //   },
          //   pointer: {
          //       width:2,
          //       shadowColor : '#fff', //默认透明
          //       shadowBlur: 5
          //   },
          //   title : {
          //       show: false
          //   },
          //   detail : {
          //       show: false
          //   },
          //   data:[{value: 0.5, name: 'gas'}]
          // },
        ],
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.echarts{
  width: 100%;
  height: 100%;
  border: rgba(255,255,255,0.2) solid 1px;
  border-radius: .3em 5em .3em .3em;
  background-color: rgba(255,255,255,0.06);
}
</style>
