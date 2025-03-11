<!-- PieChart.vue -->
<template>
  <div ref="chart" class="echarts-bar"></div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  props: {
    chartData: Object, // 饼图的数据
  },
  mounted() {
    this.renderBarChart();
  },
  methods: {
    renderBarChart() {
      const { chart } = this.$refs;

      const barChart = echarts.init(chart);

      // 饼图配置
      const option = {
        // 背景色配置
        backgroundColor: 'transparent',

        // 图例配置
        legend: {
          data: ['凭证处理量', '项目户数'],
          textStyle: {
            color: '#fff',
          },
          top: 10,
        },

        // 网格配置
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true,
        },

        // X轴配置
        xAxis: {
          type: 'category',
          data: ['2018', '2019', '2020', '2021', '2022', '2023', '2024'],
          axisLine: {
            lineStyle: {
              color: '#fff',
              opacity: 0.1,
            },
          },
          axisLabel: {
            color: '#fff',
          },
        },

        // Y轴配置
        yAxis: {
          type: 'value',
          max: 1000,
          splitNumber: 4,
          splitLine: {
            lineStyle: {
              type: 'dashed',
              color: '#fff',
              opacity: 0.1,
            },
          },
          axisLabel: {
            color: '#fff',
          },
        },

        // 系列配置
        series: [
          {
            name: '凭证处理量',
            type: 'bar',
            barWidth: 10,
            itemStyle: {
              color: '#4324F6', // 深蓝色柱子
              borderRadius: [10, 10, 0, 0]
            },
            data: [200, 350, 550, 320, 520, 680, 250],
          },
          {
            name: '项目户数',
            type: 'bar',
            barWidth: 10,
            itemStyle: {
              color: '#2FD0E7', // 青色柱子
              borderRadius: [10, 10, 0, 0]
            },
            data: [850, 650, 380, 350, 580, 750, 320],
          },
        ],
      };

      barChart.setOption(option);
    },
  },
};
</script>

<style scoped>
/* 样式可以根据需要进行自定义 */
.echarts-bar {
  width: 100%;
  height: 100%;
}
</style>
