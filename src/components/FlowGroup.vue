<template>
  <div class="flow-group">
    <ImgIcon :imgSrc="flowStartIcon" :size="30" />
    <ImgIcon :imgSrc="iconForward" :size="16" />
    <ImgButton :imgSrc="btnZD" :width="62" :height="44" text="制单"  />
    <ImgIcon :imgSrc="iconForward" :size="16" />
    <ImgButton :imgSrc="btnYWCL" :width="88" :height="44" text="业务处理" />
    <ImgIcon :imgSrc="iconForward" :size="16" />
    <ImgButton :imgSrc="btnCWCL" :width="88" :height="44" text="财务处理" />
    <ImgIcon :imgSrc="iconForward" :size="16" />
    <ImgButton :imgSrc="btnYZZ" :width="77" :height="44"  text="已制证"/>
    <ImgIcon :imgSrc="iconForward" :size="16" />
    <ImgIcon :imgSrc="flowEndIcon" :size="30" />
  </div>
</template>

<script>
import ImgIcon from '@/common/ImgIcon';
import ImgButton from '@/common/ImgButton';
import flowStartIcon from '@/assets/images/bigScreen/icon-flow-start.png';
import flowEndIcon from '@/assets/images/bigScreen/icon-flow-end.png';
import btnZD from '@/assets/images/bigScreen/img-btn-zd.png';
import btnYWCL from '@/assets/images/bigScreen/img-btn-ywcl.png';
import btnCWCL from '@/assets/images/bigScreen/img-btn-cwcl.png';
import btnYZZ from '@/assets/images/bigScreen/img-btn-yzz.png';
import iconForward from '@/assets/images/bigScreen/icon-forward.png';

export default {
  name: 'FlowGroup',
  components: {
    ImgIcon,
    ImgButton,
  },
  data() {
    return {
      flowStartIcon,
      flowEndIcon,
      btnZD,
      btnYWCL,
      btnCWCL,
      btnYZZ,
      iconForward
    };
  },
};
</script>

<style lang="scss" scoped>
.flow-group {
  display: flex;
  align-items: center;
  gap: 2px;
}
</style>
