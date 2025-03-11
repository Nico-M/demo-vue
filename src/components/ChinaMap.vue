<template>
  <div class="china-map-container">
    <transition name="fade" :css="false" @enter="onEnter" @afterEnter="onAfterEnter" @leave="onLeave">
      <ul class="china-map relative" v-if="show">
        <li
          class="vision-bar fade-in-out"
          v-for="(item, index) in visionBarList"
          :key="index"
          :style="{
            left: item.left + 'px',
            top: item.top + 'px',
            // animationDelay: index * 1 + 's', // 添加延迟，使每个元素错开显示
          }"
        >
          项目公司名称
        </li>
      </ul>
    </transition>
  </div>
</template>

<script>
import { animate } from 'motion';

export default {
  name: 'ChinaMap',
  props: {},
  data() {
    return {
      visionBarList: [
        { left: 398, top: 106 },
        { left: 553, top: 189 },
        { left: 624, top: 153 },
        { left: 570, top: 250 },
        { left: 780, top: 26 },
        { left: 658, top: 260 },
      ],
      show: false,
    };
  },
  methods: {
    async onEnter(el, onComplete) {
      // 使用 animate 方法，传入 el 和动画配置对象
      const sequence = [[el, { opacity: 1 }], ...Array.from(el.querySelectorAll('li')).map(li => [li, { y: [-5, 0], opacity: 1 }])];

      await animate(sequence);
      onComplete();
    },

    onLeave(el) {
      // 使用 animate 方法，传入 el 和动画配置对象
      animate(el, { opacity: 0, translateY: 10 }, { duration: 50 });
    },

    onAfterEnter(el) {
      // 使用 animate 方法，传入 el 和动画配置对象
      animate(
        el.querySelectorAll('li'),
        { color: ['#fff', '#fbdb55', '#fff'], scale: [1, 1.2, 1], opacity: [1, 0.8, 1] },
        { repeat: Infinity, duration: 5 },
      );
    },
  },
  mounted() {
    // 延迟显示以触发 enter 动画
    this.$nextTick(() => {
      this.show = true;
    });
  },
};
</script>

<style lang="scss" scoped>
@import '../mixins.scss';
.china-map {
  width: 938px;
  height: 583px;
  @include bg-image('@/assets/images/bigScreen/img-map');
  background-size: cover;
  margin: 0 auto;
  background-position: center center;
}

.vision-bar {
  @include bg-image('@/assets/images/bigScreen/img-vision-bar');
  background-size: cover;
  background-position: center center;
  width: 24px;
  height: 166px;
  position: absolute;
  font-size: 12px;
  writing-mode: vertical-lr; // 添加竖排显示
  text-orientation: upright; // 保持文字正向
  display: flex; // 添加flex布局
  justify-content: flex-start; // 水平居中
  align-items: flex-end;
  // animation: fadeInOut 10s infinite; // 添加动画
  opacity: 0; // 确保初始状态为不可见
  //visibility: hidden; // 添加 visibility 属性
  //animation-fill-mode: forwards; // 添加 fill-mode
}

@keyframes fadeInOut {
  0% {
    opacity: 0;
    visibility: hidden;
    transform: translateY(10px);
  }
  20% {
    opacity: 1;
    visibility: visible;
    transform: translateY(0);
  }
  80% {
    opacity: 1;
    visibility: visible;
    transform: translateY(0);
  }
  100% {
    opacity: 0;
    visibility: hidden;
    transform: translateY(-10px);
  }
}
</style>
