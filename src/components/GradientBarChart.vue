<template>
  <div ref="chart" class="echarts-bar"></div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: 'GradientBarChart',
  props: {
    chartData: {
      type: Object,
      default: () => ({
        finished: [550, 650, 320, 850, 320, 200, 650],
        unfinished: [120, 350, 180, 120, 150, 150, 380]
      })
    }
  },
  mounted() {
    this.initChart();
  },
  methods: {
    createStripePattern(color1, color2) {
      const canvas = document.createElement('canvas');
      canvas.width = 40;
      canvas.height = 40;
      const ctx = canvas.getContext('2d');
      
      // 创建渐变
      const gradient = ctx.createLinearGradient(0, 0, 40, 40);
      gradient.addColorStop(0, color1);
      gradient.addColorStop(1, color2);
      
      // 绘制条纹
      ctx.fillStyle = gradient;
      ctx.fillRect(0, 0, 40, 40);
      
      // 添加斜线条纹
      ctx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
      ctx.lineWidth = 3;
      ctx.beginPath();
      for (let i = -40; i < 80; i += 20) {
        ctx.moveTo(i, 0);
        ctx.lineTo(i + 40, 40);
      }
      ctx.stroke();
      
      return canvas;
    },
    initChart() {
      const chartDom = this.$refs.chart;
      const myChart = echarts.init(chartDom);
      
      const option = {
        backgroundColor: 'transparent',
        legend: {
          data: ['已完成', '未完成'],
          textStyle: {
            color: '#fff'
          },
          top: 10
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'category',
          data: ['2018', '2019', '2020', '2021', '2022', '2023', '2024'],
          axisLine: {
            lineStyle: {
              color: '#fff',
              opacity: 0.1
            }
          },
          axisLabel: {
            color: '#fff'
          }
        },
        yAxis: {
          type: 'value',
          max: 1000,
          splitNumber: 4,
          splitLine: {
            lineStyle: {
              type: 'dashed',
              color: '#fff',
              opacity: 0.1
            }
          },
          axisLabel: {
            color: '#fff'
          }
        },
        series: [
          {
            name: '已完成',
            type: 'bar',
            stack: 'total',
            barWidth: 10,
            itemStyle: {
              color: {
                type: 'pattern',
                image: this.createStripePattern('#7B48F8', '#4B5CC4'),
                repeat: 'repeat'
              },
              borderRadius: [10, 10, 0, 0],
              borderColor: '#0B1837',
              borderWidth: 1
            },
            data: this.chartData.finished
          },
          {
            name: '未完成',
            type: 'bar',
            stack: 'total',
            barWidth: 10,
            itemStyle: {
              color: {
                type: 'pattern',
                image: this.createStripePattern('#36D8D8', '#2B8F8F'),
                repeat: 'repeat'
              },
              borderRadius: [10, 10, 10, 10],
              borderColor: '#0B1837',
              borderWidth: 1
            },
            data: this.chartData.unfinished,
            z: 2
          }
        ]
      };

      myChart.setOption(option);

      // 添加响应式处理
      window.addEventListener('resize', () => {
        myChart.resize();
      });

      // 组件销毁时清理
      this.$once('hook:beforeDestroy', () => {
        window.removeEventListener('resize', myChart.resize);
        myChart.dispose();
      });
    }
  },
  watch: {
    chartData: {
      deep: true,
      handler() {
        this.initChart();
      }
    }
  }
};
</script>

<style scoped>
.echarts-bar {
  width: 100%;
  height: 100%;
}
</style>
