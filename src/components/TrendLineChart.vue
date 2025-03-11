<template>
  <div ref="chart" class="trend-line-chart"></div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: 'TrendLineChart',
  props: {
    chartData: {
      type: Object,
      default: () => ({
        halfYear: [250, 400, 350, 650, 400, 250, 300],
        thisYear: [300, 450, 620, 250, 300, 350, 400],
        lastYear: [200, 300, 250, 400, 600, 850, 600]
      })
    }
  },
  mounted() {
    this.initChart();
    window.addEventListener('resize', this.resizeHandler);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.resizeHandler);
    if (this.chart) this.chart.dispose();
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$refs.chart);
      
      const option = {
        backgroundColor: 'transparent',
        legend: {
          data: ['近半年', '本年', '近一年'],
          textStyle: {
            color: '#fff'
          },
          top: 10,
          right: 20
        },
        grid: {
          top: '15%',
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['2018', '2019', '2020', '2021', '2022', '2023', '2024'],
          axisLine: {
            lineStyle: {
              color: '#183b5d'
            }
          },
          axisLabel: {
            color: '#7ec7ff'
          }
        },
        yAxis: {
          type: 'value',
          min: 0,
          max: 1000,
          splitNumber: 4,
          axisLine: {
            lineStyle: {
              color: '#183b5d'
            }
          },
          splitLine: {
            lineStyle: {
              color: '#183b5d',
              opacity: 0.3
            }
          },
          axisLabel: {
            color: '#7ec7ff'
          }
        },
        series: [
          {
            name: '近半年',
            type: 'line',
            smooth: true,
            lineStyle: {
              width: 3,
              color: '#ffba00'
            },
            areaStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: 'rgba(255, 186, 0, 0.3)' },
                { offset: 1, color: 'rgba(255, 186, 0, 0)' }
              ])
            },
            data: this.chartData.halfYear
          },
          {
            name: '本年',
            type: 'line',
            smooth: true,
            lineStyle: {
              width: 3,
              color: '#2979ff'
            },
            areaStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: 'rgba(41, 121, 255, 0.3)' },
                { offset: 1, color: 'rgba(41, 121, 255, 0)' }
              ])
            },
            data: this.chartData.thisYear
          },
          {
            name: '近一年',
            type: 'line',
            smooth: true,
            lineStyle: {
              width: 3,
              color: '#00ffd6'
            },
            areaStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: 'rgba(0, 255, 214, 0.3)' },
                { offset: 1, color: 'rgba(0, 255, 214, 0)' }
              ])
            },
            data: this.chartData.lastYear
          }
        ]
      };

      this.chart.setOption(option);
    },
    resizeHandler() {
      if (this.chart) this.chart.resize();
    }
  },
  watch: {
    chartData: {
      handler() {
        this.initChart();
      },
      deep: true
    }
  }
}
</script>

<style lang="scss" scoped>
.trend-line-chart {
  width: 100%;
  height: 100%;
}
</style> 
