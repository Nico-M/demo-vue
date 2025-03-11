<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="img-button" :style="imgBtnStyle">
    <slot v-if="$slots.text" name="text"></slot>
    <template v-else>{{ text }}</template>
  </div>
</template>

<script>
export default {
  props: {
    imgSrc: {
      type: String,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
    width: {
      type: Number,
      required: true,
    },
    height: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      imgBtnStyle: {
        width: `${this.width  }px`,
        height: `${this.height  }px`,
        background: `url(${this.imgSrc}) no-repeat center center/cover`,
        backgroundSize: '100% 100%',
        lineHeight: `${this.height}px`,
        textAlign: 'center',
        fontSize: '16px',
        fontWeight: '600',
        fontFamily: 'puhuiti, sans-serif',
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.img-button {
  text-align: center;
  cursor: pointer;
}
</style>
