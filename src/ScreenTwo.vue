<template>
  <div class="screen-two text-white">
    <ScaleBox :bgc="bgImagePath" ref="fixedContent">
      <screen-header />
      <div class="screen-content">
        <el-row>
          <el-col :span="5">
            <work-info />
            <token-process class="mt-16" />
          </el-col>
          <el-col :span="14">
            <static-count />
            <!-- <china-map class="mt-16" /> -->
            <BorderMap />
          </el-col>
          <el-col :span="5">
            <ranking-list />
            <workload-list class="mt-32" :workList="workList" />
            <!-- <trend-line-chart :chartData="chartData2" /> -->
          </el-col>
        </el-row>
      </div>
      <!-- <div class="flex-box">
          <stacked-bar-chart :chartData="chartData3" />
        </div> -->
    </ScaleBox>
    <!-- 占位元素 -->
    <div class="placeholder" ref="placeholder"></div>
  </div>
</template>

<script>
import ScaleBox from './components/ScaleBox.vue';
import ScreenHeader from './components/ScreenHeader.vue';
import WorkInfo from './components/WorkInfo.vue';
import TokenProcess from './components/TokenProcess.vue';
import WorkloadList from './components/WorkloadList.vue';
import RankingList from './components/RankingList.vue';
import StaticCount from './components/StaticCount.vue';
import BorderMap from './components/BorderMap.vue';

export default {
  name: 'screen-two',
  components: {
    ScaleBox,
    ScreenHeader,
    WorkInfo,
    TokenProcess,
    WorkloadList,
    RankingList,
    StaticCount,
    BorderMap,
  },
  data() {
    return {
      chartData: {
        finished: [550, 650, 320, 850, 320, 200, 650],
        unfinished: [120, 350, 180, 120, 150, 150, 380],
      },
      mapData: [
        { name: '北京项目公司', value: [116.405285, 39.904989], amount: 100 },
        { name: '上海项目公司', value: [121.472644, 31.231706], amount: 200 },
        { name: '广州项目公司', value: [113.280637, 23.125178], amount: 300 },
      ],
      chartData2: {
        halfYear: [250, 400, 350, 650, 400, 250, 300],
        thisYear: [300, 450, 620, 250, 300, 350, 400],
        lastYear: [200, 300, 250, 400, 600, 850, 600],
      },
      chartData3: [
        { name: '香港本部公司', values: [80, 90, 95] },
        { name: '清源公司', values: [85, 95, 100] },
        // ... 其他数据
      ],
      bgImagePath: require('@/assets/images/bigScreen/bg-screen.png'),
      workList: [
        { id: '01', type: '人数户数', count: 345 },
        { id: '02', type: '人均管理户数', count: 345 },
        { id: '03', type: '累计办理资金收入笔数金额', count: 345 },
        { id: '04', type: '资金支出笔数金额', count: 345 },
        { id: '05', type: '累计编制资金计划', count: 345 },
        { id: '06', type: '编制预算报表', count: 345 },
        { id: '07', type: '税务申报次数', count: 345 },
        { id: '08', type: '年度财务报表户数每户份数', count: 345 },
        { id: '09', type: '季度财务报表户数每户份数', count: 345 },
        { id: '10', type: '月度财务报表户数每户份数', count: 345 },
      ],
    };
  },
  mounted() {
    this.updatePlaceholderSize();
    window.addEventListener('resize', this.updatePlaceholderSize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.updatePlaceholderSize);
  },
  methods: {
    updatePlaceholderSize() {
      const content = this.$refs.fixedContent;
      const { placeholder } = this.$refs;
      const clientRec = content.$el.getBoundingClientRect();
      placeholder.style.height = `${clientRec.height}px`;
    },
  },
};
</script>

<style lang="scss" scoped>
.flex-box {
  display: flex;
  gap: 20px;
}
.screen-two {
  background-color: #090d1a;
  font-family: 'puhuiti', sans-serif;
}
.screen-content {
  padding: 0 54px;
}
</style>
<style lang="scss">
@import './full-screen.scss';
@import './design/util.scss';
</style>
