<template>
  <div>
    <ChapterHeader title="工作信息" />
    <div class="mt-8">
      <div class="switch-tab">
        <div class="switch-tab-item active">工作量</div>
        <div class="switch-tab-item inactive">工作效率</div>
      </div>
      <div class="mt-8" :style="{ height }">
        <bar-chart-one />
      </div>
    </div>
  </div>
</template>

<script>
import ChapterHeader from './ChapterHeader.vue';
import BarChartOne from './BarChartOne.vue';

export default {
  name: 'WorkInfo',
  components: {
    ChapterHeader,
    BarChartOne,
  },
  props: {
    height: {
      type: String,
      default: '390px',
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../mixins.scss';
.switch-tab {
  display: flex;
}
.switch-tab-item {
  width: 50%;
  height: 32px;
  padding: 0 10px;
  line-height: 32px;
  @include bg-image('@/assets/images/bigScreen/btn-inactive');
  background-position: center center;
  background-size: cover;
  &.active {
    @include bg-image('@/assets/images/bigScreen/btn-active');
  }
  &.inactive {
    margin-left: -8px;
    padding-left: 18px;
  }
}
</style>
