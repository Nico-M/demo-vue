<template>
  <div :class="$attrs.class">
    <ChapterHeader title="凭证处理量" />
    <div class="mt-8" :style="{ height }">
      <gradient-bar-chart :chartData="chartData" />
    </div>
  </div>
</template>

<script>
import ChapterHeader from './ChapterHeader.vue';
import GradientBarChart from './GradientBarChart.vue';

export default {
  name: 'TokenProcess',
  components: {
    ChapterHeader,
    GradientBarChart,
  },
  props: {
    height: {
      type: String,
      default: '380px',
    },
  },
  data() {
    return {
      chartData: {
        finished: [550, 650, 320, 850, 320, 200, 650],
        unfinished: [120, 350, 180, 120, 150, 150, 380],
      },
    };
  },
};
</script>

<style lang="scss" scoped></style>
