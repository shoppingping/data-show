<template>
    <div id="container">
        <div id="flexCon">

            <div class="flex-row">
                <div class="flex-cell flex-cell-l">
                    <div class="chart-wrapper">
                        <h3 class="chart-title">系统运维管理指标</h3>
                        <div class="chart-div" id="rankChart">
                          <DashBoard />
                        </div>
                    </div>
                </div>
                <div class="flex-cell flex-cell-c" id="earth">
                    <div class="chart-wrapper">
                        <!-- <h3 class="chart-title">系统运行整体指标分析</h3> -->
                        <div class="chart-div chart-done">
                          <Left02 />
                        </div>
                    </div>
                </div>
                <div class="flex-cell flex-cell-r">
                    <div class="chart-wrapper">
                        <h3 class="chart-title">变更类型分析</h3>
                        <div class="chart-div" id="mapChart">
                          <DashBoard />
                        </div>
                    </div>
                </div>
            </div>

            <div class="flex-row">
                <div class="flex-cell flex-cell-l" style="padding-bottom:0;">
                    <div class="chart-wrapper">
                        <h3 class="chart-title">2018年月度股票情况及预测</h3>
                        <div class="chart-div" id="trendChart">
                        </div>
                    </div>
                </div>
                <div class="flex-cell flex-cell-c" style="padding-bottom:0;">
                    <div class="chart-wrapper">
                        <!-- <h3 class="chart-title">2018年月度股票情况及预测</h3> -->
                        <div class="chart-div" id="trendChart">
                          <!-- <DashBoard /> -->
                        </div>
                    </div>
                </div>
                <div class="flex-cell flex-cell-r" style="padding-bottom:0;">
                    <div class="chart-wrapper">
                        <h3 class="chart-title">CSRC行业分类</h3>
                        <div class="chart-div" id="csrcChart">
                          <DashBoard />
                        </div>
                    </div>
                </div>
            </div>


            <div class="flex-row">
                <div class="flex-cell flex-cell-l">
                    <div class="chart-wrapper">
                        <h3 class="chart-title">系统运维管理指标</h3>
                        <div class="chart-div" id="rankChart">
                          <DashBoard />
                        </div>
                    </div>
                </div>
                <div class="flex-cell flex-cell-c" id="earth">
                    <div class="chart-wrapper">
                        <!-- <h3 class="chart-title">系统运行整体指标分析</h3> -->
                        <div class="chart-div chart-done">

                          <Center02 />
                        </div>
                    </div>
                </div>
                <div class="flex-cell flex-cell-r">
                    <div class="chart-wrapper">
                        <h3 class="chart-title">变更类型分析</h3>
                        <div class="chart-div" id="mapChart">
                          <DashBoard />
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>
<script>
// @ is an alias to /src
import DashBoard from '@/components/DashBoard.vue'
// import Earth from '@/components/Earth.vue'
import Left02 from '@/components/Left02.vue'
import Center02 from '@/components/Center02.vue'

export default {
    name: 'Container',
    components: {
        DashBoard,
        // Earth,
        Left02,
        Center02,
    }
}
</script>
<style scoped lang="scss">
@charset "utf-8";


/* global */


/* layout */
#container {
    position: absolute;
    top: 8px;
    bottom: 22px;
    left: 0;
    right: 0;
}

#flexCon {
    height: 100%;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-flex-direction: column;
    -ms-flex-direction: column;
    flex-direction: column;
}

.flex-row {
    -webkit-flex: 1;
    -ms-flex: 1;
    flex: 1;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
}

.flex-cell {
    -webkit-flex: 1;
    -ms-flex: 1;
    flex: 1;
    padding: 8px;
}

.flex-cell-l,
.flex-cell-r {
    -webkit-flex: 2;
    -ms-flex: 2;
    flex: 2;
}

.flex-cell-c {
  -webkit-flex: 3;
  -ms-flex: 3;
  flex: 3;
  &#earth{
    position: relative;
    top: 32px;
    height: 200%;
    // bottom: -300px;
  }
}

.flex-cell-lc {
    -webkit-flex: 5;
    -ms-flex: 5;
    flex: 5;
}

.chart-wrapper {
    position: relative;
    height: 100%;
}

.chart-title {
    height: 32px;
    font-size: 22px;
    font-weight: normal;
    color: #9aa8d4;
}

.chart-div {
    position: absolute;
    top: 32px;
    bottom: 0;
    left: 0;
    right: 0;
}

.data-t {
    table-layout: fixed;
    width: 100%;
    height: 100%;
    border-collapse: collapse;
}

.data-t th,
.data-t td {
    min-height: 48px;
}

.data-t th {
    width: 60px;
    text-align: center;
    background: url("../assets/icon-bg.png") center / 100% no-repeat;
}

.data-t th img {
    width: 30px;
    height: 30px;
}

.data-t td {
    padding-left: 15px;
}

.data-t p {
    margin: 5px 0;
    line-height: 1;
    font-size: 14px;
    color: #b0c2f9;
}

.data-t p span {
    font-size: 32px;
    font-weight: bold;
    color: #fff;
}

/* media query */
@media (max-width:1900px) {
    #header {
        height: 48px;
    }

    .header-title {
        line-height: 42px;
        font-size: 24px;
    }

    .header-info {
        top: 17px;
        font-size: 14px;
    }

    .header-info-l {
        left: 15px;
    }

    .header-info-r {
        right: 15px;
    }

    .flex-cell {
        padding: 10px;
    }

    .chart-title {
        height: 24px;
        font-size: 18px;
    }

    .chart-div {
        top: 24px;
    }

    .data-t p span {
        font-size: 24px;
    }

    #footer {
        height: 16px;
    }

    #container {
        top: 48px;
        bottom: 12px;
    }
}

/* chart-loader */


/* charts */
</style>