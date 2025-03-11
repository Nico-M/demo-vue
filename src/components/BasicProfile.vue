<template>
  <Chapter title="人员基本信息">
    <div class="flex gap-12">
      <div class="avatar p-4">
        <ImgButton :imgSrc="bgOfAvatar" :width="78" :height="78" />
      </div>
      <div class="info">
        <div class="info-item flex items-center gap-16 mb-8">
          <ImgIcon :imgSrc="iconName" :size="24" />
          <div class="info-item-text">姓名:</div>
          <div class="info-item-value">张三</div>
        </div>
        <div class="info-item flex items-center gap-16 mb-8">
          <ImgIcon :imgSrc="iconCompany" :size="24" />
          <div class="info-item-text">单位:</div>
          <div class="info-item-value">XX集团</div>
        </div>
        <div class="info-item flex items-center gap-16 mb-8">
          <ImgIcon :imgSrc="iconDivision" :size="24" />
          <div class="info-item-text">所属部门:</div>
          <div class="info-item-value">资产与财务部</div>
        </div>
      </div>
    </div>
  </Chapter>
</template>

<script>
import ImgIcon from '@/common/ImgIcon';
import ImgButton from '@/common/ImgButton';
import bgOfAvatar from '@/assets/images/bigScreen/icon-avatar.png';
import iconCompany from '@/assets/images/bigScreen/icon-company.png';
import iconDivision from '@/assets/images/bigScreen/icon-division.png';
import iconName from '@/assets/images/bigScreen/icon-name.png';
import Chapter from './Chapter.vue';

export default {
  name: 'BasicProfile',
  components: {
    Chapter,
    ImgButton,
    ImgIcon,
  },
  data() {
    return {
      bgOfAvatar,
      iconCompany,
      iconDivision,
      iconName,
    };
  },
};
</script>

<style lang="scss" scoped>
.info {
  .info-item {
    background: linear-gradient(90deg, #386294 0%, rgba(38, 94, 163, 0.57) 64%, rgba(129, 185, 255, 0) 100%);
  }
}
</style>
