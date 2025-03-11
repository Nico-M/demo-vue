<template>
  <Chapter title="工单跟踪查询">
    <div class="query-bill-track flex justify-between items-center gap-8">
      <ImgButton :imgSrc="iconSearch" :width="157" :height="29">
        <template #text>
          <div class="flex justify-around items-center">
            业务类型
            <ImgIcon :imgSrc="iconExpand" :size="20" />
          </div>
        </template>
      </ImgButton>
      <ImgButton :imgSrc="btnBgOfSearchBorder" :width="158" :height="28">
        <template #text>
          <div class="text-center" style="background: rgb(39 55 96 / 60%)">
            <input type="text" placeholder="请输入单号" class="track-input">
            </div>
        </template>
      </ImgButton>
      <ImgButton :imgSrc="btnBgOfQuery" :width="72" :height="44" text="查询"> </ImgButton>
    </div>
  </Chapter>
</template>

<script>
import iconSearch from '@/assets/images/bigScreen/bg-btn-biz-select.png';
import iconExpand from '@/assets/images/bigScreen/icon-expand.png';
import btnBgOfSearchBorder from '@/assets/images/bigScreen/bg-btn-record-bd.png';
import btnBgOfQuery from '@/assets/images/bigScreen/bg-btn-query.png';
import ImgButton from '@/common/ImgButton';
import ImgIcon from '@/common/ImgIcon';
import Chapter from './Chapter.vue';

export default {
  name: 'QueryBillTrack',
  components: {
    Chapter,
    ImgButton,
    ImgIcon,
  },
  data() {
    return {
      iconSearch,
      iconExpand,
      btnBgOfSearchBorder,
      btnBgOfQuery,
    };
  },
};
</script>

<style lang="scss" scoped>
.track-input {
  width: 100%;
  height: 100%;
  background: transparent;
  border: none;
  outline: none;
  color: #fff;
  text-indent: 10px;
  &::placeholder {
    color: #868686;
    text-align: center;
  }
}
</style>
