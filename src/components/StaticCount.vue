<template>
  <div class="static-count">
    <div v-for="(item, index) in list" :key="index" class="count-item">
      <div class="count-number">{{ item.count }}</div>
      <div class="count-title">{{ item.title }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StaticCount',
  data() {
    return {
      list: [
        { count: '23414', title: '公司户数' },
        { count: '23543', title: '项目总数' },
        { count: '13376', title: '相关区域负责人' },
        { count: '96567', title: '所辖财务人数' },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
@import '../mixins.scss';
.static-count {
  display: flex;
  justify-content: center;
  gap: 30px;
  flex-grow: 1;

  .count-item {
    flex: 0 0 auto;
    position: relative;
    padding: 20px;
    border-radius: 4px;
    text-align: center;
    width: 130px;
    height: 114px;
    @include bg-image('@/assets/images/bigScreen/bg-data-base');
    background-position: center center;
    background-size: cover;
    cursor: pointer;
    .count-number {
      font-family: 'pangmenzuodaoti';
      font-size: 32px;
      color: #fff;
      margin-bottom: 8px;
    }

    .count-title {
      font-family: 'puhuiti';
      font-size: 14px;
      color: #7ec7ff;
    }

    &:hover {
      .count-number {
        transform: scale(1.1);
        transition: transform 0.3s ease;
      }
    }
  }
}
</style>
