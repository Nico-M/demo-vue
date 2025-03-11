<template>
  <div>
    <Chapter title="债务风险">
      <div :style="{ height }">
        <TrendLineChart :chartData="chartData" />
      </div>
    </Chapter>
  </div>
</template>

<script>
import Chapter from './Chapter.vue';
import TrendLineChart from './TrendLineChart.vue';

export default {
  name: 'DebtRiskList',
  components: {
    Chapter,
    TrendLineChart,
  },
  props: {
    height: {
      type: String,
      default: '400px',
    },
  },
  data() {
    return {
      chartData: {
        halfYear: [250, 400, 350, 650, 400, 250, 300],
        thisYear: [300, 450, 620, 250, 300, 350, 400],
        lastYear: [200, 300, 250, 400, 600, 850, 600],
      },
    };
  },
};
</script>

<style lang="scss" scoped></style>
