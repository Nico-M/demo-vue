<template>
    <div class="screen-three text-white">
      <ScaleBox :bgc="bgImagePath" ref="fixedContent">
        <screen-header />
        <div class="screen-content">
          <el-row>
            <el-col :span="5" class="relative">
              <div class="absolute top-0 left-0">
                <flow-group />
              </div>
              <div class="placeholder"></div>
              <ranking-list />
              <work-info  class="mt-16" height="240px"/>
              <token-process class="mt-16" height="240px" />
            </el-col>
            <el-col :span="14">
              <static-count />
              <BorderMap class="mt-16" />
              <div class="bottom-charts mt-16 flex gap-16 justify-around ">
                <DebtRiskList height="240px" />
                <AccountsReceivable height="240px" />
              </div>
            </el-col>
            <el-col :span="5">
              <query-bill-track class="mt-16" />
              <BasicProfile class="mt-16" />
              <AnnualWorkload class="mt-16" />
              <workload-list class="mt-16" :workList="workList" />
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
  import DebtRiskList from './components/DebtRiskList.vue';
  import AccountsReceivable from './components/AccountsReceivable.vue';
  import FlowGroup from './components/FlowGroup.vue';
  import QueryBillTrack from './components/QueryBillTrack.vue';
  import BasicProfile from './components/BasicProfile.vue';
  import AnnualWorkload from './components/AnnualWorkload.vue';
  import BorderMap from './components/BorderMap.vue';

  export default {
    name: 'screen-three',
    components: {
      ScaleBox,
      ScreenHeader,
      WorkInfo,
      TokenProcess,
      WorkloadList,
      RankingList,
      StaticCount,
      DebtRiskList,
      AccountsReceivable,
      FlowGroup,
      QueryBillTrack,
      BasicProfile,
      AnnualWorkload,
      BorderMap
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
        { id: '02', type: '人数户数', count: 245 },
        { id: '03', type: '人数户数', count: 125 },
        { id: '04', type: '人数户数', count: 125 },
        { id: '05', type: '人数户数', count: 125 },
        { id: '06', type: '人数户数', count: 125 },
        { id: '07', type: '人数户数', count: 125 },
          // ... 其他数据
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
  .screen-three {
    background-color: #090d1a;
    font-family: 'puhuiti', sans-serif;
  }
  .screen-content {
    padding: 0 20px;
  }
  .placeholder{
    height: 60px;
  }
  </style>
  <style lang="scss">
  @import './full-screen.scss';
  @import './design/util.scss';
  </style>
  