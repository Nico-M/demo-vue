<template>
  <div class="relative wrapper">
    <div ref="mapChart" style="height: 480px; width: 100%"></div>
    <!-- 返回按钮 -->
    <div class="back absolute left-0 top-0" v-if="selectedArea" @click="backToProvince">
      <i class="el-icon-refresh-left icon-button"></i>
      返回
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts';
import 'echarts-gl';
import roughnessImg from '@/assets/images/bigScreen/oil.jpg';
import borderJson from './border.json';

// 静态业务数据配置
const staticRegionBiz = {
  420500: ['YC市主城区污水厂网', '生态水网共建项目二期PPP工程'],
  421000: ['SS市中心城区水环境综合治理PPP项目'],
  420100: [
    'XXX流域综合治理一期工程',
    'XX东部区域清水入江PPP项目',
    'XX湖机场河流域分散式水处理服务项目',
    'xx中央生态大走廊空中轨道一期桩基土建预埋项目',
    'xx生态大走廊二期工程项目',
    'xx区新城镇建设PPP项目',
    'xx区农村村庄生活污水治理PPP项目',
  ],
  // 潼南区
  500152: ['xx区涪江流域水环境综合治理PPP项目'],
  500116: [' xx区水环境综合治理工程PPP项目'],
  500106: ['xxx“清水绿岸”治理提升工程PPP项目'],
  500113: ['xx区花溪河综合整治项目'],
  500110: ['xx区綦河流域水环境综合治理PPP项目'],
  500230: ['xx县水环境综合治理一期PPP项目'],
  431100: ['xx县城乡污水治理PPP 项目', '道县城乡水务一体化建设PPP项目'],
  430900: ['xx市中心城区水环境综合治理一期工程PPP项目'],
  430600: [
    'xx市中心城区污水系统综合治理PPP项目',
    'xx市君山区中心城区污水处理厂改扩建PPP项目',
    'xx县水环境综合治理PPP项目',
    'xx市水环境综合治理工程PPP项目',
  ],
  430100: ['xx市污水处理厂网一体PPP项目'],
  430200: ['xx市中心城区污水系统综合治理一期工程PPP项目'],
  341500: ['xx市城区水环境一期PPP项目'],
  340200: [
    'xx市城区污水系统提质增效（一期）项目',
    'xx市城区污水系统提质增效（二期）PPP项目',
    'xx市城区污水系统提质增效（三期）项目',
    'xx市江东水生态公园—中水回用示范项目',
    'xx市朱家桥污水处理厂光伏项目',
    '智慧水务建设',
    '十里江湾项目',
    'xx县城乡污水处理一体化PPP项目',
    'xx县农村污水治理试点扶贫项目',
    'xx市水环境综合整治PPP项目',
  ],
  360400: [
    'xx江市中心城区水环境系统综合治理一期项目',
    'xx江市中心城区水环境系统综合治理二期项目',
    'xx江市八里湖蓝藻应急治理项目',
    'xx江市中心城区雨污管网一体化示范工程项目',
    'xx省最美岸线（彭泽段）示范项目',
    'xx县沿江农村区域水环境综合处理工程',
    'xx县水环境综合治理PPP项目',
  ],
  320100: ['xx区农村污水处理设施全覆盖PPP项目'],
  330600: ['xx市陈蔡水库加固改造及水源地综合治理工程PPP项目'],
};

// 省份样式配置
const provinceStyles = {
  云南省: '#11A0FC',
  贵州省: '#53b6dd',
  湖北省: '#4B7FDE',
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
          distance: 80,
          alpha: 40,
          beta: 10,
          center: [-5, -5, 0],
          damping: 0.8,
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
      },
    };
  },

  mounted() {
    this.initMap();
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

    // 初始化省份地图
    initMap() {
      echarts.registerMap('border', borderJson);
      this.chart = echarts.init(this.$refs.mapChart);

      // 处理省份数据
      const mapdata = borderJson.features.map(item => {
        if (item.properties.name in provinceStyles) {
          return {
            ...item.properties,
            itemStyle: {
              color: provinceStyles[item.properties.name],
            },
          };
        }
        return item.properties;
      });

      this.chart.setOption({
        series: [this.getOption('border', mapdata)],
      });

      // 绑定点击事件
      this.bindClickEvent();
    },

    // 绑定地图点击事件
    bindClickEvent() {
      this.chart.on('click', async params => {
        if (!params.data) return;

        const { adcode, name, level } = params.data;

        // 处理区县级别点击
        if (level === 'district') {
          console.warn('无此区域地图显示！');
          this.initMap();
          return;
        }

        try {
          // 懒加载地图数据
          const mapData = await import(`../data/${adcode}.json`);
          this.renderCities(name, mapData);
          this.selectedArea = { name, adcode };
        } catch (error) {
          this.$message({
            type: 'error',
            message: '暂无数据',
          });
        }
      });
    },

    // 渲染城市地图
    renderCities(name, data) {
      if (this.chart) {
        this.chart.dispose();
        this.chart = null;
      }

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
            viewControl: {
              animation: true,
              animationDurationUpdate: 1000,
              distance: 80,
              autoRotateSpeed: 5,
              center: [0, -5, 0],
              autoRotate: true,
              minBeta: -Infinity,
              maxBeta: Infinity,
            },
            animationDurationUpdate: 2000,
            animationEasingUpdate: 'cubicInOut',
            universalTransition: true,
          },
        ],
        tooltip: {
          formatter(params) {
            return `城市: ${params.data.name}<br>`;
          },
        },
        labelLine: { show: true },
      });

      // 调整视角
    //   this.adjustView(name);
    },

    // 调整地图视角
    adjustView(name) {
      setTimeout(() => {
        this.chart.setOption({
          series: [
            {
              type: 'map3D',
              map: name,
              viewControl: {
                animation: true,
                animationDurationUpdate: 1000,
                distance: 100,
                autoRotateSpeed: 5,
                center: [0, -5, 0],
                autoRotate: true,
                minBeta: -Infinity,
                maxBeta: Infinity,
              },
              animationDurationUpdate: 2000,
              animationEasingUpdate: 'cubicInOut',
              universalTransition: true,
            },
          ],
        });
      }, 100);
    },

    // 返回省份地图
    backToProvince() {
      if (this.chart) {
        this.chart.dispose();
        this.chart = null;
      }
      this.initMap();
      this.selectedArea = null;
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
}

.back {
  text-decoration: underline;
  cursor: pointer;
  margin-left: 100px;
}
</style>
