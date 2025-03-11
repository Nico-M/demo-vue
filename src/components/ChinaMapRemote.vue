<template>
  <div class="china-map-container">
    <div ref="mapChart" class="map-chart"></div>
  </div>
</template>
<!-- eslint-disable no-unused-expressions -->
<script>
import * as echarts from 'echarts';
import { registerMap } from 'echarts/core';
import roughnessImg from '@/assets/images/bigScreen/soil.jpg';
import chinaMap from '../data/china.json'; // 你需要添加中国地图的 GeoJSON 数据
import 'echarts-gl';

export default {
  name: 'ChinaMapRemote',
  data() {
    return {
      chartInstance: null,
      cities: [
        { name: '北京', value: 100 },
        { name: '上海', value: 200 },
        { name: '广州', value: 300 },
        { name: '深圳', value: 400 },
      ],
    };
  },
  methods: {
    initChart() {
      // 注册地图数据
      registerMap('china', chinaMap);

      // 初始化图表
      this.chartInstance = echarts.init(this.$refs.mapChart);
      const mapdata = chinaMap.features.map(item => ({
        name: item.properties.name,
        value: item.properties.adcode,
      }));
      // 配置项
      const option = {
        tooltip: {
          // 提示框配置，显示地图交互信息
          show: true,
        },
        series: [
          // 系列列表
          {
            type: 'map3D', // 图表类型，设置为'map3D'表示3D地图
            map: 'china', // 地图类型，使用'china'表示中国地图
            roam: true, // 是否开启地图平移缩放
            regionHeight: 4, // 区域高度，单位为地图单位
            groundPlane: {
              // 地面配置
              show: false, // 设置false以隐藏地面
            },
            light: {
              // 光照相关配置
              main: {
                // 主光源配置
                intensity: 1.2, // 主光源强度
                shadow: true, // 是否显示阴影
                shadowQuality: 'medium', // 阴影质量
                alpha: 30, // 主光源水平角度
                beta: 40, // 主光源垂直角度
                color: '#fff', // 光源颜色
              },
            },
            viewControl: {
              // 视角控制配置
              distance: 50, // 视角距离主体的距离
              alpha: 40, // 视角绕 x 轴旋转角度
              beta: 0, // 视角绕 y 轴旋转角度
              center: [0, 3, 0], // 视角中心点位置
            },
            shading: 'realistic', // 着色效果，'realistic'表示真实感渲染
            realisticMaterial: {
              // 真实感材质配置
              roughness: 0.6, // 材质粗糙度
              metalness: 0.3, // 材质金属度
              textureTiling: [1, 3], // 材质贴图平铺
              detailTexture: roughnessImg, // 材质细节纹理贴图
            },
            label: {
              // 标签配置
              show: true,
              textStyle: {
                color: '#fff',
                fontSize: 12,
                backgroundColor: 'rgba(0,0,0,0)',
              },
            },
            emphasis: {
              // 高亮状态配置
              label: {
                show: true,
              },
              itemStyle: {
                color: '#fff',
              },
            },
            data: mapdata, // 地图数据
            instancing: true, // 是否开启实例化绘制
            itemStyle: {
              // 地图区域样式配置
              areaColor: '#101c38', // 区域颜色
              opacity: 0.8, // 区域透明度
              borderColor: '#9cd3fd', // 边框颜色
              borderWidth: 3, // 边框宽度
            },
          },
        ],
      };

      // 设置配置项
      this.chartInstance.setOption(option);
    },

    handleResize() {
      this.chartInstance && this.chartInstance.resize();
    },
  },
  mounted() {
    this.initChart();
    window.addEventListener('resize', this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize);
    this.chartInstance && this.chartInstance.dispose();
  },
};
</script>

<style lang="scss" scoped>
.china-map-container {
  width: 100%;
  height: 100%;

  .map-chart {
    width: 100%;
    height: 100%;
    min-height: 500px;
  }
}
</style>
