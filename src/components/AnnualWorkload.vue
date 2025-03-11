<template>
  <Chapter title="年度工作量">
    <div ref="chart" class="echarts-bar"></div>
  </Chapter>
</template>

<script>
import * as echarts from 'echarts';
import Chapter from './Chapter.vue';

export default {
  name: 'AnnualWorkload',
  components: {
    Chapter,
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
          data: ['单据处理量', '凭据处理量'],
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
          data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
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
            name: '单据处理量',
            type: 'bar',
            barWidth: 10,
            itemStyle: {
              color: '#4324F6', // 深蓝色柱子
              borderRadius: [10, 10, 0, 0]
            },
            data: [200, 350, 550, 320, 520, 680, 250, 350, 550, 320, 520, 680],
          },
          {
            name: '凭据处理量',
            type: 'bar',
            barWidth: 10,
            itemStyle: {
              color: '#2FD0E7', // 青色柱子
              borderRadius: [10, 10, 0, 0]
            },
            data: [850, 650, 380, 350, 580, 750, 320, 350, 550, 320, 520, 680],
          },
        ],
      };

      barChart.setOption(option);
    },
  },
};
</script>

<style lang="scss" scoped>
.echarts-bar {
  width: 100%;
  height: 180px;
}
</style>