<template>
  <Chapter title="应收账款">
    <div :style="{ height }">
      <StackedBarChart  />
    </div>
  </Chapter>
</template>

<script>
import StackedBarChart from './StackedBarChart.vue';
import Chapter from './Chapter.vue';

export default {
  name: 'AccountsReceivable',
  components: {
    StackedBarChart,
    Chapter,
  },
  props: {
    height: {
      type: String,
      default: '400px',
    },
  },
  data() {
    return {
      chartData: [
        { name: '香港本部公司', values: [80, 90, 95] },
        { name: '清源公司', values: [85, 95, 100] },
        // ... 其他数据
      ],
    };
  },
};
</script>

<style lang="scss" scoped></style>
