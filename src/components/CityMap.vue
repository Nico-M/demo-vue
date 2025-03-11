<template>
  <div class="relative wrapper">
    <div ref="mapChart" style="height: 480px; width: 100%"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';
import 'echarts-gl';
import roughnessImg from '@/assets/images/bigScreen/oil.jpg';

// 静态业务数据配置
const staticRegionBiz = {
  420500: ['宜昌市主城区污水厂网', '生态水网共建项目二期PPP工程'],
  421000: ['石首市中心城区水环境综合治理PPP项目'],
};

export default {
  name: 'BorderMap',

  data() {
    return {
      chart: null,
      selectedArea: null,
      // 地图基础配置项
      baseOption: {
        type: 'map3D',
        map: 'border',
        roam: true,
        regionHeight: 4,
        shading: 'realistic',
        // 材质相关配置
        realisticMaterial: {
          color: '#101c38',
          emission: '#1b3d7c',
          emissionIntensity: 0.3,
          detailTexture: roughnessImg,
          roughness: 0.5,
        },
        // 光照配置
        light: {
          main: {
            intensity: 1.2,
            shadow: true,
            shadowQuality: 'medium',
            alpha: 30,
            beta: 40,
            color: '#438dd7',
          },
        },
        // 视角控制
        viewControl: {
          animation: true,
          animationDurationUpdate: 1000,
          distance: 110,
          autoRotateSpeed: 5,
          center: [0, -20, 0],
          autoRotate: true,
          minBeta: -Infinity,
          maxBeta: Infinity,
        },
        // 区域样式
        itemStyle: {
          areaColor: '#101c38',
          opacity: 0.8,
          borderColor: '#9cd3fd',
          borderWidth: 3,
        },
        // 标签样式
        label: {
          show: true,
          color: '#000',
          fontSize: 16,
          fontFamily: "'puhuiti', sans-serif",
          backgroundColor: '#fff',
          opacity: 0.8,
          padding: 2,
          borderRadius: 4,
        },
        animationDurationUpdate: 2000,
        animationEasingUpdate: 'cubicInOut',
        universalTransition: true,
      },
    };
  },

  mounted() {
    this.renderCities('湖北省', '420000');
  },

  methods: {
    // 获取地图配置
    getOption(name, data) {
      return {
        ...this.baseOption,
        map: name,
        data,
      };
    },

    // 获取标签属性配置
    getLabelAttribute() {
      return {
        show: true,
        formatter(params) {
          const { adcode, name: city } = params.data;
          const projects = staticRegionBiz[adcode];
          const title = `{title|${city}}\n`;

          if (projects.length === 1) {
            return title + projects[0];
          }
          return title + projects.map((p, i) => `{item|${i + 1}.${p}}\n`).join('');
        },
        // 富文本样式配置
        rich: {
          title: {
            align: 'center',
            fontSize: 18,
            padding: [0, 0, 4, 0],
            color: '#fff',
            fontWeight: 'bold',
          },
          item: {
            padding: [4, 2],
          },
        },
        textStyle: {
          color: '#fff',
          fontSize: 16,
          fontFamily: "'puhuiti', sans-serif",
          backgroundColor: '#1f395e',
          opacity: 1,
          padding: [4, 2],
          borderRadius: 4,
        },
      };
    },
    // 渲染城市地图
    async renderCities(name, adcode) {
      if (this.chart) {
        this.chart.dispose();
        this.chart = null;
      }
      const data = await import(`../data/${adcode}.json`);

      this.chart = echarts.init(this.$refs.mapChart);
      echarts.registerMap(name, data);

      // 处理城市数据
      const mapData = data.features.map(item => {
        const { adcode: code } = item.properties;

        // 没有业务数据的城市
        if (!staticRegionBiz[code]) {
          return {
            ...item.properties,
            label: { show: false },
          };
        }

        // 有业务数据的城市
        const labelAttribute = this.getLabelAttribute();
        return {
          ...item.properties,
          label: labelAttribute,
          height: 10,
          itemStyle: {
            color: '#edc555',
          },
          emphasis: {
            label: labelAttribute,
          },
        };
      });

      // 设置地图配置
      this.chart.setOption({
        series: [
          {
            ...this.getOption(name, mapData),
          },
        ],
        tooltip: {
          formatter(params) {
            return `城市: ${params.data.name}<br>`;
          },
        },
        labelLine: { show: true },
      });
    },

  },

  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose();
      this.chart = null;
    }
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  width: 100%;
//   height: 100%;
}

.back {
  text-decoration: underline;
  cursor: pointer;
}
</style>
