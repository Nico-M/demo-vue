<template>
  <div ref="chart" class="stacked-bar-chart"></div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: 'StackedBarChart',
  props: {
    chartData: {
      type: Array,
      default: () => [
        { name: 'HK本部公司', values: [80, 90, 95] },
        { name: 'QY公司', values: [85, 95, 100] },
        { name: 'CSJ分公司', values: [75, 85, 90] },
        { name: 'AH区域公司', values: [70, 80, 85] },
        { name: 'JX区域公司', values: [90, 95, 98] },
        { name: 'HN区域公司', values: [85, 90, 95] },
        { name: 'HB区域公司', values: [65, 75, 80] },
        { name: 'SY区域公司', values: [75, 85, 90] }
      ]
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
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        grid: {
          top: '3%',
          left: '15%',
          right: '5%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'value',
          max: 100,
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            show: false
          },
          splitLine: {
            show: false
          }
        },
        yAxis: {
          type: 'category',
          inverse: true,
          data: this.chartData.map(item => item.name),
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#7ec7ff',
            fontSize: 14,
            margin: 20
          }
        },
        series: [
          {
            name: '指标1',
            type: 'bar',
            stack: 'total',
            barWidth: 20,
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [
                { offset: 0, color: 'rgba(0, 255, 214, 0.1)' },
                { offset: 1, color: '#00ffd6' }
              ]),
              borderRadius: [0, 20, 20, 0]
            },
            data: this.chartData.map(item => item.values[0])
          },
          {
            name: '指标2',
            type: 'bar',
            stack: 'total',
            barWidth: 20,
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [
                { offset: 0, color: 'rgba(41, 121, 255, 0.1)' },
                { offset: 1, color: '#2979ff' }
              ]),
              borderRadius: [0, 20, 20, 0]
            },
            data: this.chartData.map(item => item.values[1])
          },
          {
            name: '指标3',
            type: 'bar',
            stack: 'total',
            barWidth: 20,
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [
                { offset: 0, color: 'rgba(255, 186, 0, 0.1)' },
                { offset: 1, color: '#ffba00' }
              ]),
              borderRadius: [0, 20, 20, 0]
            },
            data: this.chartData.map(item => item.values[2])
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
.stacked-bar-chart {
  width: 100%;
  height: 100%;
  background: transparent;
}
</style> 
