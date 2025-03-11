<template>
  <div class="chapter-header-container">
    <div class="chapter-header-title">{{ title }}</div>
  </div>
</template>

<script>
export default {
  name: 'ChapterHeader',
  props: {
    title: {
      type: String,
      default: '',
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../mixins.scss';
.chapter-header-container {
  min-width: 445px;
  height: 38px;
  @include bg-image('@/assets/images/bigScreen/bg-chapter-title');
  background-size: cover;
  background-position: center center;
  font-family: 'puhuiti', sans-serif;
}

.chapter-header-title {
//   font-family: AlimamaShuHeiTi;
  font-size: 18px;
  color: #eff1f6;
  line-height: 26px;
  margin-left: 42px;
  padding-top: 3px;
  font-weight: bold;
}
</style>
