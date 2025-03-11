<template>
  <div :class="$attrs.class">
    <ChapterHeader title="工作信息" />
    <div class="mt-8">
      <work-info-list :workList="workList" />
    </div>
  </div>
</template>

<script>
import ChapterHeader from './ChapterHeader.vue';
import WorkInfoList from './WorkInfoList.vue';

export default {
  name: 'WorkloadList',
  components: {
    ChapterHeader,
    WorkInfoList,
  },
  props: {
    workList: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style lang="scss" scoped></style>
